# Git Branching and Merging

## branch
A branch is a reference to a commit (SHA-1 hash). It allows to work in different version of the same file in parallel. The work in a branch is independent of the work in other branches. Later the changes in a branch can be incorporated or merged into other branch(es).

### How it works
A branch represents an independent line of development. Branches serve as an abstraction for the edit/stage/commit process. You can think of them as a way to request a brand new working directory, staging area, and project history. New commits are recorded in the history for the current branch, which results in a fork in the history of the project.

## `master` branch
It is the default branch created by git when a new repository is created.

## HEAD pointer
This is a symbolic pointer that references the current branch. It tells us which branch is checked out.

## `git log --all -decorate --oneline --graph`.
Shows the commit graph in a compact form.

## `git branch`
Lists all branches. Same as `git branch --list`

## `git branch <branch name>`
Creates a new branch. The branches will be instantiated where the HEAD pointer is pointing to. This does not checkout the new branch.

## `git branch -d <branch name>`.
Deletes the given branch, but only if it doesn't have un-merged changes.

## `git branch -D <branch name>`.
Forces delete the given branch, even if it hasn't been merged.

## `git branch -m <branch name>`
Renames the current branch to <branch name>.

## `git branch -a`
Lists all remote branches.

## `git branch --merged`.
Shows which branches are merged.

## `git branch -vv`
Shows local branches and their remote tracking branches. It also shows the hash code and commit message of the latest commit. It also tells you if the remote branch has been deleted.

## `git checkout <branch name>`
Changes the current branch to the given branch. HEAD now will point to this branch.

## `git checkout -b <branch name>`
Changes the current branch to the give branch, and creates it if it doesn't exists.

## `git checkout <commit>`
Checks out the given commit hash, if this commit does not have a branch associated with it, then we get a `detached HEAD` warning. In this state we can make experimental changes and commit them without affecting any other branch.

## `git switch -c <new-branch-name>`
Creates a branch pointing to the current checkout commit, and points HEAD to this newly created branch.

## `git diff <branch name 1>..<branch name 2>`.
Shows differences between the given branches.

## `git merge <branch name>`
Merges changes in <branch name> into the current branch (the checked out one).

### There are two merging strategies:
* **Fast forward merge**: When there is a direct path between the current branch and the branch to be merged, git just move both the current branch and the HEAD to point to the commit pointed by the branch to be merged.

* **Three-way merge**: When there is no direct path between the current branch and the branch to be merged, git does a simple three-way merge, using the two snapshots pointed to by the branch tips and the common ancestor of the two. Git creates a new snapshot that results from this three-way merge and automatically creates a new commit that points to it. This is referred to as the merge commit.

## `git stash [-m "message"]`
Save the changes in the current working directory in a stack of stashes.

## `git stash list`
Lists saved stashes in the stack.

## `git stash apply [label]`
Applies latest or labeled stash (if given) to the current working directory, but keeps the stash on the stack, so it can be reused.

## `git stash pop`
Applies the latest stash and removes it from the stack.

Prev: [git basics](./git-basics.md)
Next: [git remotes](./git-remotes.md)
