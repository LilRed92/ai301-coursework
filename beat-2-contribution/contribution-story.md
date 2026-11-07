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
**Pull Request:** [GitHub PR link, once opened]

One repository, built across units 5 to 8, telling the whole story of your real
contribution. Fill it as you work, not at the end — the sections below ask for evidence that
is far easier to write down as it happens than to reconstruct in the last weekend.

Contribution Number stays `[1]` unless you make more than one contribution this term; it
just numbers them.

---

## Toolkit

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
one in the week it belongs to.

**Unit 5: Built a six-query search strategy, scanned GitHub with issue-scout, and tuned the scout and my fit profile from the results**

I built six `gh search issues` queries and a set of ranking filters from the fit profile I wrote before this unit, then updated that profile to state my skill levels (proficient in PERN/MERN, barely past beginner in Python, new to Rust, TypeScript, Tailwind and Web3, including beginner smart-contract work) and removed a sentence that contradicted my learning goals. The first scans let sprawling features and brand-new repos through, so I limited `scope-small-impact` to 3 files and added the preferred checks `outside-prs-answered`, `setup-doable`, `repo-established` and `newcomer-friendly`. In the strategy I capped results at one issue per repo, gave each query its own slot and raised the graded count to 6, dropped epic, tracking, umbrella, meta and roadmap issues, switched the JavaScript query to `react` with `help wanted` because I am proficient there, required `rust` in the Rust query's title or body, and added a Web3 query on `blockchain` after `web3` returned a legal glossary and a job post. The rerun still spent two of six slots on a Renovate dashboard and a parent issue, and the Tailwind and Web3 queries returned mostly large items, so I added a `dashboard` title drop and a bot-author filter, which I chose not to test with another practice scan.

**Unit 6: Installed a voice guard on my outgoing comments and wrote a local repo-memory file for taskchampion**

I installed the voice-guard hook, merged the four upstream rules into my voice guide (reworded so they fit any issue in any repo), and confirmed the hook fires: `gh issue comment --help` was blocked, which is the pass. My first check of the claim draft stopped on the rule against "tested locally" with no command or output, so I rewrote it to name the commit and the result (438 passed, 0 failed), and it then passed (guard log: stop at 14:29, pass at 14:38 on 2026-11-07). I also wrote a roughly 40-line `CLAUDE.local.md` for my taskchampion clone, with the CONTRIBUTING.md rules, the Task and TaskData files behind #613, the build and test commands, and "no AI policy stated". The repo ships no CLAUDE.md or AGENTS.md, so I dropped the import line, and I kept the file out of the PR with `.git/info/exclude`. The comment I already posted on #613 predates the guard and still uses the old "ran the test suite" wording, which the guard would block, so I will edit it when I make my next comment. I have only run the guard manually on drafts so far, so I have not yet seen it stop a real post.

**Unit 7: [one line on the tool work]**

[2-4 sentences: the ship-gate and your gate manifest. What it produced
on your real branch, what fought you, what changed because of it.]

**Unit 8: [one line on the tool work]**

[2-4 sentences: the PR-monitor and your playbook. What it read, what it
drafted, what you did with the draft.]

---

## Why I Chose This Issue

I found taskchampion#613 on the AI301 Issue Selection site, not through my own scan. My scout's searches turned up mostly Python and agent-framework issues, so I picked two candidates from the site and graded them directly: llm4s#2243 (add missing runnable samples to the Example Gallery) and taskchampion#613. On 2026-11-06 the scout accepted both. After I patched the rubric's scope check on 2026-11-07, it accepted llm4s#2243 as straightforward and rejected #613, because it read my own claim comment and assignment as a stranger's claim. I fixed that check and re-graded, and the scout accepted #613 with a difficulty note of ambitious: it touches the core Task and TaskData types, the maintainer's Deref idea is tentative, and moving public methods can trip the Semver check. Two preferred checks failed along the way: outside-prs-answered, because every recent PR is from the maintainer or dependabot, and newcomer-friendly on the first run, because Rust is new to me and the fix involves a trait impl.

I chose #613 anyway for three reasons. First, I like what the project does. TaskChampion implements the task storage and synchronization behind Taskwarrior, and any other application can also use it to maintain its own replica of a task list, so it is not tied to Taskwarrior. I am always looking for better task-management systems for myself, so I would be improving something I might use. Second, it is a Rust issue labeled good first issue, and Rust is a language I want to learn. Third, the maintainer, djmitche, said he would review a PR, and he is active (he merged a PR on 2026-11-02). llm4s#2243 was the easier option, but it is a docs-only edit in a language outside my profile and would teach me little. I hope to learn how Rust traits like Deref work, how a library's public types are laid out, and how to settle an open design question with a maintainer before writing code. As a tool review: the scout held up on required checks like maintainer-active and repo-in-use, but its scope check rejected nearly every real issue until I patched it, and its issue-unclaimed check could not tell my own claim from a stranger's. Its preferred-check grades also changed between runs on the same facts, so I treat them as hints, not facts. My claim comment: https://github.com/GothenburgBitFactory/taskchampion/issues/613#issuecomment-6702283993

**Toolkit**

- Tool: issue-scout (my search strategy and rubric), run in direct mode on two issue URLs, plus the unit 6 scope patch.
- What it produced: A scan on 2026-11-06 accepting both picks, a second on 2026-11-07 that accepted llm4s#2243 (straightforward) and rejected #613, and a rerun that accepted #613 with a difficulty note of ambitious.
- Difficulties: The old scope check would have rejected most real issues. issue-unclaimed read my own claim as a stranger's. Preferred checks like outside-prs-answered and newcomer-friendly gave different answers on the same repo facts across runs.
- What changed: Replaced scope-small-impact with scope-feasible and added a difficulty note that carries my earlier limits (more than 3 files, core public types, unsettled design) as "ambitious" flags. Changed issue-unclaimed to ignore claims from my own login, which I named in the rubric and scope.md.

---

## Understanding the Issue

**Problem Description**

[In your own words, what is broken or missing?]

**Expected Behavior**

[What should happen?]

**Current Behavior**

[What actually happens?]

**Affected Components**

[Which parts of the codebase are involved?]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Reproduction Process

**Environment Setup**

macOS 15.8.1 (x86_64), rustc 1.99.1 and cargo 1.99.1 (the repo's declared MSRV is 1.94.1; I did not build with 1.94.1). The project is taskchampion 3.1.1-pre at upstream `main`'s commit `d6dc3cfe8`, cloned from my fork (`git@github.com:LilRed92/taskchampion.git`) with a clean working tree. I used the library only, with `default-features = false, features = ["storage"]`, since the missing methods do not depend on any feature flag. As a baseline I ran `cargo test` at that commit: 438 passed, 0 failed across all test groups (some feature-gated groups ran 0 tests). Challenges: `cargo` was not on my PATH in one shell until I loaded `~/.cargo/env`, and my test-log script stopped finding the clone after I moved it out of week 5, so I updated the script's path.

**Steps to Reproduce**

#613 is a feature request, so there is no crash. The reproduction shows the requested methods are missing today.

1. Clone my fork and check out `d6dc3cfe8`: `git clone git@github.com:LilRed92/taskchampion.git && cd taskchampion && git checkout d6dc3cfe8`
2. Outside the clone, make a new crate (`cargo new repro613`) with these dependencies in `Cargo.toml` (use the path to your clone):
   ```toml
   taskchampion = { path = "../taskchampion", default-features = false, features = ["storage"] }
   uuid = { version = "1", features = ["v4"] }
   chrono = "0.4"
   ```
3. Replace `src/main.rs` with a program that creates a `TaskData` and calls the 8 getters (`get_status`, `get_description`, `get_entry`, `get_priority`, `get_wait`, `get_scheduled`, `get_due`, `get_modified`) and the 7 setters (`set_description`, `set_priority`, `set_entry`, `set_wait`, `set_scheduled`, `set_due`, `set_modified`) on it. The full file is in my repro report; each call is one line, for example `let _ = td.get_status();` and `td.set_wait(None, &mut ops).unwrap();`.
4. Run `cargo build`.
5. Observed result: the build fails with 15 errors, one per call.

**Reproduction Evidence**

- **Commit showing reproduction:** none (the scratch crate lives outside the clone; the clone has no changes)
- **Screenshots/logs:** `cargo build` output, error lines only:
  ```text
  error[E0599]: no method named `get_status` found for struct `TaskData` in the current scope
  error[E0599]: no method named `get_description` found for struct `TaskData` in the current scope
  ... (the same error for each of the other 13 methods)
  error: could not compile `repro613` (bin "repro613") due to 15 previous errors
  ```
- **My findings:** the issue's premise holds today. `TaskData` in `src/task/data.rs` has `create`, `get_uuid`, `get`, `has`, `properties`, `iter`, `update` and `delete`, and none of the typed accessors, while `Task` in `src/task/task.rs` defines all 15. A caller holding a `TaskData` has to use `get`/`update` with raw property strings, or convert to a `Task`. I did not check the maintainer's `Deref` suggestion; that is for my plan. `set_status`, the dependency methods and the tag methods depend on `Task`'s extra state, and I have not judged whether they belong on `TaskData`.

**Toolkit**

- Tool: repro-check, run on my claim comment and repro report together.
- What it produced: an accept verdict with all six required checks passing.
- Difficulties: my repro-check rubric is written for bugs, so I framed the report as a feature request and used a compile error as the observed result. The grader also noticed that my claim was already on the thread with older wording, so posting the new draft would duplicate it.
- What changed: before grading I corrected a line in my claim draft that said `TaskData` exposes only `get_uuid`, which I found by reading `data.rs` (it also has `get`, `has`, `update` and others). I will edit my posted comment to match instead of adding a second one.

---

## Solution Approach

**Analysis**

[Your analysis of the root cause: what is causing the issue, traced
to the files and functions involved.]

**Proposed Solution**

[High-level description of your fix approach, and what you are
deliberately NOT changing.]

**Implementation Plan**

1. [Modify file X to do Y]
2. [Add or change Z]
3. [Update tests]

[Record deviations here as they happen: what changed mid-build and
why. A recorded deviation is honest work; silent drift is not.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Testing Strategy

[What observable checks prove the fix: your reproduction steps re-run
against the built change (before and after), and the repo's own test
suite or checks with the outcome shown. "Tests pass" with nothing
observable named is not a strategy.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Implementation Notes

[A running log, added to as you work. Date each entry. What you
built, decisions you made when you made them, wrong turns included.]

**[Date]**

[Entry]

**[Date]**

[Entry]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Pull Request

**PR Link:** [GitHub PR URL when opened]

**PR Description:** [what the PR says; much of the content above
adapts into it]

**Maintainer Feedback:**

- [Date]: [feedback received, or "none yet"; silence is a normal
  state and costs you nothing]
- [Date]: [how you addressed it]

**Status:** [Awaiting review / Iterating / Merged / Closed. The
status is a fact you record, never a grade: the PR is graded as
opened.]

**Toolkit**

- Tool:
- What it produced:
- Difficulties:
- What changed:

---

## Learnings and Reflections

**Technical Skills Gained**

[What you learned technically, named concretely.]

**Challenges Overcome**

[What was hard and how you solved it; point at the real events, the
Toolkit blocks above are full of them.]

**What I'd Do Differently Next Time**

[Reflection on your process.]

---

## Resources Used

[What actually helped, not a reading list. List things this story
already shows you using: the doc you followed to set the environment
up, the thread that explained the bug, the person who answered you.
One real entry beats ten plausible ones.]

- [Link to documentation that helped]
- [Discussion, issue, or post that helped]
