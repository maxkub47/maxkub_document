---
sidebar_position: 12
title: Command Cheat Sheet
---

## Already Use

เรียกใช้ Icon Transfer ด้วย SH

```VBA
#!/bin/bash
ACSBUNDLE_JAR="/usr/local/ibmiaccess/acsbundle.jar"
DTFX_FILE="/Users/rattalig/Desktop/Output/temp.dtfx"
java -jar $ACSBUNDLE_JAR $DTFX_FILE
java_process_name=“AcsLaunchPad”
pid=$(ps aux | grep $java_process_name | grep -v grep | awk '{print $2}')
if [[ -n $pid ]]; then
  kill $pid
fi
```

ODBCINST

```shell
odbcinst -q -s
odbcinst -l
odbcinst -h
odbcinst -j
```

ISQL

```shell
isql -v metro240 max maxkub
isql metro240 max maxkub
isql metro240 max maxkub
isql -v metro240 max maxkub
isql metro240 max maxkub
```

PGCLI

```shell
pgcli -h 192.168.105.203 -p 7004 -U prod watanabe
```

SCP

```shell
scp unixODBC-2.3.9-1.ibmi7.2.ppc64.rpm  adsofr@10.200.123.99:/tmp
```

## Git

### Start New Project

```Shell
cd existing_repo
```

```Shell
git remote add origin https://gitlab.com/maxkub47/toollib.git
```

```Shell
git branch -M main
```

```Shell
git push -uf origin main
```

### Git Configuration & Setup

set a name that is identifiable for credit when review version history

```shell
git config --global user.name “[firstname lastname]”
```

set an email address that will be associated with each history marker

```shell
git config --global user.email “[valid-email]”
```

set automatic command line coloring for Git for easy reviewing

```shell
git config --global color.ui auto
```

### Initializing a Repository

initialize an existing directory as a Git repository

```shell
git init
```

retrieve an entire repository from a hosted location via URL

```shell
git clone [url]
```

Clones a specific branch from a repository.

```shell
git clone –branch <branch_name> <repository_url>
```

### Basic Git Commands

Adds a specific file to the staging area.

```shell
git add <file>
```

Adds all modified and new files to the staging area.

```shell
git add . or git add –all
```

Shows the current state of your repository, including tracked and untracked files, modified files, and branch information.

```shell
git status
```

Displays ignored files in addition to the regular status output.

```shell
git status –ignored
```

Shows the changes between the working directory and the staging area (index).

```shell
git diff
```

Displays the differences between two commits.

```shell
git diff <commit1> <commit2>
```

Displays the changes between the staging area (index) and the last commit.

```shell
git diff –staged or git diff –cached
```

Display the difference between the current directory and the last commit

```shell
git diff HEAD
```

Creates a new commit with the changes in the staging area and opens the default text editor for adding a commit message.

```shell
git commit
```

Creates a new commit with the changes in the staging area and specifies the commit message inline.

```shell
git commit -m “<message>” or git commit –message “<message>”
```

Commits all modified and deleted files in the repository without explicitly using git add to stage the changes.

```shell
git commit -a or git commit –all
```

Creates a new note and associates it with an object (commit, tag, etc.).

```shell
git notes add
```

Restores the file in the working directory to its state in the last commit.

```shell
git restore <file>
```

Moves the branch pointer to a specified commit, resetting the staging area and the working directory to match the specified commit.

```shell
git reset <commit>
```

Moves the branch pointer to a specified commit, preserving the changes in the staging area and the working directory.

```shell
git reset –soft <commit>
```

Moves the branch pointer to a specified commit, discarding all changes in the staging area and the working directory, effectively resetting the repository to the specified commit.

```shell
git reset –hard <commit>
```

Removes a file from both the working directory and the repository, staging the deletion.

```shell
git rm <file>
```

Moves or renames a file or directory in your Git repository.

```shell
git mv
```

### Git Commit

Create a new commit in a Git repository with a specific message to indicate a new feature commit in the repository.

```shell
git commit -m “feat: message”
```

Create a new commit in a Git repository with a specific message to fix the bugs in codebases

```shell
git commit -m “fix: message”
```

### Branching and Merging

Lists all branches in the repository.

```shell
git branch
```

Creates a new branch with the specified name.

```shell
git branch <branch-name>
```

Deletes the specified branch.

```shell
git branch -d <branch-name>
```

Lists all local and remote branches.

```shell
git branch -a
```

Lists all remote branches.

```shell
git branch -r
```

Switches to the specified branch.

```shell
git checkout <branch-name>
```

Creates a new branch and switches to it.

```shell
git checkout -b <new-branch-name>
```

Discards changes made to the specified file and revert it to the version in the last commit.

```shell
git checkout — <file>
```

Merges the specified branch into the current branch.

```shell
git merge <branch>
```

Displays the commit history of the current branch.

```shell
git log
```

Displays the commit history of the specified branch.

```shell
git log <branch-d
```

Displays the commit history of a file, including its renames.

```shell
git log –follow <file>
```

Displays the commit history of all branches.

```shell
git log –all
```

Stashes the changes in the working directory, allowing you to switch to a different branch or commit without committing the changes.

```shell
git stash
```

Lists all stashes in the repository.

```shell
git stash list
```

Applies and removes the most recent stash from the stash list.

```shell
git stash pop
```

Removes the most recent stash from the stash list.

```shell
git stash drop
```

Lists all tags in the repository.

```shell
git tag
```

Creates a lightweight tag at the current commit.

```shell
git tag <tag-name>
```

Creates a lightweight tag at the specified commit.

```shell
git tag <tag-name> <commit>
```

Creates an annotated tag at the current commit with a custom message.

```shell
git tag -a <tag-name> -m “<message>”
```

### Remote Repositories

Retrieves change from a remote repository, including new branches and commit.

```shell
git fetch
```

Retrieves change from the specified remote repository.

```shell
git fetch <remote>
```

Removes any remote-tracking branches that no longer exist on the remote repository.

```shell
git fetch –prune
```

Fetches changes from the remote repository and merges them into the current branch.

```shell
git pull
```

Fetches changes from the specified remote repository and merges them into the current branch.

```shell
git pull <remote>
```

Fetches changes from the remote repository and rebases the current branch onto the updated branch.

```shell
git pull –rebase
```

Pushes local commits to the remote repository.

```shell
git push
```

Pushes local commits to the specified remote repository.

```shell
git push <remote>
```

Pushes local commits to the specified branch of the remote repository.

```shell
git push <remote> <branch>
```

Pushes all branches to the remote repository.

```shell
git push –all
```

Lists all remote repositories.

```shell
git remote
```

Adds a new remote repository with the specified name and URL.

```shell
git remote add <name> <url>
```
