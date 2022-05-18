## git snapshots
* state of the project files at a given time. 
* instead of maintaining record of file-based changes, git stores it as snapshot (entire state of the proj at that moment).
* while saving snapshot, it keeps files that did not get updated, and only keep references of files that didn't change from prev snapshot to avoid dupes.

* example below. file 3 didn't change on snapshot2

|snap1|snap2|
|--|--|
|file1 v1|file2 v2|
|file2 v1 |file2 v2|
file3 v1|->|

## git states
1) Modified - files that have changed, but not yet marked by git. Won't be part of next snapshot
2) Staged - tracked by git and will be marked for next snapshot
3) Committed - changed files that have successfully become part of latest snapshot

## git config
```
git config --global user.email "ylin@mail.com"
git config --global user.name "Yang Lin"
```

## git commands
```
git init
git add .

git status

git commit -m "message"
```

git log to view commit history sorted based on time of creation. desc.
commit hash is sha-1. hashkey keeps integrity of the commit

```
git log

E:\git\git-notes>git log
commit 01f16df373329d61d3bce5e219c2a1591fc55eef (HEAD -> master)
Author: Yang Lin <ylin366@gmail.com>
Date:   Tue May 17 21:38:52 2022 -0400

    add notes
```
unstage files from prev git add .
```
git reset
```
If you want to modify or update your changes from the previous commit but don’t want to remove them completely

The --soft flag changes the state of the committed files to “staged.". this seems to work if HEAD~

git reset --soft HEAD~ is used. which resets all commit back to stage that's diff from current branch and the source branch.
```
E:\git\git-notes>git log
commit bf97995ea9a7186f3b4a5c18ddb4fdbebc457662 (HEAD -> test)
Author: Yang Lin <ylin366@gmail.com>
Date:   Tue May 17 21:57:12 2022 -0400

    test 4

commit 0b30b41318e4acb905aaf179df73af556038f3f8 (master)
Author: Yang Lin <ylin366@gmail.com>
Date:   Tue May 17 21:53:47 2022 -0400

    phase2

commit d64d3d17b737ffab51693d6fff3a3d6a27ba0fb2
Author: Yang Lin <ylin366@gmail.com>
Date:   Tue May 17 21:44:49 2022 -0400

    next changepoint

commit 01f16df373329d61d3bce5e219c2a1591fc55eef
Author: Yang Lin <ylin366@gmail.com>
Date:   Tue May 17 21:38:52 2022 -0400

    add notes

E:\git\git-notes>git reset --soft HEAD~

E:\git\git-notes>git log
commit 0b30b41318e4acb905aaf179df73af556038f3f8 (HEAD -> test, master)
Author: Yang Lin <ylin366@gmail.com>
Date:   Tue May 17 21:53:47 2022 -0400

    phase2

commit d64d3d17b737ffab51693d6fff3a3d6a27ba0fb2
Author: Yang Lin <ylin366@gmail.com>
Date:   Tue May 17 21:44:49 2022 -0400

    next changepoint

commit 01f16df373329d61d3bce5e219c2a1591fc55eef
Author: Yang Lin <ylin366@gmail.com>
Date:   Tue May 17 21:38:52 2022 -0400

    add notes
```

test4