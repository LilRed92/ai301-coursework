# Procedure: how this skill grades a pr package

## Read order

1. Read the "repo facts" section first. Note the "pull requests" line (every ask the repo states: template sections, issue link, checklist items, changelog entry, tests, the checks to run) and the "contribution policy" line, in particular whether it requires disclosing ai use.
2. Read the "issue" and "thread highlights" sections. Note every comment from an "OWNER", "COLLABORATOR" or "MEMBER" that states a culprit, a preferred approach or a request. Ignore "NONE" and "CONTRIBUTOR" opinions for this purpose.
3. Read "plan context" before the pr. Note the plan's files line, its scope and out-of-scope statements, every deliverable it lists (code change, tests, docs, changelog), its test plan (each command or repro step and the result it expects), and any deviation note. Reading the plan first keeps the pr's description from shaping what the plan is taken to say.
4. Read the candidate pr's "diff" next, before its description. List the files and hunks it changes. Reading the diff before the description means the description's claims get tested against the diff rather than the other way round.
5. Read the "commits" list, then the "description", then the "test evidence" last. Note each claim the description makes, and each command and output the test evidence shows.

## Evidence gathering

1. Unplanned changes: list every file in the diff and, for each, one line on what its hunks do. Beside each, write whether the plan's files line, scope statement or deviation note names it. For a file the plan does name, check each hunk for work the scope does not need (a rewritten function the plan never mentions, a new option, flag or setting).
2. Claims: copy each claim in the description about what the pr does, adds, covers or leaves out. Beside each, write the diff line that shows it, or "not in the diff". Copy each deliverable the plan lists and mark it in the diff, or deferred in a note that the description restates, or missing.
3. Decisive test: copy the plan's test plan steps and the repro's own command. Find the matching command in the test evidence and copy the before and after output (or note that only a statement is given). Note whether the command exercises the broken path or only a control.
4. Repo checks: list every check the plan's test plan names and every check "repo facts" says the repo asks for. For each, copy the command and the outcome shown in the test evidence, or write "not shown".
5. Clean diff: scan every added and removed line for debug output, commented-out code, dead or unused functions, imports or variables, leftover todos, whitespace or formatting-only hunks, and re-indented blocks with no logic change. List each one with its file. Skip explanatory comments.
6. Template asks: copy each ask from the "pull requests" line. Beside each, write where the description or diff meets it (the section, the issue link, the changelog file in the diff, the test file in the diff), or "skipped".
7. Ai disclosure: decide whether the policy requires disclosure for contributions generally. Copy the policy's ai sentence, and copy any sentence in the description that mentions ai use.
8. Maintainer direction: copy the direction notes from read order step 2, and any sentence of the description that engages them.

## Check execution

1. Grade the checks in the order of the rubric table: no unplanned changes, claims match the diff, decisive before and after, repo checks shown, clean diff, template asks met, ai disclosure, maintainer direction engaged.
2. Grade each check using only the gathered notes for that check and the rubric's pass condition. Do not re-read the whole package for a check, except to confirm one quote.
3. For no unplanned changes, grade fail if any file or hunk in the notes is neither named by the plan nor needed by its scope and not covered by a deviation note, and name the file. Grade fail even when the description admits the extra change, if the change is not needed to fix the issue. Do not let a polished description or a full checklist outweigh a hunk the plan never asked for.
4. For claims match the diff, grade fail if any claim is marked "not in the diff", or if a planned deliverable is marked missing. Grade pass when a missing deliverable is named as deferred in the plan's deviation note and restated in the description.
5. For decisive before and after, grade pass only if the notes show printed output, an exit code or a value from the broken path, before and after. A comment after a command that quotes the actual output counts as output. A sentence saying the result changed, or a run of a control only, does not.
6. For repo checks shown, grade pass only if every listed check has a command and an outcome. A statement such as "tests pass" with the command named and a count or status counts. "Tests pass" with no command does not.
7. For template asks met and ai disclosure, if "repo facts" states no asks or no ai requirement, grade pass and write "no stated ask" or "no general disclosure requirement". Otherwise grade pass only if every stated ask is met.
8. For maintainer direction engaged, if read order step 2 found no such comment, grade pass and write "no maintainer direction in the thread".
9. If the evidence for a check is missing from the package (for example there is no test evidence section at all), grade it unclear. Do not guess.
10. Write one evidence line per check: the fact or quote that decided it.

## Verdict assembly

1. Count the required checks (all except maintainer direction engaged). Treat any unclear grade on a required check as fail.
2. If every required check passes, the verdict is accept. If any required check fails, the verdict is reject. The maintainer direction grade never changes the verdict.
3. Before the json block, write one line per check with its grade. For a reject, quote the evidence line of each failed required check, in rubric order, and start with the first failed one as the deciding check.
4. Emit the json block with one entry per check (grade pass, fail or unclear) and the verdict, as SKILL.md specifies. Put nothing after it.
5. If any step above could not be followed because the procedure was silent, say so in one line before the json block.
