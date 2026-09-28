# Rubric: is this a good first issue?

<!--
THIS IS THE PART YOU WRITE. The skill in SKILL.md executes whatever checks
you define here. It ships empty on purpose: the judgment is your work.

A filled rubric must contain:

1. At least one row in the checks table. Each row needs all four columns:
   - Check: a short name (used in the output JSON).
   - Evidence: exactly what to look at, and where. Name the source
     (repo-facts block, issue body, comment thread, or the locations in
     references/evidence-guide.md). "The repo" is not a source; "the last
     5 default-branch commit dates" is.
   - Pass condition: a condition someone else could apply and get your
     answer. Prefer thresholds with numbers ("a maintainer commented
     within 30 days") over adjectives ("maintainer is responsive").
   - Weight: `required` (a fail here rejects the issue) or `preferred`
     (never changes the verdict; a nice-to-have that helps rank the
     issues you accept).

2. A verdict rule below the table: how the check grades combine into
   accept or reject, including how `unclear` is treated. The verdict
   space is binary. If you write no rule for `unclear`, the skill treats
   it as fail.

Cover what actually kills first contributions. The lecture named four
families: the maintainer is alive, the repo is in use, the scope fits a
newcomer, and nobody else is already on it. A rubric that ignores a family
will fail eval issues designed around that family.
-->

## Checks

| Check                     | Evidence                                                                | Pass condition                                                                                                                                                                                                                                                                                                                                                                                                                                    | Weight   |
| ------------------------- | ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- |
| `maintainer-active`       | Repo-facts block and comment thread                                     | The maintainer has commented, committed, or merged a pull request within the last 30 days.                                                                                                                                                                                                                                                                                                                                                        | required |
| `issue-unclaimed`         | Repo-facts block and comment thread                                     | The repo-facts show no assignee, and no user in the comments has stated they are working on it or linked an open pull request, unless over 90 days old with no follow-up.                                                                                                                                                                                                                                                                         | required |
| `repo-in-use`             | Repo-facts block                                                        | The repository has had new commits, merged pull requests, or active releases within the last 60 days.                                                                                                                                                                                                                                                                                                                                             | required |
| `scope-small-impact`      | Issue body and comments                                                 | The issue describes a single bounded objective: a specific bug fix, localized feature, or cohesive documentation update. Listing implementation steps, related pages/files, variants of a single UI preview, or multiple diagnosed causes of a single bug does not make it an umbrella issue. Must not be an open-ended tracking/umbrella issue coordinating separate sub-tasks across the codebase, must not be a vague one-line wish lacking specification, must have no history of multiple abandoned/closed unmerged PR attempts, and any open design debate must be settled with clear maintainer consensus. | required |
| `ai-contribution-allowed` | CONTRIBUTING.md / AI policy files / repo-facts contribution-policy line | The repo states no outright ban on AI-generated contributions (disclosure or review requirements are fine, a stated ban is not)                                                                                                                                                                                                                                                                                                                   | required |

## Verdict rule

Accept the issue only if every required check passes. Count an `unclear` or `?` on a required check as a fail. Preferred checks never change the final verdict, they rank accepted issues.
