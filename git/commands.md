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

##### Cloning a repository
```
git clone https://github.com/YuriiBaryshev/CyberSecurityHandbook.git            # clone the remote repository into the directory of the same name
git clone https://github.com/YuriiBaryshev/CyberSecurityHandbook.git FolderName # clone the remote repository to the "FolderName" directory
git clone https://github.com/YuriiBaryshev/CyberSecurityHandbook.git .          # clone the repository to the current directory
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
```

##### Undoing changes
```
git checkout text.txt      # DANGER: undo changes in the file, return the file state existing in the index
git reset --hard           # DANGER: undo changes; return what is in the commit to which HEAD points (uncommitted changes are removed from the index and from the working directory, untraceable files will remain in place)
git clean -df              # Delete untraceable files and directories
```

##### Commits
```
git commit -m "Name of commit"    # commit the indexed changes (commit), add a message
git commit -a -m "Name of commit" # index tracked files (ONLY tracked files, NOT new files) and commit, add a message
```