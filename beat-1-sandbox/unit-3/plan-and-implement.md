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

PENDING: will be added later.

---

## Your branch

**Branch**

fix/56-structural-chunker-no-headings

**Evidence**

PENDING: will be added later.

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
