# Getters Only: How My First Plan for TaskChampion #613 Got Smaller and Better

## Overview

TaskChampion is the Rust library behind Taskwarrior's task storage and sync. Its `Task` type has typed getters and setters such as `get_due` and `set_wait`, but the lower-level `TaskData` type has none, so anyone holding a `TaskData` has to read raw strings and parse them by hand. I took issue #613 to close that gap. My first plan was too big, and the maintainer and I cut it down before I wrote the fix. I then built the smaller version and opened PR 796: https://github.com/GothenburgBitFactory/taskchampion/pull/796. It is open and waiting for review.

## What happened

**1. I built the first plan before asking.** After claiming the issue I read `src/task/data.rs` and `src/task/task.rs`. My first approach added 8 getters and 7 setters to `TaskData` and kept `Task`'s methods in place. I built it locally with 7 unit tests, and `cargo test` showed 445 passed, 0 failed.

**2. Going back through the code showed a problem with the setters.** `Task::set_value` stamps the `modified` timestamp, and `TaskData::update` deliberately does not. Setters on `TaskData` would skip that step. On 2026-11-08 I posted this on the issue.

> The getters are plain single-key reads and can move to `TaskData` unchanged. The setters can't move as they are: `Task::set_value` stamps `modified` and tracks it in `Task`'s `updated_modified` flag, while `TaskData::update` deliberately does not.

**3. The maintainer found a second reason I had missed, and set the scope.** djmitche replied on the issue.

> The setters do two things that aren't practical for TaskData: update `modified`, and add the change to `ops`. In fact, it really wouldn't make sense to change the data in a TaskData object, as there would be no way to make that change in the replica.
>
> So, let's just focus on the getters, which I think means we can use Deref.

**4. I changed my own work.** I threw away the 7 setters and their tests and rebuilt the plan around the 8 getters and a read-only `Deref`. I also moved the proof to the front. Before writing any fix, I committed three failing tests (`660140c1f`) and ran `cargo test --lib task::data`.

```
error[E0599]: no method named `get_status` found for struct `data::TaskData` in the current scope
error[E0599]: no method named `get_description` found for struct `data::TaskData` in the current scope
...
error[E0599]: no method named `get_modified` found for struct `data::TaskData` in the current scope
error: could not compile `taskchampion` (lib test) due to 21 previous errors
```

After I added the 8 getters to `TaskData`, the same command on the branch head gave this.

```
test task::data::test::getters_defaults ... ok
test task::data::test::getters_values ... ok
test task::data::test::getters_invalid_timestamp ... ok
test result: ok. 13 passed; 0 failed
```

**5. What landed.** The maintainer agreed to the narrowed scope in writing, the failing tests now pass, and the full `cargo test` run gives 442 passed and 0 failed (the 438 baseline plus 4 new tests). PR 796 is open and has not been reviewed yet, so the change is not merged.

## Limitations and what's next

My first plan cost me a full local build and 7 tests that I threw away. I only found the problem because I reread the code. I would not have found the second reason (`ops`) at all without the maintainer. The fix is also narrow. It covers read access only, and `TaskData` still has no typed way to write a property. That is deliberate, but it means the original idea in #613 is only half done. I also have no review yet, so I do not know if djmitche wants the `Deref` approach handled differently.

My next step is to wait on the PR. My playbook says to nudge only after 5 quiet days with no reply, and I will rework the change if the maintainer asks. For my own habits, I will post my plan and my questions on the issue before building next time, not after.
