# Procedure: how this skill grades a plan package

## Read order

1. Read the "repo facts" section first. Note the contribution-policy line, in particular whether it requires disclosing ai use.
2. Read the "issue" section and the "thread highlights" section. Note every comment whose author role is "OWNER", "COLLABORATOR" or "MEMBER" that states a culprit, a preferred approach or a request. Ignore opinions from "NONE" or "CONTRIBUTOR" authors for this purpose.
3. Read the "repro evidence" section before the plan. Note what each numbered step shows, what each artifact shows, and what each control run rules in or out. Note the actual line. Reading it first keeps the plan's claims from shaping how the evidence is read.
4. Read the "candidate plan" section. Note its stated cause, its scope and out-of-scope statements, its list of changes or files, its test plan, and any stated risks.
5. Read the "candidate plan comment" section last. Note which maintainer direction it names, and whether it includes an ai-use statement.

## Evidence gathering

1. Cause: copy the plan's stated cause in one sentence. Then list each repro step, artifact and control run in one line each, with what it shows. Do not look for support yet; just list.
2. Scope: list every separate piece of work the plan commits to (each change, each file group, each new option or migration). Note which ones the plan marks as out of scope.
3. Executable: copy the file, function or module names the plan will change, and the one approach it picked. Note any place the plan gives alternatives, says "maybe", says "somewhere", or defers a decision.
4. Test: copy the test plan's commands or steps and the result it says to expect. Note which repro step each one reuses.
5. Maintainer direction: copy the direction notes from read order step 2, and copy the sentences of the plan comment and plan that mention the thread.
6. Ai disclosure: copy the policy's ai sentence, and copy any sentence in the plan comment that mentions ai use.
7. Unknowns: copy the plan's risks and unknowns text, if any.

## Check execution

1. Grade the checks in the order of the rubric table: cause fits repro, bounded scope, executable, decisive test, maintainer direction, ai disclosure, honest unknowns.
2. Grade each check using only the gathered notes for that check and the rubric's pass condition. Do not re-read the whole package for a check, except to confirm one quote.
3. For cause fits repro, test the stated cause against each listed control run and artifact one at a time. If a single control or artifact contradicts the cause, grade fail and name it. Do not accept the cause because the issue or the thread says so.
4. For bounded scope, count the work items from evidence gathering step 2. Grade fail if any item is not needed to fix the reproduced symptom or its tests and is not marked out of scope.
5. For maintainer direction, if read order step 2 found no such comment, grade pass and write "no maintainer direction in the thread". Otherwise grade pass only if the plan comment names that direction.
6. For ai disclosure, decide first whether the policy requires disclosure for comments or contributions generally. If it does not, grade pass and write "no general disclosure requirement". If it does, grade pass only if the plan comment states ai use.
7. If the evidence for a check is missing from the package (for example there is no test plan at all), grade it unclear. Do not guess.
8. Write one evidence line per check: the fact or quote that decided it.

## Verdict assembly

1. Count the required checks (all except honest unknowns). Treat any unclear grade on a required check as fail.
2. If every required check passes, the verdict is accept. If any required check fails, the verdict is reject. The honest unknowns grade never changes the verdict.
3. Before the json block, write one line per check with its grade. For a reject, quote the evidence line of each failed required check.
4. Emit the json block with one entry per check (grade pass, fail or unclear) and the verdict, as skill.md specifies. Put nothing after it.
5. If any step above could not be followed because the procedure was silent, say so in one line before the json block.
