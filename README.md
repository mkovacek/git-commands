# Useful Git Commands

## Table of contents

* [Setting up git](#setting-up-git)
* [Starting a repository](#starting-a-repository)
* [Checking the status of your files](#checking-the-status-of-your-files)
* [Staging files](#staging-files)
* [Committing](#committing)
* [Staging and remotes](#staging-and-remotes)
* [Working with remotes](#working-with-remotes)
* [Cloning and branching](#cloning-and-branching)
* [Merge and merge conflicts](#merge-and-merge-conflicts)
* [Tagging](#tagging)
* [Rebase](#rebase)
* [Stashing files](#stashing-files)
* [Cherry-pick](#cherry-pick)
* [Reflog](#reflog)
* [Restoring](#restoring)


##### Setting up git

```sh
# who gets credit for changes
$ git config --global user.name "User Name"

# what email you use
$ git config --global user.email "yourEmail@email.com"

#pretty command line colors
$ git config --global color.ui true 

#LINE ENDINGS
#On Unix - changes CR/LF to LF on commit
$git config --global core.autocrlf input 

#On Windows - changes LF to CR/LF on checkout
$git config --global core.autocrlf true 
```

##### Starting a repository

```sh
# initialized empty git repository (local)
$ git init
```

#### Checking the status of your files

```sh
$ git status
# On branch master
# nothing to commit (working directory clean)
```

If you add a new file to your project, and the file didn't exist before, when you run a `$ git status` you should see your untracked file like this:

```sh
$ git status
# On branch master
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#   README
# nothing added to commit but untracked files present (use "git add" to track)
```

#### Staging files

```sh
# Adding a file
$ git add <file>

# Adding all new or modified files
$ git add --all 

# Adding all files changes in a directory
$ git add .

# add all txt files in current directory
$ git add *.txt 

# add all txt files in docs directory
$ git add docs/*.txt 

# add all files in docs directory
$ git add docs/ 

# add all txt files in the whole project
$ git add "*.txt"  

# add all txt files in current directory
$ git add *.txt 
```

#### Committing

```sh
# commit changes (creates snapshots of staging)
$ git commit -m "Commit message" 

# add changes from all tracked files and commit, doesn't add new (untracked) files
$ git commit -a -m "Commit message" 
```

#### Staging and remotes

```sh
# shows unstaged differences since last commit
$ git diff  

# view staged differences
$ git diff --staged 

## Unstaging files

# unstage specific file , head refferes to last commit
$ git reset HEAD <fileName> 

# delete all changes since last commit from specific file
$ git checkout --<fileName> 

## Undoing a commit

# reset last commit into staging, ^ moves commit before HEAD
$ git reset --soft HEAD^

## Adding to a commit
$ git add <forgoted File>
$ git commit --amend -m 'We forgot to add a file to last commit'

## Undoing a commit and changes

# undo last commit and all changes
$ git reset --hard HEAD^ 

# undo last 2 commits and all changes
$ git reset --hard HEAD^^
```

#### Working with remotes

```sh
# add new remotes
$ git remote add <remote name> <address> 

# remove remotes
$ git remove rm <name> 

# show remotes
$ git remote -v 

# push to specific remotes
$ git push  <remote name> <branch> 

# pull from remote
$ git pull
```

#### Cloning and branching

```sh
# clone a repository
$ git clone <url> 

# creates branch
$ git branch <name>  

# switch to branch
$ git checkout <name> 

# creates and checks out to branch
$ git checkout -b <name> 

# pushes branch to remote, links local branch to the remote branch
$ git push origin <branch name> 

# list all remote branches
$ git branch -r 

# shows remote branches
$ git remote show origin 

# deletes remote branch
$ git push origin :<branch name> 

# deletes local branch
$ git branch -D <branch name> 

# cleans up deleted remote branches
$ git remote prune origin 
```

#### Merge and merge conflicts

```sh
# first switch to master or where you want to merge
$ git checkout master  

# than merge other branch to master
$ git merge <branch name>   

# MERGE CONFLICTS

# <<<<<<HEAD
#  local version code
# ==============
#  remote version code
# >>>>>>>>>>
# 45dsa5d4s5dsad45ds
```

#### Tagging

```sh
# list all tags
$ git tag   

# add a new tag
$ git tag -a v0.0.2  -m 'version 0.0.2'   

# push new tags
$ git push --tags 

# checkout code at commit
$ git checkout v0.0.2 
```

#### Rebase

```sh
# pull changes from remote
$ git fetch   

# move all changes to master which are not in origin/master to a temporary area; run all origin/master commits; run all commits in the temporary area, one at a time
$ git rebase    

## Local branch rebase

# switch to branch
$ git checkout <branch name>

# rebase master
$ git rebase master

# switch to master
$ git checkout master

# merge to master
$ git merge <branch name>

# if Conflicts, fix it and then git rebase --continue

## Interactive rebase
$ git rebase – i HEAD 

# Squashing commits together
$ git rebase -i
This will give you an interface on your core editor:
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit //THIS
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell

# Squashing commits together using reset --soft
$ git reset --soft HEAD~number_of_commits
$ git commit
$ git rebase -- continue


# Split commit 
$ git rebase -i
This will give you an interface on your core editor:
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending //THIS
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell

$ git reset --HEAD^
$ git add --all
$ git commit -m "Commit msg"
$ git rebase --continue
```


#### Stashing files

```sh
# Stash local changes
$ git stash

# Stash local changes with a custom message
$ git stash save "this is your custom message"

# Re-apply the changes you saved in your latest stash
$ git stash apply

# Re-apply the changes you saved in a given stash number
$ git stash apply stash@{stash_number}

# Drops any stash by its number
$ git stash drop stash@{0}

# Apply the stash and then immediately drop it from your stack
$ git stash pop

# 'Release' a particular stash from your list of stashes
$ git stash pop stash@{stash_number}

# List all stashes
$ git stash list

# Show the latest stash changes
$ git stash show

# See diff details of a given stash number
$ git diff stash@{0}

# staging area not to be stashed
$ git stash save –keep-index 

# untracked files to be stashed too
$ git stash save –include-untracked 

# clear all stashes at once
$ git stash clear
```

#### Cherry-pick

```sh
# takes specific commit to master branch
$ git checkout master
$ git cherry-pick 53212e5 

# edit for changing commit message
$ git cherry-pick --edit 53212  

# pull changes and stages them, but doesn't commit
$ git cherry-pick --no-commit 5321 6457 

# adds current user's name to commit message
$ git cherry-pick --signoff 5454 
```

#### Reflog

```sh
# secong log
$ git reflog
```

#### Restoring

```sh
# restore specific commit
$ git reset --hard 1e654 

# restore branch
$ git branch <new branch name> 287ed 
```
