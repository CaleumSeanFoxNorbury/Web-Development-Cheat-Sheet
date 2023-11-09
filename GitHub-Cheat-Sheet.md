# GitHub Cheat Sheet

**Git Commands and actions.**

## Command And Document Keys 

`[ PLACEHOLDER ]` - command input parameter

`--PLACEHOLDER` - command parameter

`local branch` - locally pulled down remote branch, stored locally

`remote branch` - branch stored on github servers, diffs from local branch if any local changes are made

## Setup And Init 

**Setting up account/user information that is used across the GitHub instance and is applied to all local repositories.**

### Configuring Account 

`git config --global user.name “[firstname lastname]”` - setting usrname for log references

`git config --global user.email “[valid-email]”` - setting an email to be assoicated with each history marker and a log reference 

`git config --global color.ui auto` - set auto command link highlighting for Git command reviewing  

## Commits And Staging 

**Git staging area**

`git status` - show modified files in working dir, these will be the changes within the next commit

`git add [file]` - add a file thats in this current state to your next commit

`git reset [file]` - unstage a file while retaining the changes in working dir

`git diff` - show difference of whats not yet staged

`git diff --staged` - show difference of whats staged but not yet commited

`git cimmit -m [commit description(short but detailed)]` - commit current state of changes on working dir (add destriptive message) 

## Branches And Merging

**Isloating, changing, and intgrating branchs** 

`git branch` - list of branches, show current active branch with a `*` 

`git branch [branch-name]` - create a new branch within the current commit

`git checkout` - switch branches, and check it out into your working dir

`git merge [branch]` - merge branches history (commit tree) into current active branch

`git log` - show all commits in branch history

## Inspect And Compare

**Exploring logs, differences and object information**

`git log` - show commit tree fro current active branch

`git log branchB..branchA` - showe commits from branchA that arnt in branchB

`git log --follow [file]` - show commits from manipulated specified file

`git diff branchB..branchA` - show diff of whats in branchA thats not in branchB

`git show [SHA]` - show any git object in human readable format

## Fetch(Update), Pull(Fetch & Merge) And Share

**Fethcing and updating local repositories and updates from remote repositories**

`git remote add [alias] [url]` - add a git url as a alias

`git fetch [alias]` - fetch down all branches and their changes from git remote specified by the alias

`git merge [alias]/[branch]` - merge a remote branchs changes into current branch(this could cause merge conflicts to be resolved) 

`git push [alias] [branch]` - push local branch changes to remote branch 

`git pull` - fetch and merge any changes (commits) from the tracking (current) remote branch  

## Tracking 

**Vesioning and removing files and file paths**

`git rm [file]` - delete file and stage the removal for next commit

`git mv [existing-branch-path] [new-path]` - change existing file path and stage the move for next commit

`git log --stat -M` - showing all commit logs, with highlighted any paths that have been manipulated

## Rewrite History 

**Rewritting changes to branches, updating commits and clearing history**

`git rebase [branch]` - apply all commits of current ative branch ahead of specified one, keeps git tree clean with updates

`git reset --hard [commit]` - clear staging area, rewrite working tree from specified commit 

## Temp And Stashes

**Temp store changes from tracked files**

`git stash` - saved manipulated and staged changes

`git stash list` - list `stack-order` of stashed file changes

`git stash pop` - write workingt from top of stash stack

`git stash drop` - discard the changes from top of stash-stack


## .gitignore

Adding a git ignore file will allow git to ignore certain files or directories that shouldn’t be pushed to githubs servers, these files should be applied to dependency directories or files containing sensitive information, please remember as soon as code has been pushed, the information will forever like within the commit tree and can be retrieved. Any exposed keys or passwords should be changed immediately.

**Example:**

```
    /directoryPath
```

Once a change has happened within the `.gitignore` file, then the command below will need to be run for these changes to be applied.

`git rm -r --cached [file/folder path]`

## Reference 

### [2023] GitHub Education - https://education.github.com/git-cheat-sheet-education.pdf

