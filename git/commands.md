# Git commands

[Repository manipulation](#repository-manipulation)

### Repository manipulation

##### Create repository

To create repository You should choose the folder and run

```
git init
```

from the command line at the folder.

After running the command respective git's technical files would be created.

##### Settings
Before starting work, you need to make some settings:

```

git config --global user.name "Your Name" # specify the name with which the commits will be signed
git config --global user.email "e@w.com"  # specify the email that will be in the committer's description
```

##### Adding changes to the index
```
git add .        # add to the index all new, changed, deleted files from the current directory and its subdirectories
git add text.txt # add a file to the index (has been changed, has been deleted, or is it a new file)
git add -i       # launch an interactive shell to add only the selected files to the index
git add -p       # show new/changed files one by one with their changes and a question about tracking/indexing
```

##### Removing changes from the index
```

git reset            # remove from the index all changes added to it (in the working directory all changes will be saved), the antipode of git add
git reset readme.txt # remove changes to the specified file from the index (changes in the working directory will be saved)
git reset --hard @~      # move HEAD (and branch) to the previous commit, make the working directory and index the same as they were at the time of the previous commit
git reset --hard 75e2d51 # move HEAD (and branch) to the commit with the specified hash, make the working directory and index the same as they were at the time of the specified commit
git reset --soft @~      # move HEAD (and branch) to the previous commit, but leave all changes in the working directory and index
git reset --soft @~2     # same, but move HEAD (and branch) two commits backward
git reset @~             # move HEAD (and branch) to the previous commit, leave the working directory as it is, and set the index to what it was at the time of the previous commit (more convenient than git reset --soft @~ if you need to re-set the index)
#  Almost like git reset --hard, but safer: no changes in the working directory can be lost
git reset --keep @~      # move HEAD (and branch) to the previous commit, reset the index, but leave changes in the working directory if possible (if the file with changes was changed between commits, there will be an error and the switch will not happen)
```

##### Commits
```
git commit -m "Name of commit"    # commit the indexed changes (commit), add a message
git commit -a -m "Name of commit" # index tracked files (ONLY tracked files, NOT new files) and commit, add a message
```


##### Temporarily switch to another commit
```
git checkout b9533bb # switch to a commit with the specified hash (move HEAD to the specified commit, return the working directory to the state at the time of that commit)
git checkout master  # switch to the commit to which the master points (move HEAD to the commit to which the master points, return the working directory to the state at the time of that commit)
```

##### Switch to another commit and continue work from it
You will need to create a new branch starting with the specified commit.
```
git checkout -b new-branch 1234567   # create a new-branch branch starting with a commit with hash 1234567 (move HEAD to the specified commit, return the working directory to the state it was at the time of that commit, create a pointer to that commit (branch) with the specified name)
```

##### Restoring changes
```
git checkout 1234567 index.html  # restore the specified file in the working directory at the time of the specified commit (and add this change to the index) (git reset index.html to remove from the index, but keep the changes in the file)
```

##### Copying commits (transferring commits)
```
git cherry-pick 1234567          # copy the changes from the specified commit to the active branch, commit those changes
git cherry-pick master~2..master # copy the changes from the master (the last 2 commits) to the active branch
git cherry-pick -n 1234567       # copy the changes from the specified commit to the active branch, but DO NOT commit (assuming that we will commit the changes ourselves later)
git cherry-pick master..feature  # copy to the active branch the changes from all the commits of the feature branch since it diverged from the master (similar to a branch merge, but this is copying changes, not merging), commit those changes; this may cause a conflict
git cherry-pick --abort    # interrupt the conflicting transfer of commits
git cherry-pick --continue # continue conflict transfer of commits (will only work after the conflict has been resolved)
```

##### Deleting a file
```
git rm text.txt    # delete the tracked unmodified file and index this change
git rm -f text.txt # delete the tracked changed file and index the change
git rm -r log/     # delete all the contents of the tracked directory log/ and index this change
git rm ind*        # delete all tracked files with a name beginning with "ind" in the current directory and index this change
git rm --cached readme.txt # remove the indexed file from the tracked files (FILE STAYS ON) (often used for files that were accidentally added to the tracked files)
```

##### Moving/renaming files
There is no renaming for git. Renaming is treated as deleting the old file and creating a new one. The fact of renaming can only be determined after indexing the change.
```
git mv text.txt test_new.txt # Rename the file "text.txt" to "test_new.txt" and index this change
git mv readme_new.md folder/ # move the readme_new.md file to the folder/ directory (must exist) and index this change
```

##### Clone repository
To clone repository You should choose the folder and run from the command line at the folder.
```
git clone https://github.com/YuriiBaryshev/CyberSecurityHandbook.git            # clone the remote repository into the directory of the same name
git clone https://github.com/YuriiBaryshev/CyberSecurityHandbook.git FolderName # clone the remote repository to the "FolderName" directory
git clone https://github.com/YuriiBaryshev/CyberSecurityHandbook.git .          # clone the repository to the current directory
```

After running the command a new directory with the name of cloned repository will be created. This command also creates remote-tracking branches for each branch in the cloned repository and creates and checks out an initial branch that is forked from the cloned repository’s currently active branch.

##### Create/delete branch

To create branch You should run

```
git branch <name_branch>
git branch vadim
```

from the command line at the folder.

If You want to delete branch, You should run

```
git branch -D <name_branch>
```

##### Switch branches or restore working tree
To switch branch you should run 
```
git checkout [<branch>]
``` 
from the command line at the folder.

After running the command you will see the name of the branch you switched to at the end of the path.

##### Revert changed
To revert changes You should use command git reset

To hard reset files to HEAD on Git, use the “git reset” command with the “–hard” option and specify the HEAD.

The “–hard” option is used in order to reset the files of the index (or the staging area) and of the working directory.

The "HEAD" is the hash of commit you want go to.
```
git reset --hard HEAD~2
```
going back two commits before HEAD     
```
git reset --hard 1234567
```
going back to commit 1234567

All commits that have already been committed to a remote repository must be cancelled with a new commit (git revert) to avoid problems with the development history of other contributors.
```
git revert HEAD --no-edit    # create a new commit that cancels changes to the last commit without starting the message editor
git revert b9533bb --no-edit # same, but the changes made by the commit with the specified hash (b9533bb) are undone
```

```
git commit --amend -m "Name"  # "re-commit" changes from the last commit, replace it with a new commit with a different message (move the current branch one commit back, keeping the working directory and index "as is", create a new commit with data from the "canceled" commit, but with a new message)
```

```
git checkout text.txt      # DANGER: undo changes in the file, return the file state existing in the index
git clean -df              # Delete untraceable files and directories
```
