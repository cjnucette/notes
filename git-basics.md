# git-basics

## `git init`
Creates a new repository in the current directory.

## `git clone <url> [<new name>]`
Gets repository from a remote server pointed by <url> and giving optionally a <new name>.  
<url> can be:
* https: https://github.com/libgit2/ligbit2
* git: git://github.com/user/libgit2.git
* ssh: user@server/libgit2.git


## `git config--system/--global/--local`
Sets options used when committing files.
* git config --global user.name='name of the user'.
* git config --global user.email='user@email.com'

## `git config --list`
Lists the current options.

## `git status`
Displays the current status of the files (tracked and untracked) in the  working directory and the staging area.

## `git add `filename/glob pattern`
* **flow: working directory -> staging area.**
Adds the specified file(s) to the staging area.

## `git commit`
* **flow: staging area -> commit (history).**
Commits staged files to the repository.

## `git log`
Shows commit history.

## `git log -p`
Shows commit history including the file's changes.

## `git log -- filename`
Shows commit history for the given file.

## `git diff`
Shows differences between files in the working directory and the staging area.

## `git diff --staged`
Shows differences between files in the staging area and the commit (history).

## `git rm filename`
Removes the file from the working directory, and stages the delete.

## `git restore "filename" or git checkout -- "filename"`
* **flow: staging area -> working directory.**
Replaces the file in the working directory with the corresponding staged file. Modifications made to the file in the working directory are discarded.

## `git checkout "commit SHA-1" -- "filename"`
* **flow: commit -> staging area and working directory.**
Restores the give file from the given commit to the working directory and staging area.

## `git reset "commit SHA-1" -- "filename"`
* **flow: commit -> staging area.**
Replaces or restores the given file to the staging area with the version of the file in the given commit (e.g. HEAD for the latest commit).

## .gitignore file
Files and directories listed in this file are ignored by git commands.

Next: [git branching and merging](./git-branching-and-merging.md)
