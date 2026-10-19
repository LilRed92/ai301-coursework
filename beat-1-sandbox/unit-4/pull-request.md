# Unit 4 — Test and Submit

Path: `beat-1-sandbox/unit-4/pull-request.md`

Record of the pull request you opened against the Path Review repo, and of the evaluation
runs that produced `eval-run.txt`. This file is graded at the path above; a copy kept
anywhere else in the repository is not read.

Complete every labelled field below. Each is graded on its own; content placed under the wrong
label is not graded.

---

## Your pull request

**Pull request**

PENDING: the pull request has not been opened yet. The link will be added once it is open on codepath/pathreview-ai301-fa26-s1.

**Branch**

fix/56-structural-chunker-no-headings

## Eval iterations

Answer all four sections. Quote source text directly; paraphrase does not satisfy these
fields.

**Run history**

Run 1 (full run, harness): 20/20, PASS, every category matched (clear-accept 7/7, not-tested 4/4, silent-drift 4/4, standards-wall 2/2, unreviewable 3/3). This is the only scored run, and it matches the agreement line in the committed `eval-run.txt`.

Two things happened before it that were not scored runs. A dry run outside the harness, with four Sonnet subagents grading the 20 packages in eval mode, also agreed on 20/20. One earlier harness attempt graded nothing: every call exited with an authentication error (OAuth token revoked), so no packages were graded and no score exists for it.

**Package analysis**

pkg-20 (ghostty-org/ghostty#13604, standards-wall). My rubric decided reject and the gold label is reject.

The fix is bounded, matches the plan, and has decisive before and after output (`ESC[?997;2n` before, `ESC[?997;1n` after). What holds it is the "ai disclosure" check. The repo facts say the policy requires all AI use to be disclosed, naming the tool and the extent, and the description has no AI statement. The check reads the policy line first and only requires a statement when the policy requires disclosure, so a package like pkg-02 (no stated AI policy) is not held for it. Here the policy does require it, so the check fails, and because it is required, the verdict is reject. Excellent code and evidence do not rescue it, which is the point of the standards-wall category.

**Check rationale**

| ai disclosure | the "contribution policy" line in "repo facts", read against the "description". | pass if the policy does not require disclosing ai use in contributions generally (no ai policy, assistive use allowed, or a rule only about writing comments in your own words), or if the description contains an explicit statement that ai was used that names the tool or extent. fail if the policy says all ai use must be disclosed and the description has no such statement. | required |

It reads this way because the repo's own stated ask decides whether a statement is needed, not whether AI was used. I rejected a flat rule of always requiring a disclosure statement, because it would hold clear accepts such as pkg-02 and pkg-19 that have no AI policy to satisfy. I also rejected a rule that only looks for the word "AI", because pkg-11 shows a policy that is about comments being written by humans, not about disclosure. The pass condition names those exceptions so another grader gets the same answer. The row follows the shape of my Unit 3 check of the same name, with "description" in place of "plan comment".

**Trade-offs**

After the dry run, one row changed: "repo checks shown" now says a formatter or linter named with its outcome, or stated as a ticked checklist item, counts as shown. That was added because pkg-08 had only a ticked "code formatted" item and a strict grader could have rejected a clear accept. The cost is that a package which only ticks "formatted" without running anything would pass that check. I accept that, because the other required checks still decide the verdict.

The full run came after that change and agreed on all 20, so no `--only` re-grade or canary run was needed. The checks overlap on purpose: churn and dead code fail both "no unplanned changes" and "clean diff". That is harmless for the verdict because either one rejects, but it means the note column cannot show which family a package belongs to. The case this rubric would still miss is a PR whose evidence is real output but for the wrong input, if the plan's test plan is vague about which input must be re-run.

---

Related paths: `eval-run.txt` in this directory; your skill's files in
`tools/pr-precheck/`.
