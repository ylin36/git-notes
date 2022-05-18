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

The --soft flag changes the state of the committed files to “staged.". this works if current branch is g
```
git reset --soft HEAD~
```

test4