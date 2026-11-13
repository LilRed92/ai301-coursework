# Contribution: Make simple property getters/setters available in TaskData

Path: `beat-2-contribution/contribution-story.md`

This file is Assignment 5, and it is graded at the path above; a copy kept anywhere else in
the repository is not read. **Keep every section header below under its exact name** — the
format criteria grade exactly that. Your course repo link is the whole submission: no tool
files and no evidence uploads are part of Assignment 5.

**Contribution Number:** [1]
**Student:** Kacie Dearman
**GitHub Username:** LilRed92
**Issue:** https://github.com/GothenburgBitFactory/taskchampion/issues/613
**Pull Request:** https://github.com/GothenburgBitFactory/taskchampion/pull/796

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

<!--
Every story section below, from Why I Chose This Issue through Pull
Request, ends with a Toolkit block: which tool did that phase's work
and how you used it, what it produced, what difficulties or
shortcomings it presented, and what you changed or would change
because of them. Together the blocks are the thread the rubric's
Toolkit points read, and they are the raw material for your unit-9
portfolio, so keep them current as you work rather than
reconstructing them later.

A Toolkit block looks like this (copy it into each story section and
fill it there):

```text
**Toolkit**

- Tool: [which tool did this phase's work, and how you used it]
- What it produced: [described in a sentence or a short excerpt]
- Difficulties: [what fought you or fell short, or "none met"]
- What changed: [the patch, revision, or workaround, what you would
  update, or "nothing"]
```

This section also keeps one short dated entry per week of tool work,
starting below: what you built or changed that week, what broke, and
what you changed because of it. The blocks tell the story where it
happened; these entries are the toolkit's own timeline.

All four entries are graded. Keep every heading below, and fill each
one in the week it belongs to. -->

**Unit 5: Built a six-query search strategy, scanned GitHub with `issue-scout`, and tuned the scout and my fit profile from the results**

I built six `gh search issues` queries and a set of ranking filters from the fit profile I wrote before this unit, then updated that profile to state my skill levels (proficient in PERN/MERN, barely past beginner in Python, new to Rust, TypeScript, Tailwind and Web3, including beginner smart-contract work) and removed a sentence that contradicted my learning goals. The first scans let sprawling features and brand-new repos through, so I limited `scope-small-impact` to 3 files and added the preferred checks `outside-prs-answered`, `setup-doable`, `repo-established` and `newcomer-friendly`. In the strategy I capped results at one issue per repo, gave each query its own slot and raised the graded count to 6, dropped epic, tracking, umbrella, meta and roadmap issues, switched the JavaScript query to `react` with `help wanted` because I am proficient there, required `rust` in the Rust query's title or body, and added a Web3 query on `blockchain` after `web3` returned a legal glossary and a job post. The rerun still spent two of six slots on a Renovate dashboard and a parent issue, and the Tailwind and Web3 queries returned mostly large items, so I added a `dashboard` title drop and a bot-author filter, which I chose not to test with another practice scan.

**Unit 6: Installed a voice guard on my outgoing comments and wrote a local repo-memory file for taskchampion**

I installed the voice-guard hook, merged the four upstream rules into my voice guide (reworded so they fit any issue in any repo), and confirmed the hook fires: `gh issue comment --help` was blocked, which is the pass. My first check of the claim draft stopped on the rule against "tested locally" with no command or output, so I rewrote it to name the commit and the result (438 passed, 0 failed), after which it passed (guard log: stop at 2:29, pass at 2:38 on 2026-11-07). I also wrote a roughly 40-line `CLAUDE.local.md` for my taskchampion clone, with the CONTRIBUTING.md rules, the Task and TaskData files behind #613, the build and test commands, and "no AI policy stated". The repo ships no CLAUDE.md or AGENTS.md, so I dropped the import line, and I kept the file out of the PR with `.git/info/exclude`. The comment I already posted on #613 predates the guard and still used the old "ran the test suite" wording, which the guard would block, so I edited that claim comment. I have only run the guard manually on drafts so far, so I have not yet seen it stop a real post.

*Update (2026-11-13):* The guard has now stopped a real post. It blocked my first comment on PR 796 about the Formatting failure, because the draft said `cargo fmt --check` produced a diff and that the other checks passed without showing the command or its output. I added the command and the output, and the comment then went through.

**Unit 7: Wrote a gate manifest, passed the ship-gate on my real branch and opened PR 796**

I wrote a `ship-manifest.md` with the five checks taken from the upstream CI workflows, and the ship-gate ran them on my branch, then ran `pr-precheck` in live mode. It passed on the run I pasted, with all five checks ok and all eight `pr-precheck` checks passing. The earlier semver failure is what led to the thin `Task` wrappers, and I amended and force-pushed the wrapper commit before opening the PR. The gate could not catch the Formatting failure that showed up in upstream CI on `src/server/cloud/mod.rs`, because that file is not in my diff and my local `cargo fmt --check` passes.

**Unit 8: Wrote a playbook from five merged taskchampion PRs and ran the PR monitor on PR 796**

I wrote my playbook from five recent merged PRs by outside contributors (#795, #779, #762, #757 and #722): djmitche first replied within about 27 hours on every one, and merging took 1 to 14 days, so I set a nudge threshold of 5 quiet days with no reply and 7 after I have answered a review. The monitor read PR 796 on 2026-11-13, saw 1 failing check out of 21 and no comments, and drafted a rebase and fix plan with nothing to post, following my rule not to nudge before day 5. The monitor could not see which check failed and labeled the state BRANCH-STALE, so I read the log myself: it was Formatting on `src/server/cloud/mod.rs`, a file my PR does not touch, and after I updated to Rust 1.100.0 my local `cargo fmt --check` reported the same diff, so a new rustfmt release caused it. I did not follow the fix steps, because a fix commit would have put an unrelated file into my PR, and there's truly nothing to fix on my end.

*Update (2026-11-13):* After the monitor run, I added a rule to the Response rules section of my playbook: when a check fails, I read its log first, then post one short comment saying whether the failure was mine and what I checked or fixed.

---

## Why I Chose This Issue

I found taskchampion#613 on the AI301 Issue Selection site, not through my own scan. My scout's searches turned up mostly Python and agent-framework issues, so I picked two candidates from the site and graded them directly: llm4s#2243 (add missing runnable samples to the Example Gallery) and taskchampion#613. On 2026-11-06 the scout accepted both. After I patched the rubric's scope check on 2026-11-07, it accepted llm4s#2243 as straightforward and rejected #613, because it read my own claim comment and assignment as a stranger's claim. I fixed that check and re-graded, and the scout accepted #613 with a difficulty note of ambitious: it touches the core `Task` and `TaskData` types, the maintainer's `Deref` idea is tentative, and moving public methods can trip the Semver check. Two preferred checks failed along the way: `outside-prs-answered`, because every recent PR is from the maintainer or dependabot, and `newcomer-friendly` on the first run, because Rust is new to me and the fix involves a trait impl.

I chose #613 anyway for three reasons. First, I like what the project does. TaskChampion implements the task storage and synchronization behind Taskwarrior, and any other application can also use it to maintain its own replica of a task list, so it is not tied to Taskwarrior. I am always looking for better task-management systems for myself, so I would be improving something I might use. Second, it is a Rust issue labeled good first issue, and Rust is a language I want to learn. Third, the maintainer, djmitche, said he would review a PR, and he is active (he merged a PR on 2026-11-02). llm4s#2243 was the easier option, but it is a docs-only edit in a language outside my profile and would teach me little. I hope to learn how Rust traits like `Deref` work, how a library's public types are laid out, and how to settle an open design question with a maintainer before writing code. As a tool review, the scout held up on required checks like `maintainer-active` and `repo-in-use`, but its scope check rejected nearly every real issue until I patched it, and its `issue-unclaimed` check could not tell my own claim from a stranger's. Its preferred-check grades also changed between runs on the same facts, so I treat them as hints, not facts. My claim comment: https://github.com/GothenburgBitFactory/taskchampion/issues/613#issuecomment-6702283993

**Toolkit**

- Tool: `issue-scout` (my search strategy and rubric), run in direct mode on two issue URLs, plus the Unit 6 scope patch.
- What it produced: A scan on 2026-11-06 accepting both picks, a second on 2026-11-07 that accepted llm4s#2243 (straightforward) and rejected #613, and a rerun that accepted #613 with a difficulty note of ambitious.
- Difficulties: The old scope check would have rejected most real issues. The `issue-unclaimed` check read my own claim as a stranger's. Preferred checks like `outside-prs-answered` and `newcomer-friendly` gave different answers on the same repo facts across runs.
- What changed: I replaced `scope-small-impact` with `scope-feasible` and added a difficulty note that carries my earlier limits (more than 3 files, core public types, unsettled design) as "ambitious" flags. I changed `issue-unclaimed` to ignore claims from my own login, which I named in the rubric and `scope.md`.

---

## Understanding the Issue

**Problem Description**

Nothing is broken, but something is missing. In taskchampion, `Task` has typed getters such as `get_description` and `get_due`, but `TaskData`, the low-level type that holds a task's UUID and key/value map, has none of them. Anyone working with a `TaskData` has to read raw property strings with `get` and parse them by hand.

**Expected Behavior**

A caller holding a `TaskData` can call the same simple getters that `Task` has (`get_status`, `get_description`, `get_entry`, `get_priority`, `get_wait`, `get_scheduled`, `get_due`, `get_modified`) and get the same defaults and parsed timestamps. The maintainer's reply on the issue narrowed this to getters only. The setters stay on `Task`, because `Task::set_value` stamps `modified` and `TaskData::update` does not.

**Current Behavior**

Calling any of those getters on a `TaskData` fails to compile with `E0599` (no method found). `Task` defines all of them, and each one reads `self.data`.

**Affected Components**

`src/task/data.rs` (`TaskData`) and `src/task/task.rs` (`Task`, its getters, `get_timestamp` and the private `Prop` enum). `src/task/mod.rs` re-exports both types, and `src/replica.rs` builds them, so neither needs to change.

**Toolkit**

- Tool: I used Claude Code to check my understanding of which methods can move in `data.rs` and `task.rs`.
- What it produced: A confirmation of which `Task` methods are plain reads of `self.data` and which depend on `Task`'s extra state (`modified` handling, the dependency map, synthetic tags).
- Difficulties: My initial evaluation of the issue assumed getters and setters would both move. I raised on 2026-11-08 that the setters cannot move and the maintainer agreed, so I had to redo the scope.
- What changed: After the maintainer agreed on #613, I limited the plan to the 8 getters and kept the setters on `Task`, because `Task::set_value` stamps `modified` and `TaskData::update` does not.

---

## Reproduction Process

**Environment Setup**

- OS: macOS 15.8.1 (x86_64)
- Rust: rustc 1.99.1 and cargo 1.99.1 (the repo's MSRV is 1.94.1; I did not build with 1.94.1)
- Repo: `GothenburgBitFactory/taskchampion` at commit `d6dc3cfe8` (taskchampion 3.1.1-pre), cloned from my fork (`git@github.com:LilRed92/taskchampion.git`) with a clean working tree
- Features: default features; the missing methods do not depend on any feature flag
- Baseline: `cargo test` at that commit gives 438 passed, 0 failed across all test groups (some feature-gated groups ran 0 tests)
- Challenges: `cargo` was not on my PATH in one shell until I loaded `~/.cargo/env`, and my test-log script stopped finding the clone after I moved it out of week 5, so I updated the script's path

**Steps to Reproduce**

#613 is a feature request, so there is no crash. The reproduction shows the requested methods are missing today.

1. Clone my fork and check out my tests-only commit, which sits directly on `d6dc3cfe8`: `git clone git@github.com:LilRed92/taskchampion.git && cd taskchampion && git checkout <commit>` (commit link below)
2. The commit adds three tests to `mod test` in `src/task/data.rs` (`getters_defaults`, `getters_values`, `getters_invalid_timestamp`). They call the 8 getters (`get_status`, `get_description`, `get_entry`, `get_priority`, `get_wait`, `get_scheduled`, `get_due`, `get_modified`) on a `TaskData`.
3. Run `cargo test --lib task::data`.
4. Observed result: The tests do not compile. There is an `E0599` error for each getter call, 21 in total (the three tests repeat the calls).

**Reproduction Evidence**

- **Commit showing reproduction:** https://github.com/LilRed92/taskchampion/commit/660140c1f
- **Screenshots/logs:** `cargo test --lib task::data` output, error lines only with repeated lines shown once, run on 2026-11-11 with the tests added on top of `d6dc3cfe8`:
  ```text
  error[E0599]: no method named `get_status` found for struct `data::TaskData` in the current scope
  error[E0599]: no method named `get_description` found for struct `data::TaskData` in the current scope
  error[E0599]: no method named `get_priority` found for struct `data::TaskData` in the current scope
  error[E0599]: no method named `get_entry` found for struct `data::TaskData` in the current scope
  error[E0599]: no method named `get_wait` found for struct `data::TaskData` in the current scope
  error[E0599]: no method named `get_scheduled` found for struct `data::TaskData` in the current scope
  error[E0599]: no method named `get_due` found for struct `data::TaskData` in the current scope
  error[E0599]: no method named `get_modified` found for struct `data::TaskData` in the current scope
  error: could not compile `taskchampion` (lib test) due to 21 previous errors
  ```
- **My findings:** The issue's premise holds today. `TaskData` in `src/task/data.rs` has `create`, `get_uuid`, `get`, `has`, `properties`, `iter`, `update` and `delete`, and none of the typed getters, while `Task` in `src/task/task.rs` defines all 8. A caller holding a `TaskData` has to use `get` with raw property strings, or convert to a `Task`.

**Toolkit**

- Tool: `repro-check`, run on my first claim comment and repro report together.
- What it produced: An accept verdict with all six required checks passing.
- Difficulties: My `repro-check` rubric is written for bugs, so I framed the report as a feature request and used a compile error as the observed result. The grader also noticed that my claim was already on the thread with older wording, so posting the new draft would have duplicated it.
- What changed: Two separate things, at different times. First, before grading, I fixed an error in my claim draft. It said `TaskData` exposes only `get_uuid`, but reading `data.rs` showed it also has `get`, `has`, `update` and others. Second, and unrelated to that fix, my plan changed to getters only after the maintainer agreed on #613, so I redid the reproduction for just the 8 getters, this time as failing tests inside the crate (21 errors across three tests, shown above). I have not run `repro-check` on that second report.

---

## Solution Approach

**Analysis**

The 8 getters live only on `Task` in `src/task/task.rs`: `get_status`, `get_description`, `get_entry`, `get_priority`, `get_wait`, `get_scheduled`, `get_due` and `get_modified`. Each one is a plain read of `self.data`, which is a `TaskData`. The timestamp ones go through `Task::get_timestamp`, which parses the stored string and calls `utc_timestamp`. `TaskData` in `src/task/data.rs` has `create`, `get_uuid`, `get`, `has`, `properties`, `iter`, `update` and `delete`, but no typed getters. The key names (`status`, `description`, and so on) are in the private `Prop` enum in `task.rs`, so `data.rs` cannot use them today.

**Proposed Solution**

Move the 8 getters to `TaskData`, with the same defaults and doc comments. Add a read-only `impl Deref<Target = TaskData> for Task` (no `DerefMut`) so existing `Task` callers still compile, delete `Task`'s own copies, and have `Task::get_timestamp` call `TaskData`'s version. This is what the maintainer, djmitche, agreed to on #613. If Cargo Semver Checks flags the removed `Task` methods, I will keep thin `Task` wrappers that call through to `TaskData`, which he said is fine. I am not changing: any setters, `set_status`, the dependency, blocking and tag methods, UDAs, annotations, or the public signatures of `Task`.

**Implementation Plan**

1. In `data.rs` `mod test`, add tests for the getters (defaults, values, an invalid timestamp). Run them first and confirm they fail with `E0599`. That output is my "before" evidence.
2. In `task.rs`, make `enum Prop` `pub(super)`, and in `data.rs` import `Prop`, `utc_timestamp`, `Status` and `Timestamp`.
3. In `data.rs`, add the 8 getters and `pub(in crate::task) fn get_timestamp`, with `Task`'s existing doc comments.
4. In `task.rs`, add the `Deref` impl, delete the 8 getters, and make `Task::get_timestamp` call `self.data.get_timestamp(property)`. Add a test that a `Task` derefs to `TaskData`.
5. Run `cargo test` (expect 442 passed: 438 baseline plus 4 new), `cargo fmt --check`, clippy, the nightly rustdoc check (`cargo +nightly rustdoc -p taskchampion --all-features -- -Z unstable-options --check -Dwarnings`, as CI runs it) and `cargo semver-checks` with the CI features, all locally before the PR. If semver-checks fails, add thin `Task` wrappers.

Deviation, recorded before building: I first thought both the getters and the setters had to move to `TaskData`, and my first plan said so. I raised this with the maintainer on 2026-11-08 and he agreed the setters cannot move, because `Task::set_value` stamps `modified` and `TaskData::update` deliberately does not. Going back through the code confirmed it, so this plan is getters only.

**Toolkit**

- Tool: I used `plan-check` to grade `plan.md` and my draft plan comment (`plan-comment.md`) against issue #613.
- What it produced: A verdict of accept. All seven checks passed, including the preferred honest-unknowns check. It also listed four things to fix before I could use the comment.
- Difficulties: The four fixes were the wording about running Cargo Semver Checks, which rustdoc command I meant, the credit for the setters point, and the commit-link placeholder. On the credit, my files said the maintainer's reply showed the setters cannot move, but I raised it first. The semver one came from my notes saying the tool was not installed, which was out of date because I installed it and nightly later. `plan-check` also said its own procedure is silent on two things. The first is how to read reproduction evidence for a feature request, where the repro is a failing test. The second is how to treat an unfilled placeholder.
- What changed: I kept the plan saying I run Cargo Semver Checks and rustdoc myself, and wrote out the full rustdoc command. I reworded the setters line to point at my 2026-11-08 comment, and put my pushed commit link in place of the placeholder.

---

## Testing Strategy

**Before and after.** My reproduction is the three getter tests in `src/task/data.rs` (`getters_defaults`, `getters_values` and `getters_invalid_timestamp`). On commit `660140c1f`, which holds only the tests, `cargo test --lib task::data` fails to compile with 21 `E0599` errors, because `TaskData` has no `get_status`, `get_description`, `get_entry`, `get_priority`, `get_wait`, `get_scheduled`, `get_due` or `get_modified`. On the branch head the same command gives 13 passed, 0 failed.

**The repo's own checks.** I ran the five checks the upstream CI runs, all locally, on the branch head:

- `cargo test`: 442 passed, 0 failed. That is the 438 baseline plus my 3 getter tests and the `test_deref_to_task_data` test.
- `cargo fmt --check`: clean.
- `cargo clippy --all-features --no-deps -- -D warnings`: clean.
- `cargo +nightly rustdoc -p taskchampion --all-features -- -Z unstable-options --check -Dwarnings`: clean.
- `cargo semver-checks --default-features --features sync,storage,storage-indexeddb`: 229 pass, 31 skip, no semver update required.

**What the checks caught.** `cargo semver-checks` failed after I deleted `Task`'s getters, with `inherent_method_missing` for 7 methods. That is why the branch has thin `Task` wrappers. The raw before and after output is in `test_evidence.md`, which I kept out of the commits.

**Toolkit**

- Tool: I used Claude Code to run the five checks and to record the before and after output.
- What it produced: The 21 `E0599` errors before the fix, and 442 passed with clean fmt, clippy, rustdoc and semver checks after it.
- Difficulties: The semver check failed in the middle of the work, so one passing run was not enough. I needed the failing run and the passing run both on record. Also, a stricter clippy run with `--all-targets` fails on files I did not touch (`src/server/cloud/aws.rs`, `src/storage/test.rs` and `src/task/time.rs`). That is not one of the CI checks, so I used the CI form.
- What changed: The failing semver run led to the thin `Task` wrappers, and I re-ran all five checks after adding them.

---

## Implementation Notes

**2026-11-12**

Added the 8 getters to `TaskData` in `src/task/data.rs`, plus a crate-private `get_timestamp` that they share, and made `enum Prop` `pub(super)` in `src/task/task.rs` so `data.rs` can use the key names. I copied the bodies and doc comments from `Task` as they are. Four of the `Task` getters (`get_status`, `get_description`, `get_entry`, `get_priority`) have no doc comment, so I wrote one-line comments for them in the same style as the other methods in `data.rs`. I left `Task` untouched in this step, so nothing can break yet. The three tests from my first commit now compile and pass (13 passed in `task::data`), and the full `cargo test` gives 441 passed, 0 failed, which is the 438 baseline plus the 3 getter tests. `cargo fmt --check` and clippy with `-D warnings` are clean.

**2026-11-12**

Added a read-only `impl Deref<Target = TaskData> for Task` with no `DerefMut`, deleted `Task`'s 8 getters, and made `Task::get_timestamp` call `self.data.get_timestamp(property)`. I added the `test_deref_to_task_data` test, which checks that a `Task` derefs to its `TaskData` and that `get_description` works through it. `cargo test` gives 442 passed, 0 failed, which is the 438 baseline plus the 3 getter tests and the deref test. `cargo fmt --check`, clippy with `-D warnings` and the nightly rustdoc check are clean. `cargo semver-checks` failed with `inherent_method_missing`, listing 7 removed `Task` methods: `get_status`, `get_description`, `get_entry`, `get_priority`, `get_wait`, `get_modified` and `get_due`. `get_scheduled` was not flagged, so it was not public in the 3.1.0 baseline. This is the case my plan covers, so the next step is thin `Task` wrappers that call through to `TaskData`.

**2026-11-12**

Added thin `Task` wrappers that call through to `TaskData` for the 7 methods `cargo semver-checks` flagged: `get_status`, `get_description`, `get_entry`, `get_priority`, `get_wait`, `get_modified` and `get_due`. I kept the doc comments the originals had. I also added a wrapper for `get_scheduled`, even though the check did not flag it, so that all 8 getters behave the same way on `Task`. Re-running all five checks gives 442 passed in `cargo test`, and `cargo fmt --check`, clippy, the nightly rustdoc check and `cargo semver-checks` are clean (229 pass, 31 skip, no semver update required). I amended the wrapper commit to include the `get_scheduled` wrapper and reworded its message, then force-pushed with `--force-with-lease` because no PR was open yet.

**Toolkit**

- Tool: Before each commit I used Claude Code to check that all of the getters, the `Deref` impl and the wrappers in `src/task/data.rs` and `src/task/task.rs` were written correctly.
- What it produced: Three commits plus the amend, each checked with the five checks before I committed it.
- Difficulties: Admittedly, I usually use AI to create my commit messages. Typically they're spot on, but for this project they were not. One described changes that did not happen and the wrapper commit message called the wrappers new getters. I ended up going back and amending two commit messages to fix before opening the PR.
- What changed: I rewrote the wrapper commit message to explain the semver reason, and amended and force-pushed the branch before opening the PR.

---

## Pull Request

**PR Link:** https://github.com/GothenburgBitFactory/taskchampion/pull/796

**PR Description:** The PR is titled "Add simple property getters to TaskData" and closes #613. It moves the 8 getters (`get_status`, `get_description`, `get_entry`, `get_priority`, `get_wait`, `get_scheduled`, `get_due` and `get_modified`) onto `TaskData`, adds a read-only `Deref<Target = TaskData>` for `Task`, and deletes `Task`'s copies. The setters stay on `Task`, as the maintainer agreed. `cargo semver-checks` flagged 7 removed `Task` methods, so the PR keeps thin `Task` wrappers for them, plus one for `get_scheduled` so all 8 match. The description shows the 21 `E0599` errors before, 13 passed in `task::data` after, and the five checks (442 passed in `cargo test`, 229 pass and 31 skip in `cargo semver-checks`). It also has an "AI help" section.

**Maintainer Feedback:**

- 2026-11-13: None yet.
- 2026-11-13: I posted a comment on the PR explaining that the Formatting failure is in `src/server/cloud/mod.rs`, which my PR does not touch, with the `cargo fmt --check` output from Rust 1.100.0 and a note that I am leaving the PR as it is: https://github.com/GothenburgBitFactory/taskchampion/pull/796#issuecomment-6866533657

**CI:** Every check passes except Formatting. That job fails on `src/server/cloud/mod.rs`, a file my PR does not touch, and `cargo fmt --check` passes locally. The fmt job runs on `stable`, and I think a newer rustfmt than mine changed how it wants block comments laid out, but I have not confirmed that.

**CI update (2026-11-13):** I went back and confirmed the cause. I updated my local toolchain from Rust 1.99.1 to 1.100.0, which was released on 2026-11-12. With 1.100.0, `cargo fmt --check` reports the same diff in `mod.rs` on my branch, so a newer rustfmt changed how it wants that block comment laid out. I changed nothing in the PR.

**Status:** Awaiting review

**Toolkit**

- Tool: I used the ship-gate and my gate manifest to check the branch, then opened the PR through Claude Code with `gh pr create` and `pr_draft.md`.
- What it produced: A `PASS`. The five repo checks ran (`cargo test`, `cargo fmt --check`, clippy, the nightly rustdoc check and `cargo semver-checks`), and `pr-precheck` passed all eight of its checks against my diff and description.
- Difficulties: The first line of `pr_draft.md` was the PR title, so it was repeated at the top of the description. Claude pointed that out when I ran the command to create the PR. After the PR opened, the upstream Formatting check failed on a file I did not touch, which the local gate could not catch because my toolchain differs from the one in CI.
- What changed: I deleted the title line from the description through GitHub after the PR was created. Nothing changed in the code. I recorded the CI result here instead of changing `mod.rs`, because the ship-gate had approved a diff of only `data.rs` and `task.rs` and mod.rs is out of scope anyway.

---

## Learnings and Reflections

**Technical Skills Gained**

I learned how a read-only `Deref<Target = TaskData>` for `Task` lets callers keep using methods that moved to another type, and why I left out `DerefMut`. I learned Rust's narrower visibility levels, `pub(super)` for `Prop` and `pub(in crate::task)` for `get_timestamp`, so the new code could use them without making them public. I learned that `cargo semver-checks` reports a removed method as `inherent_method_missing`, and that a thin wrapper that calls through to the new method keeps the public API the same. I also learned to find the checks a repo runs in its `.github/workflows/` files and to run the same commands locally before opening a PR, and to amend a pushed commit and push it with `--force-with-lease` before any PR is open.

**Challenges Overcome**

My first plan moved both the getters and the setters to `TaskData`. I raised on #613 that the setters cannot move, because `Task::set_value` stamps `modified` and `TaskData::update` does not, and the maintainer agreed, so I rebuilt the plan around the 8 getters only. After I deleted `Task`'s getters, `cargo semver-checks` failed on 7 removed methods, and I added thin wrappers (plus one for `get_scheduled`) until it passed. Several commit messages that were first drafted by my commit message generator that uses AI did not match the diff, so I checked each one against the change and rewrote the wrapper message before pushing. After I opened the PR, the Formatting check failed on `src/server/cloud/mod.rs`, a file I did not touch. I traced it to Rust 1.100.0, confirmed it by updating my toolchain, and left the PR alone.

**What I'd Do Differently Next Time**

I would install `cargo-semver-checks` and nightly Rust before writing my plan, because I had to correct the plan and the story after I realized I could run them locally. I would ask the maintainer about the scope at the start, before building a plan around the wrong assumption. I would read each commit message against its diff before accepting it. I would also keep my toolchain up to date when a repo's CI runs on `stable`, so my local checks match CI.

---

## Resources Used

- [Issue #613 and the maintainer's reply](https://github.com/GothenburgBitFactory/taskchampion/issues/613): the thread that set my scope to getters only and agreed to the thin-wrapper fallback.
- `CONTRIBUTING.md` and `.github/workflows/checks.yml` in taskchampion: they gave me the five checks I ran locally.
- [cargo-semver-checks](https://github.com/obi1kenobi/cargo-semver-checks): it caught the removed `Task` methods.
- [The `Deref` trait in the Rust standard library docs](https://doc.rust-lang.org/std/ops/trait.Deref.html): for the read-only `Deref` impl.
- Merged PRs #795, #779, #762, #757 and #722 on taskchampion: I used how fast djmitche replied to set my playbook's thresholds.
