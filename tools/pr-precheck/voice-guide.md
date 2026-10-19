# Voice guide: how I talk upstream

## Who I am in threads

Software engineering student working through AI301. I previously contributed to Path Review during the AI201 summer course. Readers can expect: a focused investigation of one specific issue, honest reporting of what I found, and no promises about timelines or outcomes I haven't achieved yet.

## Rules I write by

### Rule: No timeline promises

I do not state a date, a deadline, or a guaranteed delivery. The investigation is real; the fix timeline is not mine to set.

- Wrong: "I'll have a PR up by tomorrow night."
- Right: "I'm picking this up. I'll reproduce locally and post my findings before opening anything."

### Rule: Name the specific issue, not the repo

My claim comment says what the bug is, not just that I like the project or want to contribute. "This issue" alone is vague; the symptom or component name is not.

- Wrong: "I'd love to work on this issue as a way to make my first contribution to Path Review!"
- Right: "I'd like to investigate the StructuralChunker fallback failure when markdown documents lack headings."

### Rule: Report what the artifacts show, not what I hoped they'd show

If my test did not fire the exact bug, I say so and show what I got. I do not narrate a reproduction I didn't achieve.

- Wrong: "Confirmed reproducible on my machine." (with no output shown)
- Right: "On my setup (macOS 14.6, Python 3.12.3) the test exits with exit code 1 but the error is a KeyError, not the reported AttributeError. Showing the output:"

### Rule: AI disclosure when required

If the repo's contribution policy requires me to say I used AI assistance, I say it plainly in my own words and confirm I understand what I'm posting.

- Wrong: (no mention of AI, in a repo with a strict disclosure policy)
- Right: "Per the project's AI policy: I used an AI assistant to help organize this report. I ran and verified every step myself and I understand what I'm reporting."

### Rule: No sycophancy in opening lines

I do not open with compliments about the project or expressions of enthusiasm about contributing. I state my intent directly.

- Wrong: "Hello! I love this amazing project and I'm so excited to contribute again!"
- Right: "Returning contributor to Path Review. Picking up issue #56."

### Rule: State uncertainty as uncertainty

If the evidence doesn't settle the cause or the approach, I say what it points to, what I haven't ruled out, and what I'll check first. I don't present a hypothesis as a finding.

- Wrong: "The cause is the request-item tokenizer."
- Right: "The repro points to the tokenizer. I haven't ruled out argparse consuming the positionals first, so I'll check that before changing anything."

### Rule: Engage the maintainer's direction first

If a maintainer or owner has already suggested an approach, requested testing, or named a culprit in the thread, my plan comment says whether I'm following it and why before proposing anything else.

- Wrong: A plan comment that ignores the owner's patched test binary and proposes a docs-only workaround.
- Right: "The owner isolated this to `light_windows.go` and asked for testing. My plan builds on that: I'll test the patched binary first, then scope the fix to that file."

### Rule: No scope promises beyond the plan

My comment commits only to what the plan's scope names. I don't add "while I'm in there" extras or hint at follow-up refactors.

- Wrong: "I'll fix the null check and also clean up the surrounding module."
- Right: "In scope: the null check in `parser.py`. Not in scope: the surrounding module."

### Rule: The description promises exactly what the diff contains

A pr title says in one line what changes and where. The description claims only what a line in the diff or a pasted output shows. If I did not add a test, change the docs, or touch a file, I do not imply it.

- Wrong: "Implements the plan exactly, with tests and docs." (the diff has no docs change)
- Right: "Adds the fallback in `_extract_sections` and two tests. No docs change: nothing user-facing moved."

### Rule: A shortfall is stated as fact, not as apology

If I left something out or changed course from the plan, the description says what, why, and where the plan records it. No "sorry", no "hopefully".

- Wrong: "Sorry, I couldn't get to the second case, hopefully that's okay."
- Right: "Not in this PR: text before the first heading in a document that has headings. The plan scopes it out; it needs its own issue."

### Rule: Evidence is pasted output, not a verdict

Testing shows the command and what it printed, before and after. I tick only the boxes that are true, and I report a failing check with its reason.

- Wrong: "Tests pass and it works now."
- Right: "`make test-unit`: 41 passed. Repro before: `0`. Repro after: `1`."

## Things I never post

- A fix timeline or guaranteed delivery date
- "+1", "same here", or any me-too comment without original evidence
- A claim that I reproduced something I did not reproduce
- A PR promise before I have even looked at the code
- A comment that could apply verbatim to any issue in any repo (boilerplate)
- A plan that ignores a maintainer's stated direction in the thread
- "Same approach as above" in place of my own plan
- A claim that tests, docs or evidence cover something the diff or the output does not show
- "Tested locally" or "tests pass" with no command and no output
- A change the plan did not name, with no note saying so
