# FAQs about git



### Merging my local changes with another branch
This can be done directly in the standard merge process. You should save the ```merge``` history using the ```--no-ff flag```, which means no fast forward.

Go to the branch where the changes will be poured in, make sure it is up to date and start the process:
```git merge <otherbranch> --no-ff```

Then a message appears saying ```merge X into Y branch```, after which you can safely start your merge.

### Cancel a commit before the changes are published
If you have made a commit that you later need to edit or completely erase, the git ```reset``` command helps.
```
git reset HEAD~1 # cancel the last commit, save changes
```
```
git reset --hard HEAD~1 # cancel the last commit, erase changes
```
Be careful using the second option as changes to your local files will be lost.
To save the commit message, type:
```
git commit -i ORIG_HEAD
```

### Restoring a deleted branch
You can use ```git reflog``` to get the hash (SHA1) of the last commit in a remote branch. Copy that hash and use it in the command:
```
git checkout <sha>
```
After that you can restore the deleted branch with this command:
```
git checkout -b <branch name>
```

### Display commits containing deleted files
To find out which commits contain deleted files, use the command:
```
git log --diff-filter=D --summary
```
It will show a list of commits in which files were deleted.

### Synchronize the branch with the master repository
To synchronize recent changes in the master repository (or with any other branch you have been working with), you need to "rebase" the local branch. Suppose you are working on the ```foobar``` branch:
```
git checkout foobar
```
And then you "relocate":
```
git rebase master
```
After that, the ```origin``` commits from the master will be applied. Once the conflicts have been resolved, the process can be continued with the ```git rebase --continue``` command. Now you can continue working on your branch or merge it into the master repository.

### Restoring a deleted file
If you accidentally delete a file, you can quickly restore it:
```
git checkout myfile.txt
```
If you want to recover a file from a specific time point in the commit history, find out the hash of the needed commit and run the command:
```
git checkout $commit~1 myfile.txt
```

### Undo local file changes
The easiest way to get rid of unwanted changes to files and folders is to restore the state of the last commit. This can be done with a special command:
```
git checkout myfile.txt
```
It is also possible to restore a specific file path:
```
git checkout -- path-to-file
```

### Clearing all hidden states
You can clear all hidden states with the following command:
```
git stash clear
```

### Deleting untraceable files and folders
To delete untraceable files and folders from the working copy, type the following command:
```
git clean -f
```
To basically remove them:
```
git clean -fd
```
Tip: To see which files are redundant, before deleting them directly, type:
```
git clean -n
```

### Changing a commit message before sending it
You can change the commit message with the ```git commit --amend``` command, which will open an editor where you can make the necessary corrections to the last message.

The message can also be changed directly with the command
```
git commit --amend -m "New message"
```

### Sort commits by author
To display a list of commits filtered by author, use the following command:
```
git log --author="Author Name"
```

### Search for a specific message in all commits
To find the specific text of a commit message that matches a regular expression, use the command
```
git log --grep <query>
```

### Changing a commit message after it has been sent
In this case, the process takes two steps. First, you will have to modify the message with ```git commit --amend``` and then rewrite the local branch commit history: ```git push <remote> <branch> --force```

Warning: such a forced overwriting can lead to loss of commits from an external branch if it has not been synchronized for a long time, so be careful.

### Combine two or more commits
Here we need to perform an interactive rebase. If you are rebasing relative to the master branch, you should start with ```git rebase -i master```. However, if the rebase is not relative to a branch, you will need to rebase relative to ```HEAD```

If you need to combine the last two commits, you can use the
```
git rebase -i HEAD~2
```

After it is entered, instructions for selecting commits will appear. If you want to combine all commits with the first oldest commit, write ```pick``` on the first line and change the letter to ```f``` for all other commits. 

### Deleting a file from git while keeping its local copy
To remove a file from git but save it locally, use the following command:
```
git rm --cached myfile.txt
```

### Viewing an old revision of a file
It is possible to view the contents of a file at a specific point in time in the past. To do this you need to use the command:
```
git show commitHash:myfile.txt
```

### Matching commits for a specific function to be added to a release branch
If you decide to combine and publish commits, a new commit will appear in the release branch, so the history of a particular feature branch will remain unchanged.

Below is an example of how to achieve this effect:
```
git fetch origin
git checkout [release-branch]
git rebase origin/[release-branch]
git merge —squash —no-commit [feature-branch]
git commit -m 'Merge X into Y'
```
In the end, only one commit will remain in the release branch, and the history of changes in the development branch of a particular feature will remain untouched.

### Rolling back to a specific commit in history
If you are not too worried about changes in the local repository, you can "roll back" to a particular commit in the history by using the command:
```
git reset --hard HEAD~1
```
This command will set ```HEAD``` on a particular commit. You can also use a commit hash.

### Stop tracking existing files
If you want to stop tracking files that are already in the repository but still want to keep it local, commit changes and run the command:
```
git rm -r --cached
```
It will remove the modified files from the staging area. Then run the command:
```
git add
```
and commit the changes.

### Restore a deleted tag
If you need to restore a tag that was accidentally deleted, you can start by searching for it:
```
git fsck --unreachable | grep tag
```
Once the desired tag is found, it should be restored:
```
git update-ref refs/tags/tag-name
```

### Creating a new branch with changes to the current branch
A common situation is when users start modifying files in a branch to fix something, only to remember later that they didn't create a new branch beforehand. Fortunately, there is a way to do this already in the process:
```
git checkout -b new-branch-name
```
This command moves the files from the current branch to a new one, which you can then commit.

### Publishing a local branch for remote editing
If you have created a local branch and you want other users to be able to work with it, use the command:
```
git push -u origin new-branch-name
```

### Restoration of accumulated changes
If user changes are in stack mode, you can apply them to the branch with the ```git stash apply``` command. You can also run ```git diff```, which will help you identify differences. In order to then get rid of the accumulated data, you need to run the command:
```
git stash drop
```
If there is more than one accumulation, you can use the command to find the right one:
```
git stash list
```
and then you can apply it using its index:
```
git stash@{1}
```
Note that the indices are counted from zero.

### Renaming a local and remote branch
Suppose you have a branch "fix-bug25" which you want to rename to "hotfix-users". First of all, you will need to change the local branch:
```
git branch -m fix-bug25 hotfix-users
```
And then the deleted branch: it cannot be renamed directly, so you will have to delete it and then re-publish it with a new name. Before proceeding with these procedures, make sure that no team member is working on the branch! Deleting a branch:
```
git push origin :fix-bug25
```
And now we republish it with a new name:```git push origin hotfix-users```

### Cancelling a commit after sending it to the master repository
Consider the procedure for returning one or more commits that you want to erase from a deleted branch. You can identify a particular commit by its hash:
```
git revert b712c3c
```
Only the commit that is second to the last commit is canceled:
```
git revert HEAD^
```
A simple cancellation of the last commit:
```
git revert -n HEAD
```

### Remove a file from the buffer
To remove a file added by mistake from the buffer, use a simple command:
```
git reset HEAD unlovedfile.txt
```

### Commit to the wrong branch
You need to switch to a new branch that you forgot to create beforehand:
```
git checkout -b new-branch-name
```
And then switch to the original branch:
```
git checkout original-branch-name
```
...and roll back to the last commit you want to save.
To do this, you can use the ```git log``` command and save the hash (SHA1) of the last commit you want to keep. For example, this is ```a31a45c```

Now you need to reset it: ```git reset --hard a31a45c``` and submit the result.

Warning: Make sure no one sends commits to the original branch during the above procedures, otherwise these changes will be lost!

### Removing an external branch
If you want to delete a branch, enter the command:
```
git push origin --delete branch-name
```

### Resetting a local branch to remote state
In case there are no changes to be saved, you can reset the local branch to the remote state with two simple commands.
First of all, you need to get fresh updates from the deleted branch:
```
git fetch deleted-branch-name
```
And then you need to tell git that the local branch should be rolled back to the remote state:
```
git reset --hard origin/local-branch-name
```
If you have a commit to save, you must create a new branch and commit before resetting:
```
git branch new-branch-name
git commit -m "Update"
```

### Displays the number of commits from each participant
Want to know how many commits each team member has made?
This command outputs a list, sorted in descending order of the number of commits: 
```
git shortlog -s -n
```

### Display all commits of the same file
If you want to see all commits with changes to a particular file, use the ```git log --follow -p -- myfile```

The ```--follow``` argument allows you to output all changes over the file, even if it was renamed in the process.

If ```-p``` is omitted, the system outputs only commit messages, but not their contents.

### Using command aliases on the command line
Tired of typing in ```git status``` every time? You can assign a simple alias to this command, which is easier and faster to type into git.
```
git config --global alias.st status
```

- now you only need to write ```git st```

You can go further and assign aliases to more complex commands:
```
git config --global alias.logme 'log -p --author=Dmytro'
```
The ```git logme``` alias will now output all of our commits.

### Mark a conflicting file as resolved
To mark one or more conflicting files as resolved so that you can modify them normally, use the command:
```
git add filename
```
You can then run ```git commit``` to resolve conflicts and publish the changes.

### View all unsent commits
To view all commits that have not yet been submitted to the appropriate branches, use the following command:
```
git log --branches --not --remotes
```
In addition, you can use:
```
git log origin/master..HEAD
```

### Renaming a tag
To rename an existing tag:
```
git tag new-title-tag old-title-tag
git tag -d old-title-tag
git push origin :refs/tags/old-tag-title
git push --tags
```

### Removing old branches deleted from an external repository
If a branch is removed from an external repository, it can also be erased from the local repository by using the command ```git-remote prune remote-branch-name```.
It will remove an old branch called name-deleted-brand that has already been wiped from the external repository, but is still available locally in ```remotes/remote-branch-title```

### Updating a specific submodule
To update a specific submodule in the repository, you need to add the path to the submodule:
```
git submodule update --remote --merge <path>
```

### Preparing deleted files
To prepare files and folders that were deleted locally for the commit, you can use a special command:
```
git add -u
```
If you want to prepare only the path currently in use, use the:
```
git add -u
```