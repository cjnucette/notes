# Advanced git

## Move a commit to a different branch (if it is the last commit)

* Checkout the branch where you want to move the commit to.

`git checkout <branchname>`

* Copy the commit to the current branch.

`git cherry-pick <commit>`

* Go to the branch where the commit was copied from.

`git checkout <copied commit branchname>`

* Reset the commit history to the commit before the copied commit.

`git reset --hard HEAD~1`

## Recover a deleted commit using `reflog`

* run `reflog` this will show a journal of the movement of the HEAD pointer.

`git reflog`

* Copy the \<commit\> number you want to restore.
* Create a new branch using based on the copied commit.

`git checkout <new branchname> <commit>`

## Interactive Rebase.
Use this in your own feature branch. **Do not do this on pushed commit**.

1. How far back do you want to go? What should be the "base" commit?
2. Start the interactive rebase session with: `git rebase -i <parent base commit>` to select the parent of the commit you want to change.
3. The editor opens up. In here only determine which "actions" you want to perform. Don't change commit data in this step, yet!. **Note**: commits are in "reverse" order or the order in which they will be reapplied.

### Examples

#### Editing old commit messages.

1. Select the parent commit: `git rebase -i HEAD~3`.
2. An editor window opens up with the list of commit to be affected. Also there is a list of possible action options.
3. Replace the word "pick" that appears before the commit you want to change the message with "reword" option and save.
4. Then another editor window opens up with the selected commit. In this window change the message and save.
5. All commits are reapplied including the changed one.

#### Adding a change to an old commit

1. Add the changes (files) to the next commit: `git add <filename>`
2. When committing the changes you need to provide the `--fixup` option and the commit to be fixed: `git commit --fixup <commit to be fixed>`
4. Now that we created a `fixup` commit, we run the interactive rebase remembering to select the one before or parent of the one we want to _fix_ with the option `--autosquash`: `git rebase -i --autosquash <parent commit>`
5. A new editor window opens up with the commit to be affected preceded by the word `fixup`. In here everything has been done, so the only you should do is to save the file.
6. All the commits are reapplied and the new commit is integrated with the commit to be fixed.

For other cases: [First Aid Kit for Git](https://www.bit.ly/git-first-aid-kit)
