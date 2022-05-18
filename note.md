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
```

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
```