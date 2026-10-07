# Plan: issue #56, StructuralChunker drops documents with no headings

## Diagnosis

`StructuralChunker.chunk()` returns an empty list for any document that contains no markdown heading. In `_extract_sections` (`ingestion/chunking/structural_chunker.py`), a line of regular content is only collected when a heading has already been seen:

```python
if heading_stack or current_section_lines:  # Only collect if we have a heading
    current_section_lines.append(line)
```

For a headingless document both `heading_stack` and `current_section_lines` stay empty, so no line is ever collected, no section is built, and `chunk()` has nothing to loop over.

The line is at line 120 of `structural_chunker.py` on `main` at `f89c06f`. This follows from my reproduction, which I posted on the issue. I originally ran it on an earlier checkout (`5963b35`) with the same code in `_extract_sections`, and I am re-running it on `f89c06f`, before and after the fix. The posted results were:

- Headingless text: `.venv/bin/python -c "...print(len(c.chunk('This is a plain document with no headings at all. ' * 20, {})))"` printed `0`.
- Control, same text with one leading `# Title` heading: printed `1`. The control isolates the trigger to the absence of a heading, not the text, its length, or the metadata.
- Unit test: `tests/unit/test_structural_chunker.py::TestStructuralChunker::test_document_with_no_headings` fails with `assert 0 >= 1` (`where 0 = len([])`).

Expected (from the test): `len(result) >= 1`. Actual: `[]`.

## Scope

In scope: when a non-blank document yields no heading sections, `_extract_sections` returns the whole document as one section, so `chunk()` produces at least one chunk. One function, one file.

Not in scope:
- Text that appears before the first heading in a document that does have headings. The same condition looks like it would drop that text too, but my repro did not test it, so I am leaving it for a separate issue.
- Any change to `chunk()`, the semantic chunker, the token limit, or other chunkers.
- Any change to how headed documents are split.

## Files I will touch

- `ingestion/chunking/structural_chunker.py` (`_extract_sections`)
- `tests/unit/test_structural_chunker.py`: remove the `xfail(strict=True)` marker on `test_document_with_no_headings` (it is marked as the known failure for this issue, and a strict xfail turns an unexpected pass into a failure), and add one regression test

## Approach

1. In `_extract_sections`, after the final-section save, add a fallback: if `sections` is empty and `text.strip()` is non-empty, append one section with `content` set to the stripped text, `path` set to an empty list, and `level` set to `0`.
2. `chunk()` already handles a section with an empty path (`" > ".join([])` gives an empty `heading_path`) and already sub-chunks large sections through the semantic chunker, so no change is needed there.
3. Remove the strict `xfail` marker from `test_document_with_no_headings` so the existing test guards the fix.
4. Add one regression test that a long headingless document (over `SECTION_TOKEN_LIMIT`) is returned as non-empty chunks, so the semantic sub-chunking path is also covered.

## Test plan

Re-run my Unit 2 repro steps from the repository root, with the output I expect after the fix:

1. Headingless command above: expected `1` (was `0`).
2. Control command with `# Title`: expected `1` (unchanged).
3. `.venv/bin/python -m pytest tests/unit/test_structural_chunker.py::TestStructuralChunker::test_document_with_no_headings`: expected pass (was `assert 0 >= 1` with the xfail marker removed).
4. `.venv/bin/python -m pytest tests/unit/test_structural_chunker.py`: expected to pass in full, including the new long-document test, to show existing headed-document behavior did not change.

## Risks and unknowns

- An empty `heading_path` and `heading_level` of `0` on these chunks is my choice. I searched the repository at `f89c06f` for other uses of `heading_path` and `heading_level`: outside the chunker itself and its own test file, only a docstring in `ingestion/chunking/base.py` mentions `heading_path`, and no code reads it. I have not checked runtime consumers outside this repository.
- My original repro ran on `5963b35`, not `f89c06f`. The code is the same, but I have not yet confirmed the same output on `f89c06f`; I will check that on the unfixed code first.
- I have not confirmed whether the maintainers prefer this fallback in `_extract_sections` or in `chunk()`. I chose `_extract_sections` because that is where my repro traced the cause.

## Deviations

Nothing changed from the plan as posted; it held. One thing I found while writing it, before posting: `test_document_with_no_headings` carried a strict `xfail` marker for this issue, so the fix would have turned that test into a failure until the marker was removed. Removing it is listed in the plan above, and the build did exactly that plus the fallback and one new test.
