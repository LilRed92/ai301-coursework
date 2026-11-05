# Evidence guide: where evidence lives in a pr package

## Plan fidelity (harness category: silent-drift)

Where it lives: in an eval bundle, the "plan context" section (the plan's files line, scope and out-of-scope statements, list of deliverables, and any deviation note), read against the candidate pr's "diff" (the files and hunks it changes) and its "description" (the claims it makes about the diff). Live mode: `plan.md` (including its "## Deviations" heading), the output of `git diff main...HEAD` from the top folder of the fork's clone, and `pr_draft.md`.

What good looks like: every changed file and hunk is work the plan names or its scope needs, and every deliverable the plan lists is in the diff, or is named as deferred in the plan and restated in the description. Silent drift runs two ways. More than the plan: a rewritten function, a new option, flag or setting, or an extra file the plan never named, under a description that says "exactly as planned". Less than the plan: a promised test or docs update missing from the diff while the description says it was done. A disclosed deviation re-ties a mismatch only if the fix needs it; a disclosed cleanup is still an unplanned change.

## Test evidence (harness category: not-tested)

Where it lives: the candidate pr's "test evidence" section, read against the plan's test plan and the repro evidence in "plan context", and the checks that "repo facts" says the repo asks for. Live mode: `test_evidence.md` (the before and after of the unit 2 repro steps, plus the output of `make test-unit`, `make test-integration`, `make lint` and `make typecheck`), and the Testing section of `pr_draft.md`.

What good looks like: the plan's repro command is re-run on the broken path, with printed output, an exit code or a value shown before and after, so the two differ the way the plan expected. Each check the plan or repo names appears with its command and its outcome. A failing check reported honestly with the reason counts as evidence; a hidden one does not. Weak evidence is "tested locally", "works now", "tests pass" with no command, or a run of only a control or an unchanged path (for example a different input than the issue's, or one of two failing steps the plan named).

## Diff quality (harness category: unreviewable)

Where it lives: the candidate pr's "diff" (added and removed lines in every hunk) and its "commits" list. Live mode: `git diff main...HEAD` (and `git diff main...HEAD --stat` for the file list), and `git log main..HEAD --oneline`.

What good looks like: the fix, its tests and its changelog or docs entry, and nothing else, so a reviewer sees the change at a glance. The debris tells are: a debug print or log line left in, a commented-out line or block (a first attempt, an experiment), a dead or unused function, import or variable, a leftover todo, whitespace or formatting-only hunks, and a re-indented block with no logic change. An explanatory comment is not debris. Commit messages such as "wip", "misc" or "fmt" are a hint to look harder at the diff, but the diff decides.

## Standards and comms (harness category: standards-wall)

Where it lives: the "repo facts" section's "pull requests" line (template sections, issue link, checklist items, changelog or release-notes entry, tests) and "contribution policy" line (including any ai-use rule), read against the candidate pr's "description" and "diff"; the "thread highlights" section for maintainer direction. Live mode: `.github/PULL_REQUEST_TEMPLATE.md` and `docs/CONTRIBUTING.md` in the fork's clone, the issue thread on GitHub, `pr_draft.md`, and `scope.md` (the course's house rule that the template is always used, with the ai-use disclosure under "Notes for Reviewers").

What good looks like: every section of the template filled with real content, "Closes #" followed by the issue number, checklist boxes ticked only when true (the CI box left unticked until the pr is open), the changelog or release-notes entry in the diff when asked, and an ai-use statement in the description's own words where the policy requires it (in live mode the course always requires it). Non-compliance is a stated ask that is visibly skipped, boilerplate left in a section, or no disclosure under a policy that requires one. Whether the description's claims match the diff is plan fidelity, above.
