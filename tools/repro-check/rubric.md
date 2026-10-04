# Rubric: is this reproduction package ready to post?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever
checks you define here. It ships empty on purpose: the judgment is your
work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four
   columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where in the package. Name
     the part (the claim comment, the repro report's environment
     record, the artifacts read against the issue's description, the
     repo-facts block) or a location from your
     references/evidence-guide.md. "The report" is not a source; "the
     output excerpt read against the error the issue describes" is.
   - Pass condition: a decision rule about the OUTCOME that someone
     else could apply and get your answer. Judge the thing itself (does
     the artifact show the issue's behavior?), never the write-up's
     shape (how many steps it has, how long it is, whether it uses a
     template's headings). Structure-shaped checks are what make
     graders disagree with themselves.
   - Weight: `required` (a fail here holds the package) or `preferred`
     (never changes the verdict).

2. A verdict rule below the table: how the check grades combine into
   accept (ready) or reject (hold), including how `unclear` is
   treated. The verdict space is binary. If you write no rule for
   `unclear`, the skill treats it as fail.

Cover what actually gets bad packages posted. The lecture named the
proof families: the environment is recorded, the steps are complete
and followable, the behavior shown matches the issue (not an adjacent
one), the outcome is stated honestly (an evidenced cannot-reproduce is
a pass, a confident wrong-target is not), and the words respect the
repo's conventions. A rubric that ignores a family will fail eval
packages designed around that family.
-->

## Checks

| Check | Evidence | Pass condition | Weight |
|---|---|---|---|
| env-recorded | The repro report's environment section (see evidence-guide.md § Environment) | The report names a specific OS (or platform), the tool or library version under test, and any build or driver variant the issue targets. An environment that just says "Windows" with no version or driver on a driver-specific issue fails. | required |

| steps-followable | The repro report's steps-to-reproduce section (see evidence-guide.md § Steps) | A stranger starting from a fresh clone or install could execute the steps as written and arrive at the trigger point. Steps that depend on private repos, unshared configs, or omit the command that actually fires the bug fail. | required |

| behavior-matches | The output excerpts or terminal logs in the repro report, read against the issue's described symptom (see evidence-guide.md § Behavior shown) | The artifact (log, console output, test failure, screenshot) shows the same failure mode the issue describes : same exit code, same error type, same observable deviation. An artifact that shows a graceful validation error when the issue reports a crash, or a completely different error, fails even if the prose says "reproduced". An honest evidenced cannot-reproduce (real attempt, real artifacts showing a different or null result, with a stated reason) passes. | required |

| artifact-present | The repro report body : output excerpts, terminal captures, or test output (see evidence-guide.md § Behavior shown) | At least one raw artifact (verbatim log lines, console output, test output, or screenshot) is shown, not merely asserted in prose. "I confirmed this behavior" with no artifact fails. | required |

| comms-specific | The candidate claim comment (see evidence-guide.md § Comms) | The claim names the specific issue being worked, states what the contributor will do next (investigate, reproduce, report findings), and avoids promising a fix timeline or a guaranteed delivery date. A comment that says "I will fix this in 2 days" or only says "+1 / me too / please assign me" fails. | required |

| conventions-followed | The repo-facts block (contribution policy and AI policy) read against both the claim comment and the repro report | If the repo's stated policy requires AI-use disclosure (any language requiring contributors to state that AI assisted their work), then at least one of the posted comments must contain an explicit disclosure. If the policy is permissive or silent on AI, this check passes regardless of whether disclosure appears. | required |

## Verdict rule

Accept if every required check passes. A grade of `unclear` on any required check counts as fail. Preferred checks never change the verdict.
