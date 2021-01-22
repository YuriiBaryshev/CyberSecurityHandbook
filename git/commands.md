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

##### Create/delete branch

To create branch You should run

```
git branch <name_branch>
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
git reset --hard 7a9ad7f
```
going back to commit 7a9ad7f
