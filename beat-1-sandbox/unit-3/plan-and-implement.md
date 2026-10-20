# Unit 3 — Plan and Build

Path: `beat-1-sandbox/unit-3/plan-and-implement.md`

Record of your plan, the branch you built it on, and the evaluation runs that produced
`eval-run.txt`. This file is graded at the path above; a copy kept anywhere else in the
repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Posted upstream

**GitHub username**

LilRed92

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s1/issues/56#issuecomment-6262649663

Posted text:

> Plan for #56, building on my reproduction above. I ran it on an earlier checkout (`5963b35`); `_extract_sections` is the same on current `main` (`f89c06f`), and I am re-running it there before building.
>
> **Cause:** in `_extract_sections` (`ingestion/chunking/structural_chunker.py`, line 120 on `main`), content lines are only collected once a heading has been seen. A document with no headings collects nothing, so `chunk()` returns `[]`. My control run (same text with one leading `# Title`) returned 1 chunk, and `test_document_with_no_headings` fails with `assert 0 >= 1`, so the trigger is the missing heading.
>
> **Change:** if no heading sections are found and the text is not blank, `_extract_sections` returns the whole document as one section (empty path, level 0). `chunk()` already handles that section and already sub-chunks anything over the token limit. One function, plus tests: I will remove the strict `xfail` marker on `test_document_with_no_headings` (otherwise the fix makes it fail) and add one regression test for the long-document path.
>
> **Not in this change:** text before the first heading in a document that does have headings. It looks like the same condition drops it, but I did not test it, so I'd treat it as a separate issue.
>
> **Test:** re-run my repro command (expect `1`, was `0`), the heading control (expect `1`), `test_document_with_no_headings` (expect pass), then the full `test_structural_chunker.py` file.
>
> **Open question:** the fallback chunks get an empty `heading_path`. Inside this repo nothing outside the chunker reads it, but I have not checked consumers elsewhere. If you would prefer the fallback in `chunk()` rather than `_extract_sections`, say so.
>
> Note: I used an AI assistant to help draft this plan. I ran the reproduction and read the code myself, and I understand what I am proposing.

---

## Your branch

**Branch**

fix/56-structural-chunker-no-headings

**Evidence**

Branch `fix/56-structural-chunker-no-headings` in my fork, base `f89c06f`, Python 3.12.15, pytest 9.1.1. Same script and same test file run twice: once on the unmodified base (fix stashed), once with the fix applied. Captured with `week-4/ev.sh before` and `ev.sh after` on 2026-10-19.

| Check | Before (no fix) | After (fix) |
|---|---|---|
| Headingless text, short (`StructuralChunker().chunk`) | 0 chunks | 1 chunk |
| Headingless text, long (sub-chunked past the token limit) | 0 chunks | 4 chunks |
| Control, same text with a leading `# Title` | 1 chunk | 1 chunk |
| `test_document_with_no_headings` | XFAIL | PASSED |
| `test_long_document_with_no_headings_is_not_dropped` | not present | PASSED |
| `tests/unit/test_structural_chunker.py` | 14 passed, 1 xfailed (15 tests) | 16 passed |

The control stays at 1 chunk in both runs, so the change affects only documents with no headings. The pre-fix xfail reason reads: `issue #56: structural chunker drops documents with no headings`.

Plan-check on the plan and the posted comment returned `accept`, with all 7 checks passing.

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

1. Partial run, 6 packages (pkg-04, pkg-20, pkg-07, pkg-15, pkg-17, pkg-09): 6/6.
2. Full run, 20 packages: 19/20 (`agreement: 19/20 scored items  (bar: 18/20: PASS)`), saved to `eval-run.txt`.

**Package analysis**

`pkg-14` (zellij-org/zellij#5174). The gold label is accept; my rubric decided reject, and the run's note column said `failed: executable`.

The plan's diagnosis, scope and test plan all passed. The failure came from its Files line: "exact functions to be pinned in the PR after tracing the query issuance with debug logs". The plan names an area (the client attach path in `zellij-server` and `zellij-client`'s terminal query issuance) and one chosen approach (consume pending OSC color query responses in the reattach handshake), but it defers the specific function to build time. My "executable" check passes only if the plan "names the specific file, function or module it will change", and it fails if "a core decision is deferred to build time". Naming the exact function was the part deferred, so the check read it as a fail.

I think the gold label is defensible: the plan is bounded, has a decisive test and states its risk, and a contributor could start by tracing the debug output as it describes. The staff note calls it "arguable on the deferral, ready as scoped". My check cannot tell a deferred function name from a deferred decision, and I did not change it.

**Check rationale**

The "executable" row, exactly as it reads in `tools/plan-check/rubric.md`:

> | executable | the plan's named files, functions or modules, and its approach or ordered changes. | pass if the plan names the specific file, function or module it will change and states one chosen approach, so a stranger could start without asking the author. fail if the location is vague ("somewhere", "upstream or vendored, whichever is easier"), if the approach is an investigation with no chosen fix, if a core decision is deferred to build time, or if no file or area is named. | required |

It reads that way because the unbuildable packages (pkg-10, pkg-17, pkg-18) fail for the same reasons the fail clause lists: no files, no chosen approach, and decisions pushed to build time ("whichever is easier" is quoted from pkg-18). I wrote the pass condition around two outcomes a reader can verify, a named location and one chosen approach, instead of how detailed the plan looks, so two graders would agree. I kept it `required` because a plan nobody can start is not ready to post. I did not revise this row after the full run, even though it cost pkg-14.

**Trade-offs**

The "executable" check gives up plans that name the right area and approach but defer the exact function, which is pkg-14, so it changes that package's result (gold accept, mine reject). I accept that miss. Loosening it to allow "an area and one chosen approach" would let pkg-14 through, but it would also move the line for pkg-10, pkg-17 and pkg-18, whose gold notes describe vague or deferred decisions, and a single full run is the only way to see which way those would flip. The run was already 19/20 with every category matched, so I changed nothing after it. I did not re-run any canaries with `--only`, because I made no loosening change that needed one. The files in `eval-run.txt` match the files in `tools/plan-check/` (same hashes in the run header), which is how I know the run describes the rubric I uploaded.

---

Related paths: `plan.md` and `eval-run.txt` in this directory; your skill's files in
`tools/plan-check/`.
