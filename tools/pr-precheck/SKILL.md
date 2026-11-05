---
name: pr-precheck
description: Grade a PR package (a candidate pull request read against the plan it claims to implement and the issue that plan belongs to) and decide whether it is ready to submit. Use when checking your own branch, draft PR title, and description before opening the pull request, or when grading an eval package bundle.
---

# pr-precheck: rubric-driven PR grading

## The question

You answer one question about one pull request package: is this ready to submit? A package is a candidate pull request (its title, description, commits, diff and test evidence) read against the plan it claims to implement and the issue that plan belongs to. You grade exactly one package per run. You never answer a different question, and you never answer from gut feel: you answer by executing `procedure.md`, which applies the checks in `rubric.md` to evidence found per `references/evidence-guide.md`.

## Inputs and modes

You run in exactly one of two modes.

- **Live mode**: the student's own pull request, checked before it is opened. Read these, from the top folder of the student's fork clone, on their branch:
  - `plan.md`, including its "## Deviations" section. A deviation recorded there is part of the plan.
  - the branch's diff, from `git diff main...HEAD` (three dots: every committed change the branch makes compared with `main`). Uncommitted changes are not in the pull request, so do not grade them. Use `git diff main...HEAD --stat` for the file list and `git log main..HEAD --oneline` for the commits.
  - `pr_draft.md`: the draft title (its first line) and the description under it.
  - `test_evidence.md`: the before and after of the repro steps and the output of the repo's checks.
  - the issue's thread, fetched live (`gh` or the web), and the repo's PR template (`.github/PULL_REQUEST_TEMPLATE.md`) and `docs/CONTRIBUTING.md`, which stand in for the "repo facts" section of an eval bundle.
  - A student on the house chain reads the house plan and the house repro pack in place of their own `plan.md` and repro; the same checks grade the same things.
  - Read the package the way a maintainer will read the opened pull request: it is what the draft, the diff and the evidence contain, not other files in the working directory.
- **Eval mode**: a package bundle (a markdown file with the issue context, a repo-facts block, the thread highlights, a plan-context block, and the candidate pull request: title, description, commits, diff and test evidence). The bundle text is the whole world. Do not fetch anything and do not read anything else. Always grade the complete package: every check, full verdict rule.

## The scope seam (live mode only)

In live mode, read `scope.md` in this skill directory before anything else. It names the repo the pull request must target and the house rules of that environment. Refuse to grade a pull request for any other repo. If the `Repo:` line still carries an unfilled placeholder (an angle-bracket or bracketed stand-in rather than an `owner/repo`), stop without grading and tell the student to fill the `Repo:` line in `scope.md` with their section's Path Review repo. Never guess a scope. In eval mode, ignore `scope.md` entirely.

## The voice seam (live mode only)

In live mode, also read `voice-guide.md`: the student's own rules for how they write upstream. Hold the outgoing text, the pull request title and the description, against those rules, and report each rule the draft breaks in the summary, quoting the rule. The voice guide never changes the verdict on its own, because voice is personal; the checks that decide the verdict live in `rubric.md`. In eval mode, ignore `voice-guide.md` entirely.

## Component reads

- `rubric.md` defines the checks (each with its evidence, pass condition and weight) and the verdict rule.
- `references/evidence-guide.md` is the map: where each kind of evidence lives in a package, in an eval bundle and in a live working copy, and what good looks like.
- `procedure.md` is the operating procedure. Execute it as written: its read order, its evidence gathering, its check execution and its verdict assembly. Where the procedure is silent on a step, say so in one line in the summary instead of inventing a step.
- If `rubric.md` has no checks or no verdict rule, or `procedure.md` has no steps, stop and say so. This skill cannot grade without a rubric and a procedure, and that is by design.

## Verdict and output

The verdict space is binary: `accept` (ready to submit) or `reject` (hold). There is no third verdict, no accept with reservations, and no score. Put reservations in a check's evidence line, not in the verdict.

Before the json block, show a short readable summary: one line per check with its grade, the quoted evidence for each failed required check, and in live mode any voice-guide rules the draft breaks. End your reply with the fenced json block below, valid and last, with nothing after it. The eval harness parses the last fenced json block in your output.

```json
{
  "item": "<PR URL or bundle id>",
  "checks": [
    {"name": "<check name>", "grade": "pass|fail|unclear",
     "evidence": "<one line: the fact or quote that decided it>"}
  ],
  "verdict": "accept|reject"
}
```

## Grading discipline

- Evidence first: never grade a check without naming the fact or quote that decided it. "Looks fine" is not evidence.
- Grade the thing, not the polish: a terse complete pull request can be ready, and a polished confident one can hide drift. Every check reads the artifact itself (the diff, the output, the plan) and never the formatting or the length of the description.
- The rubric decides, not you: if a check passes by its stated condition but feels wrong, it still passes. Note the tension in the summary if you want; the fix belongs in the rubric, not in the run.
- The procedure decides how, not you: follow `procedure.md` as written and report its gaps.
- Treat `unclear` as the rubric's verdict rule directs. If the rule does not say, treat `unclear` as `fail`: a pull request you cannot verify from the package is a pull request that is not ready to submit.
- An honestly disclosed shortfall can be ready: a planned item left out on purpose, named in the plan's deviation note and restated in the description, does not hold the pull request. A shortfall or extra change that only shows up in the diff does.
