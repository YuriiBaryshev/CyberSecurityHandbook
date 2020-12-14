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

##### Add file/directory
Adds files in the to the staging area for Git. Before a file is available to commit to a repository, the file needs to be added to the Git index (staging area). There are a few different ways to use git add, by adding entire directories, specific files, or all unstaged files.
```
Usage:
git add <file or directory name>
```
Example:
To add all files not staged:
$ git add .
```
To stage a specific file:
$ git add index.html
```
To stage an entire directory:
$ git add css
