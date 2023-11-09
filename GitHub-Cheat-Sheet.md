# GitHub Cheat Sheet

Git Commands and actions.

## Command And Document Keys 

`[ PLACEHOLDER ]` - command input parameter

`--PLACEHOLDER` - command parameter   

## Setup And Init 

Setting up account/user information that is used across the GitHub instance and is applied to all local repositories.

### Configuring Account 

`git config --global user.name “[firstname lastname]”` - setting usrname for log references

`git config --global user.email “[valid-email]”` - setting an email to be assoicated with each history marker and a log reference 

`git config --global color.ui auto` - set auto command link highlighting for Git command reviewing  

## Commits And Staging 

Git staging area

`git status` - show modified files in working dir, these will be the changes within the next commit

`git add [file]` - add a file thats in this current state to your next commit

`git reset [file]` - unstage a file while retaining the changes in working dir

`git diff` - show difference of whats not yet staged

`git diff --staged` - show difference of whats staged but not yet commited

`git cimmit -m [commit description(short but detailed)]` - commit current state of changes on working dir (add destriptive message) 

## Branches And Merging

``

## Compare

## Fetch(Update), Pull(Fetch & Merge) And Share

## Tracking 

## Rewrite History 

## Temp And Stashes

## Reference 

### [2023] GitHub Education - https://education.github.com/git-cheat-sheet-education.pdf

