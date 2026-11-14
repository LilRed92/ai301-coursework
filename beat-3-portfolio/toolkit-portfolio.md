# Toolkit Portfolio

Path: `beat-3-portfolio/toolkit-portfolio.md`

**Student:** Kacie Dearman

## Featured Tools

I chose these four because together they tell the whole arc of my term: the scout found me a real issue, the voice guard kept me honest on the thread, the ship-gate caught every local check before I opened the PR, and the pr-monitor is what I use now that the PR is open. Each one changed in response to something that actually went wrong.

**issue-scout**

**What it is, and the judgment hole I wrote:** The scout runs a set of `gh search issues` queries against GitHub and grades each result against my rubric. The judgment is entirely in the rubric and search strategy: which checks are required, what counts as a pass, and how the difficulty note is worded. I wrote both files myself.

**How it evolved, dated:**

- **2026-10-29 (first scan):** The rubric's `scope-small-impact` check was too loose. terminal-agent issues with six sub-tasks passed because the check said listed steps didn't make an umbrella. Three of the five results came from a two-month-old org with two to four stars. I added a file-count limit and three preferred checks (`outside-prs-answered`, `setup-doable`, `repo-established`) after the scan.
- **2026-11-05 (second scan):** `scope-small-impact` still let taskchampion#613 through, and Carefold filled three of six slots. I added a one-issue-per-repo cap and a per-query slot to the strategy, dropped umbrella-signaling labels and titles, changed the JavaScript query to `react` with `help wanted` (I am proficient there, not a beginner), required `rust` in the body or title for Rust results, and added a `Web3` query searching `blockchain`.
- **2026-11-06 (direct grading):** The `issue-unclaimed` check rejected taskchampion#613 because it read my own claim comment as a stranger's. I added my login (LilRed92) to the rubric and told the check to ignore claims, assignments, and linked PRs from that login, and to name each login it did or didn't ignore. A rerun accepted #613 with a difficulty note of ambitious.
- **2026-11-07 (rubric patch, not rescanned):** Replaced `scope-small-impact` with `scope-feasible`, which rejects only issues that are not one piece of work. Added the difficulty note (straightforward, moderate, ambitious) so scope flags go into the notes rather than the verdict, letting me claim an ambitious issue knowing what to ask the maintainer early.

**Evidence:**

Before the 2026-11-05 scope patch, the rubric accepted terminal-agent#4 (streaming across 4 providers, agent loop, and UI) because "listed steps and related files do not make an umbrella." After the patch, the check reads:

> The issue describes one identifiable piece of work someone could start: a behavior, a gap, or a task you can point at. It fails only when there is no single piece of work in it: a codebase-wide checklist, an "improve X everywhere", or a container issue tracking many sub-tasks.

Before the 2026-11-07 `issue-unclaimed` fix, the check's evidence field read nothing about the scout's own login. After the fix it reads:

> The repo-facts show no assignee other than LilRed92 (the scout's user, also named under "Who is running the scout" in scope.md), and no user other than LilRed92 in the comments has stated they are working on it or linked an open pull request [...] Ignore every comment, assignment and linked pull request from LilRed92: it is the scout's user's own claim, not a stranger's. The evidence for this check must name each login it ignored and each login that remains.

---

**voice-guard**

**What it is, and the judgment hole I wrote:** The voice guard hooks into `gh` commands and checks outgoing text against a voice guide I wrote. The judgment is the voice guide: the rules, the wrong/right examples, and the "things I never post" list. I wrote every rule and example myself, drawing on the upstream rules and my own gaps.

**How it evolved, dated:**

- **2026-11-07 (unit 6, first use):** Installed the hook and merged four upstream rules into my guide. The hook blocked `gh issue comment --help` on purpose. When I ran it manually on my claim draft, it stopped at 14:29 for "tested locally with no command and no output," which was exactly the rule I had written. I rewrote the draft and it passed at 14:38.
- **2026-11-11 (plan comment):** I ran the guard on my plan comment for taskchampion#613. It stopped at 03:40 for the "engage the maintainer's direction first" rule — my draft proposed a path without first saying I was following djmitche's stated approach. I added a sentence that named his direction and said I was following it. It passed at 03:40 (same minute, different run).
- **2026-11-11 (AI disclosure):** An earlier draft of the claim failed at 00:13 for the AI disclosure rule. I rewrote it to name what I used AI for and state that I was present and actively involved. It passed at 00:30, then failed again at 00:35 for a stricter version of the same rule. I revised once more and it passed at 00:38.
- **2026-11-13 (PR comment):** The hook stopped a `gh pr comment` at 16:25 for "testing shows the command and what it printed." I revised to add the actual command and output before reposting. It passed at 16:30.

**Evidence:**

Guard log excerpt (from `~/.claude/voice-guard/guard-log.md`), showing the stop and pass on the claim draft:

```
2026-11-07 14:29 [manual] stop: rule broken: "Tested locally" or "tests pass" with no command and no output | target: claim-draft.md
2026-11-07 14:38 [manual] pass | target: claim-draft.md
```

Guard log excerpt showing the hook stopping a live `gh pr comment` on 2026-11-13:

```
2026-11-13 16:25 [hook] stop: rule broken: "Testing shows the command and what it printed, before and after. I tick only the boxes that are true, and I report a failing check with its reason." | target: gh pr comment https://github.com/GothenburgBitFactory/taskchampion/pull/796 --body-file
2026-11-13 16:30 [hook] pass | target: gh pr comment https://github.com/GothenburgBitFactory/taskchampion/pull/796 --body-file
```

---

**ship-gate**

**What it is, and the judgment hole I wrote:** The ship-gate checks a PR before it goes up. It runs every check in the ship manifest I wrote, then grades the PR title and body against the pr-precheck skill. My judgment is the manifest (which checks are required and what commands run them) and the ship-gate scope (what constitutes a clean diff and honest claims). I also wrote the CLAUDE.local.md that teaches the gate about the repo.

**How it evolved, dated:**

- **2026-11-10 to 2026-11-11 (hook installs, four BLOCKs):** The hook ran and blocked `gh pr create --help` four times with "no PR text to check." Each was a setup-only run. The gate is working as designed: it requires both `--title` and `--body-file` to even start.
- **2026-11-13 (first real run):** Manual run on the full title and `pr_draft.md`. All five manifest checks passed: `cargo test` (442 passed, 133 seconds), `cargo fmt --check`, clippy with `-D warnings`, `cargo +nightly rustdoc`, and `cargo semver-checks` (229 pass, 31 skip, no semver update required). All eight pr-precheck checks passed. Verdict: PASS.
- **2026-11-13 (hook honored the manual pass):** The hook picked up the same fingerprints and passed without re-running the manifest checks.

**Evidence:**

From `~/.claude/ship-gate/gate-log.md`, the passing run on 2026-11-13:

```
verdict: PASS
fingerprints: head 2f9a1d550fe122961ee7daa97849df92175d84ce base d6dc3cfe8cab21bea4e7ccee374cdb20598b207d
manifest checks:
  Tests: cargo test -> ok (133s)
  Formatting: cargo fmt --check -> ok (1s)
  Clippy: cargo clippy --all-features --no-deps -- -D warnings -> ok (1s)
  Docs (rustdoc, CI form): cargo +nightly rustdoc ... -> ok (12s)
  Semver: cargo semver-checks ... -> ok (58s)
```

The semver check had failed on a prior commit (commit `d3e56482a`, before wrappers) with `inherent_method_missing` on 7 methods. The gate forced me to add the thin wrappers before I could ship.

---

**pr-monitor**

**What it is, and the judgment hole I wrote:** The pr-monitor watches an open PR and decides what to do next based on a playbook I wrote. The judgment is the playbook: the staleness thresholds, the nudge rules, and the walk-away criteria, all grounded in that specific repo's history.

**How it evolved, dated:**

- **2026-11-13 (first state check, 15:20):** The monitor read PR 796 and returned `branch-stale: 1 failing, 20 passing`. PR was 35 minutes old. I ran two more state checks and confirmed the state fingerprint.
- **2026-11-13 (first full run, 15:42):** The monitor read the failing check, looked at the PR thread (0 comments), and drafted a rebase plan rather than a reply, because there was nothing to reply to yet. The playbook thresholds are 5 quiet days before nudging on a PR with no reply at all, and 7 quiet days after I have already answered a review. Neither threshold was anywhere close.
- **Playbook calibration:** I based the thresholds on five recent outside-contributor PRs on the repo (#795, #779, #762, #757, #722). djmitche replied within about 1 to 27 hours on each. Merging took 1 to 14 days. I set the first nudge at 5 days because even the slowest first reply came within 2 days.

**Evidence:**

From `~/.claude/pr-monitor/playbook.md`, my staleness thresholds and nudge rules:

```
Staleness thresholds:
- A PR with no reply at all: I wait 5 quiet days before I would nudge.
- A PR where I already answered a review: I wait 7 quiet days.

Nudge etiquette:
- I send at most one nudge, and only after the threshold above has passed.
- It names what the PR does in one sentence, mentions anything new since I opened it,
  and asks for one thing: a review.
- It tags only djmitche.
- I do not send a second nudge.
```

From the monitor log, the first full run:

```
2026-11-13 15:42 [run]
state: branch-stale: the branch needs work: failing checks (1 failing, 20 passing)
move: Rebase/fix plan for PR #796, with nothing to post yet (via the rebase plan form)
```

---

## Inventory

- **repro-check:** Grades claim drafts and reproduction reports. I added a voice guide and merged the upstream rules into it. I used it to pass my claim on taskchampion#613 (all six required checks passed) and to fix a scope error in my claim draft before I posted.
- **plan-check:** Grades a plan file and plan comment draft against an open issue. I used it on `plan.md` and `plan-comment.md` for #613. It accepted both with four things to fix first (semver wording, the rustdoc command, the setters credit, and a commit-link placeholder). I fixed all four before posting.
- **pr-precheck:** Runs eight checks on the diff and PR draft: unplanned changes, claims matching the diff, before/after evidence, repo checks shown, clean diff, template asks met, AI disclosure, and maintainer direction engaged. All eight passed on the ship-gate run before the PR opened. Its voice guide shares rules with the voice guard.

---

## The Arc

**Beat 1**
Date: 2026-10-29
Friction: My first issue-scout scan returned three results from the same two-month-old org and let through issues spanning six sub-tasks and multiple modules because my `scope-small-impact` check only counted whether the issue had listed steps, not how many files it touched or whether it was an umbrella.
Change: Added a file-count limit to `scope-small-impact`, added three preferred checks (`outside-prs-answered`, `setup-doable`, `repo-established`), fixed the zsh quote around separator strings, and added notes on what drove each change to scan-notes.md.
Result: The second scan on 2026-11-05 stopped the two-month-old org from filling the top results, and the new preferred checks produced a cleaner ranking.

**Beat 2**
Date: 2026-11-05
Friction: The second scan still let Carefold fill three of six slots, and the JavaScript and Tailwind queries returned nothing useful. The `scope-small-impact` check still accepted taskchampion#613 on a 2-file count even though it moves methods on a core public type with an unsettled design.
Change: Added a one-issue-per-repo cap and a one-slot-per-query rule to the strategy, changed the JavaScript query to `react` with `help wanted`, required `rust` in the body or title for Rust results, added a `blockchain` Web3 query, and added a `dashboard` title drop and a bot-author filter to block Renovate dashboards.
Result: On the rerun, the JavaScript fix worked and splitApp#15 reached the top six. The Tailwind and Web3 queries still returned mostly umbrella issues and produced no accepted candidates, but the main slots no longer went to repeat repos or bots.

**Beat 3**
Date: 2026-11-06 to 2026-11-07
Friction: Direct grading on taskchampion#613 failed `issue-unclaimed` because the check read my own claim comment and my assignment as a stranger's claim. A scope patch had already been planned but not yet written.
Change: Added my login (LilRed92) to the rubric row for `issue-unclaimed` and told it to name each login it ignored. Replaced `scope-small-impact` with `scope-feasible` and added the difficulty note system (straightforward, moderate, ambitious) so scope flags inform the choice without blocking it.
Result: A rerun accepted #613 with a difficulty note of ambitious, and the evidence line named LilRed92 as ignored and djmitche as the remaining login. I claimed the issue knowing the design edge to raise with the maintainer early, which I did on 2026-11-08.

**Beat 4**
Date: 2026-11-07 to 2026-11-11
Friction: My claim draft failed the voice guard three times across two days: once for "tested locally with no command and no output," once for the AI disclosure rule, and once again for a stricter restatement of the same rule. My plan comment for #613 also failed once for not naming the maintainer's direction before proposing anything.
Change: Rewrote the claim draft each time to name the specific command and output, then to name the AI tool and what I used it for and state that I was present in any code I touched. Rewrote the plan comment opening to say "Following djmitche's direction on the issue" before the plan.
Result: Every revised draft passed the guard. The claim went up on the thread. The guard stopped a live `gh pr comment` on 2026-11-13 for the same evidence rule, and that stop fixed another shortcut before it reached the maintainer.

**Beat 5**
Date: 2026-11-12 to 2026-11-13
Friction: `cargo semver-checks` failed on commit `d3e56482a` (Deref added, 8 Task getters deleted, no wrappers) with `inherent_method_missing` on 7 methods. The plan had covered this case but I still had to actually see the failure before I added the wrappers.
Change: Added thin Task wrappers for all 8 getters (the 7 flagged plus `get_scheduled` for consistency). Re-ran all five manifest checks. The ship-gate manual run on 2026-11-13 passed all eight pr-precheck checks and all five manifest checks.
Result: PR 796 opened on 2026-11-13. The gate log fingerprints confirm the head commit, the passing verdict, and each check's time. The PR is open and waiting for review.

---

## Limitations and What's Next

The scout's preferred checks are still unstable. `outside-prs-answered` and `newcomer-friendly` have flipped on the same repo facts between sessions without any rubric change, because the grader names different PRs or lines each time. I cannot treat a single preferred-check grade as a stable fact, only the required checks. A fix would force each check to name the specific lines or PRs it counted so the evidence is checkable across runs.

The voice guard only catches what I think to put in the voice guide. It stopped four real mistakes this term, but each one was a rule I had already written. It would not have caught a mistake I had not anticipated. The guard log has no record of a check it was not asked to run.

The pr-monitor is new and has only one entry in the log. I do not yet know whether the playbook thresholds are right, because the PR has been open less than a day and djmitche has not replied yet. I will not know until it gets its first review.

My next step for the scout is to add a check that asks whether the issue changes a core public type, so an issue like #613 carries a mandatory flag instead of only a difficulty note. For the voice guard, I would add a rule about not claiming tests cover something that the diff does not contain, because that is the most common slip I see in my own drafts. For the pr-monitor, I will update the playbook after the first review lands, using the actual timing to check whether my 5-day threshold fits this repo.

**Tool limits.**

issue-scout: Preferred checks are unstable across sessions; the same repo facts can flip a preferred check between runs. The rubric grades one issue at a time and cannot compare two candidates directly.

voice-guard: Only enforces rules I wrote in advance. A mistake I did not anticipate goes unchecked. The hook also stops `--help` and interactive forms, so testing the hook itself requires real draft text.

ship-gate: Runs all five manifest checks locally but cannot run the CI environment exactly. A check that passes locally may still fail in CI if the environment differs (for example, nightly toolchain version).

pr-monitor: Playbook thresholds are based on five historical PRs, not on the current maintainer's reply to my specific PR. They are estimates, not guarantees.
