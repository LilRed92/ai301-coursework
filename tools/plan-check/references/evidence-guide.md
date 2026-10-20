# Evidence guide: where evidence lives in a plan package

## Diagnosis and grounding

Where it lives: in an eval bundle, the plan's diagnosis or cause text (inside the "candidate plan" section), and the "repro evidence" section: the numbered steps, any artifact output, the control or control runs lines, and the expected and actual lines. Live mode: the plan.md diagnosis, read against the repro comment the student posted on their issue.

What good looks like: the stated cause explains the actual line and is consistent with every control. A cause is ungrounded when a control with the suspected component removed or bypassed still shows the bug, when an artifact shows the bad value already exists before the suspected step runs, or when the plan only repeats what the issue or thread said.

## Scope

Where it lives: the plan's scope statement (scope, in scope, not in scope), its changes or approach list, and its files line. Live mode: the same parts of plan.md.

What good looks like: one change that fixes the reproduced symptom, plus tests for it, with other work named as out of scope. Scope creep looks like extra work items the symptom does not need: a refactor, a migration, a new option or settings panel, a new framework, or other platforms.

## Executability

Where it lives: the plan's file, function and module names, and its numbered changes or approach steps. Live mode: the files you will touch and approach parts of plan.md.

What good looks like: a stranger could start without asking the author, because the plan names where to edit and which approach it picked. Vague plans say "somewhere", "whichever is easier", "investigate" or "maybe also", or leave the main decision to build time.

## Test plan

Where it lives: the plan's test plan text, read against the numbered steps in the "repro evidence" section. Live mode: the test plan part of plan.md, read against the posted repro comment.

What good looks like: the test reuses specific repro steps or a named command, and states a result that would differ between the buggy and fixed builds (an exit code, an output line, a visible color or value). A vague test says "run the test suite", "should feel fast" or "nothing else should break".

## Honesty

Where it lives: the plan's risk, risks or unknowns text, and how certain the diagnosis sounds. Live mode: the risks and unknowns part of plan.md, and the "## Deviations" heading for build changes.

What good looks like: things the repro did not show are labeled as unknowns or risks. False confidence presents a guess as a finding.

## Comms

Where it lives: the "candidate plan comment" section, read against two other places. First, the "thread highlights" section (author roles are in brackets, such as "OWNER", "COLLABORATOR" or "NONE"). Second, the "repo facts" section, especially the contribution policy line and its ai rules. Live mode: the draft comment.md, the live issue thread (via gh or the web), and the repo's contributing and ai policy files.

What good looks like: the comment names any direction from an "OWNER", "COLLABORATOR" or "MEMBER" (a culprit, a preferred option, a testing request) and says whether the plan follows it. Where the policy says all ai use must be disclosed, the comment states that ai was used. Policies that only ask for human-written comments, only ask for disclosure in pull requests, or say nothing about ai do not require a statement. Boilerplate that could sit on any issue is not engagement.
