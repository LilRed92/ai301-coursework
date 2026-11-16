I found a gap in an open source task-management library called TaskChampion and opened a fix for it. Its simple "read this field" helpers worked on one kind of data but not on the closely related kind underneath it, so I moved them where they belong.

The fix is open for review, so I can't call it finished. The maintainer agreed with my plan in writing, and my own tests went from failing to passing.

The part I'm proudest of is that my first plan was too big. I had planned to move the helpers that read data and the helpers that change it. When I reread the code, I saw the changing ones skip a step that records when something was last edited. I told the maintainer before going further. He agreed, and he added a reason I hadn't thought of. I threw away what I had built and started over with the smaller plan.

It was my first real contribution to someone else's project. Asking before building cost me a few hours of work and saved the maintainer a review of something he would have turned down.

https://github.com/GothenburgBitFactory/taskchampion/pull/796

#opensource #rust
