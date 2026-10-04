# Evidence guide: where proof lives in a reproduction package

<!--
THIS IS THE PART YOU WRITE (new this week: Unit 1 handed you this file
finished; the scaffolding fades). The skill uses this guide as its map:
for every kind of proof a rubric check names, this file says WHERE to
find it in a package and WHAT GOOD LOOKS LIKE when you do.

Under each family heading below, write:

- Where it lives: the exact places to look. In an eval bundle (which
  section of the package: the issue context, the repo-facts block, the
  claim comment, the repro report and its parts). In live mode (where
  on GitHub or in the draft: the issue thread, the repo's docs, the
  student's draft comment).\
- What good looks like: one or two sentences someone else could apply.
  Prefer observable conditions ("the versions named match what the
  issue targets, or the difference is called out") over adjectives
  ("environment is thorough").

A rubric check whose evidence this guide cannot locate is a check
nobody else can execute; the rubric swap showed you what that feels
like. Write the map you wish your grader had.
-->

## Environment

Where it lives: The repro report's opening block or first paragraph, typically labeled "Environment:" or equivalent. In an eval bundle, look at the top of the "Candidate repro report" section. In live mode, look at the top of the draft repro comment.

What good looks like: The report names a specific OS (including version or distro), the exact version or commit of the tool or library under test, and any driver or build variant the issue's own description calls out as relevant. If the reporter tested on a version different from the one the issue targets, good looks like: the deviation is named and called out (not silently swapped). A bare "Windows" with no driver on a driver-specific Windows issue is not sufficient.

## Steps

Where it lives: The reproduction steps section of the repro report, usually a numbered list. In an eval bundle, this is inside the "Candidate repro report" section. In live mode, it is the numbered steps in the draft.

What good looks like: The steps form a self-contained sequence: they start from a fresh install, clone, or known state and end at the point where the bug fires. Every command is shown verbatim. A stranger who has never seen the repo before could paste the commands in order and reach the trigger. Steps that reference private files, unshared config, or simply say "watch it loop" without showing what to run are not followable.

## Behavior shown

Where it lives: The output excerpts, terminal captures, test output, or screenshots embedded in the repro report, using fenced code blocks or inline quotes. In an eval bundle, this is the artifact content inside the "Candidate repro report" section, read against the issue body in the "## Issue" section. In live mode, these are the raw output blocks in the draft repro comment, checked against the issue page.

What good looks like: The shown artifact matches the failure mode the issue describes : same class of error, same exit code, same observable deviation. A control run (showing the behavior does not occur under a slightly different condition) strengthens the match but is not required to pass. An honest cannot-reproduce passes if: there is a real attempt with real output, the output is shown verbatim, and the reporter names what differed from the issue's setup. A confident reproduction of an adjacent symptom (different error type, different exit code, graceful validation error instead of crash) fails even when the prose says "reproduced."

## Honesty

Where it lives: The claim in the prose (what the repro report asserts happened) compared against the artifacts shown in the same report. In an eval bundle, look for the "Expected" / "Actual" or equivalent framing in the repro report, then read it against the literal artifact blocks above it. In live mode, compare the summary sentences in the draft to the output blocks in the same draft.

What good looks like: The prose description matches what the artifacts actually show. "Reproduced the crash" is honest when the artifact is a stack trace ending in a process exit; it is not honest when the artifact is a graceful validation message. An evidenced cannot-reproduce : where the artifact shows the bug did not fire, the reason is stated, and the reporter does not assert success they did not achieve : is a passing honest report.

## Comms

Where it lives: The candidate claim comment (the "## Candidate claim comment" section in an eval bundle; the claim draft in live mode). Also the repo-facts block for contribution policy and AI policy, and both comment drafts for convention compliance.

What good looks like: The claim comment names the specific issue (by symptom, behavior, or ID) and describes what the contributor will do next in concrete terms (reproduce, investigate a specific component, post findings). It does not promise a timeline, a guaranteed fix, or a delivery date. It is not a generic "+1", a "please assign me" with no intent, or a boilerplate assign-request. For AI disclosure: if the repo's contribution policy or AI policy states that AI-assisted work must be disclosed, at least one of the posted comments (claim or repro) includes an explicit statement that AI assistance was used.
