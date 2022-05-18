- [git works in snapshots](#git-works-in-snapshots)
- [git states](#git-states)
- [git config](#git-config)
- [git init/add/commit](#git-initaddcommit)
- [git log](#git-log)
- [git reset](#git-reset)
  - [--soft](#--soft)
  - [-hard](#-hard)
  - [HEAD~#](#head)
- [branch](#branch)
  - [checkout](#checkout)
  - [branch then checkout](#branch-then-checkout)
  - [renaming current branch](#renaming-current-branch)
  - [renaming branch without switching over](#renaming-branch-without-switching-over)
  - [deleting branch](#deleting-branch)
- [stash](#stash)
- [git merge](#git-merge)
  - [merge conflicts](#merge-conflicts)
  - [resolve merge conflict](#resolve-merge-conflict)
- [remote repo](#remote-repo)
  - [.gitignore](#gitignore)
  - [add remote and alias](#add-remote-and-alias)
  - [git push](#git-push)
  - [git clone](#git-clone)
  - [shallow clone](#shallow-clone)
  - [git fetch](#git-fetch)
  - [git pull](#git-pull)
- [git revert](#git-revert)
- [Pull request](#pull-request)
- [git rebase](#git-rebase)
  - [rebase conflicts](#rebase-conflicts)
  - [rebase vs merge](#rebase-vs-merge)
  - [When should you use merge vs rebase?](#when-should-you-use-merge-vs-rebase)
- [other notable items during Pull Request (Taken from bitbucket)](#other-notable-items-during-pull-request-taken-from-bitbucket)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>


## git works in snapshots
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

## git init/add/commit
```
git init
git add .

git status

git commit -m "message"
```

## git log
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
## git reset
### --soft
If you want to modify or update your changes from the previous commit but don’t want to remove them completely

The --soft flag changes the state of the committed files to “staged.".

git reset --soft HEAD~1 is used.
```
E:\git\git-notes>git log
commit bf97995ea9a7186f3b4a5c18ddb4fdbebc457662 (HEAD -> test)
Author: Yang Lin <ylin3..
Date:   Tue May 17 21:57:12 2022 -0400

    test 4

commit 0b30b41318e4acb905aaf179df73af556038f3f8 (master)
Author: Yang Lin <ylin..
Date:   Tue May 17 21:53:47 2022 -0400

    phase2

commit d64d3d17b737ffab51693d6fff3a3d6a27ba0fb2
Author: Yang Lin <y..
Date:   Tue May 17 21:44:49 2022 -0400

    next changepoint

commit 01f16df373329d61d3bce5e219c2a1591fc55eef
Author: Yang Lin <yl..
Date:   Tue May 17 21:38:52 2022 -0400

    add notes

E:\git\git-notes>git reset --soft HEAD~1

E:\git\git-notes>git log
commit 0b30b41318e4acb905aaf179df73af556038f3f8 (HEAD -> test, master)
Author: Yang Lin <yl..
Date:   Tue May 17 21:53:47 2022 -0400

    phase2

commit d64d3d17b737ffab51693d6fff3a3d6a27ba0fb2
Author: Yang Lin <yl..
Date:   Tue May 17 21:44:49 2022 -0400

    next changepoint

commit 01f16df373329d61d3bce5e219c2a1591fc55eef
Author: Yang Lin <yli..
Date:   Tue May 17 21:38:52 2022 -0400

    add notes
```

### -hard
if you want to get rid of changes that were part of the recent commit, --hard flag will reset the change and not preserve them.

```
git reset --hard HEAD~1
```

### HEAD~#
dictate how many commits to go back
```
git reset --soft HEAD~2

// go back 2 commits
```

## branch
branch without switching current branch
```
git branch <branch-name>
```

### checkout
```
git checkout <branch-name>
```
### branch then checkout
```
git checkout -b <branch-name>
```

### renaming current branch
switch over to the branch you want to rename, then use git branch -m to rename it
```
git checkout <branch-name>
git branch -m <new-name>
```

### renaming branch without switching over
```
git branch -m old_name new_name
```
### deleting branch
**you cannot delete branch you are currently on**
```
git branch -d <branch-name>
```

## stash
if while working on your separate branch and making some changes that you don’t want to commit just yet, but you will be required to switch over to another branch to do something else in between.
```
git stash // notice files will disappear

git checkout other-branch // do work on other branch
git checkout prev-branch // come back

git stash apply // reapply the stashed files
```

## git merge
when we merge the two branches, they will find the most recent common commit that they share. From that point forward, the commit history will be different for both branches. Git will then merge the branch into the other by creating a **new merge commit** for it.

Once the merging process is complete, the commit history of the merged branch will also become part of the branch with which it merged. The changes that were present only in the feature branch will also become available in the master branch as well.
```
git checkout master
git merge <feature-branch>
```

### merge conflicts
```
git checkout -b feature-branch
echo 'changed in feature-branch' > file1.txt
git commit -m 'changed f1'

git checkout master
echo 'changed in master' > file1.txt
git commit -m 'changed f1' 

git merge feature_branch
```

### resolve merge conflict
choose which one you want. 
```
<<<<<<< HEAD
=======
>>>>>>> feature-branch
```
```
git add file1.txt
git commit -m "fixed merge conflict"
```

## remote repo
### .gitignore
```
# if you dont want to track a single file
abc.txt

#if you dont want to track files with a certain extension
*.pyc

# if you dont want to track a directory
htmlcov/
```

### add remote and alias
add our remote repository to the local one.
```
// give it <name> origin like below instead
git remote add <name> <url_to_remote_repository> 
```
Note: The name origin is essentially a more human-readable way to link to the remote repository instead of always having to use the actual URL. origin is simply a conventional name, but we can use any other name as well.
```
git remote add origin <url_to_remote_repository>
```

### git push
example of pushing to master in origin, if we're already on master
git push <remote_repository> <branch_name>
```
git push origin master
```
link upstream for current branch when pushing
```
git push -u origin <branch-name>

// future just do git push
```

### git clone
```
git clone <link_to_repository>

// clone a branch that the HEAD in the remote repository doesn’t point to by default, 
// you can also provide the name of that specific branch with the git clone command.
git clone --branch <branch_name> <link_to_repository>
```
### shallow clone
if a remote repository that we want to clone has too long of a commit history that will result in longer times to download and clone. This occurs when the project is very large and has a very large commit history. we can clone the commit history up to a certain point by using the --depth flag.
```
git clone <repository_url> --depth 1
```
### git fetch
download the updated changes from a remote repository.

it merely downloads the latest changes and does not affect your local codebase and updates. you can use it to look how remote has changed

For example, let’s say you are working on the master branch,
```
git fetch origin
```
to merge it when you're ready
```
git merge origin/master
```
**during this, you could have switched over to the fetched branch using**
```
git checkout origin/master command.
```

### git pull
fetch and merges
```
git pull origin branch_name
```

## git revert
git reset only works well locally because changing the commit history on a remote repository will result in a history conflict with everyone who has a clone of that repository. The remote commit history will begin to differ from theirs.

In order to set an old commit, which is free from any known flaw, and have it set as our latest commit, we can use the following command:

**git revert will add another commit on top of the commit** that contains flaws in your code.

```
git revert HEAD~1
```

## Pull request
intermediate step before you can merge your contribution into the source code

## git rebase
rebase is useful for making sure that the branch you are working on diverges from the latest version of the parent branch.

before rebase
```
       my-branch---e---f
           /
master--a-----b---c----d
```
rebase current my-branch with master
```
git checkout my-branch
git rebase master
```
after rebase
``` 
                my-branch---e---f
                       /
master --a---b---c---d
```

example usecase:

We want to make sure that new-branch looks like it is taken out from the latest version of the master branch. This means that new_branch would be branching out from the latest commit from master.
```
Checkout to the new-branch from the currently active master branch.
Enter git rebase master
```

### rebase conflicts
```
        my-branch----c
               /      
master -------a--b

if c and b touches same lines of code
this will fail
          my-branch X--c
                   /      
master -------a--b
```
you have to resolve the merge conflict 
once merge conflict is resolved
```
git rebase --continue
```

### rebase vs merge

rebase|merge
|--|--|
|does not result in new commits.<br>makes rebased branch’s commit history to look like it <br>was branched from most recent version of the parent branch.|new merge commit for the branch with which another is merged.|

### When should you use merge vs rebase?

* *rebase* *is not* ideal when multiple people working on a particular branch. collaborators can routinely pulling the latest version of the branch on their local machines, unaware that someone rebased it, fundamentally altering its state and leading to inconsistent branches for everyone. 

* If the branch were rebased and pushed to the remote repository, when others pull it, the updated branch would conflict with the local one even though it would be the same branch.

* *git merge* if alter the commit history of a branch *is not* ideal.

* git merge will retain the commit history as it is and add a new merge commit instead, while rebasing a branch will alter the commit history for that branch. This is nice for others collaborating on a branch since one person merging another branch with it would result in a new commit that others can easily pull locally from a remote repository. 

* rebase *is* ideal if you’re the only dev on the branch. rebasing makes the branch line look nice.

## other notable items during Pull Request (Taken from bitbucket)
* Merge commit (--no-ff) DEFAULT: Always create a new merge commit and update the target branch to it, even if the source branch is already up to date with the target branch.
* Fast-forward (--ff): If the source branch is out of date with the target branch, create a merge commit. Otherwise, update the target branch to the latest commit on the source branch.
* Fast-forward only (--ff-only): If the source branch is out of date with the target branch, reject the merge request. Otherwise, update the target branch to the latest commit on the source branch.
* Rebase, merge  (rebase + merge --no-ff): Commits from the source branch onto the target branch, creating a new non-merge commit for each incoming commit. Creates a merge commit to update the target branch. The PR branch is not modified by this operation.
* Rebase, fast-forward (rebase + merge --ff-only): Commits from the source branch onto the target branch, creating a new non-merge commit for each incoming commit. Fast-forwards the target branch with the resulting commits. The PR branch is not modified by this operation.
* Squash (--squash): Combine all commits into one new non-merge commit on the target branch.
* Squash, fast-forward only (--squash --ff-only): If the source branch is out of date with the target branch, reject the merge request. Otherwise, combine all commits into one new non-merge commit on the target branch.






