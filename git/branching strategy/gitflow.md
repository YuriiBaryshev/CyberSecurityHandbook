# Gitflow strategy

---

## Getting start

Gitflow is just abstract idea of Git workflow. 
Gitflow just dictate how to set up branches and how to merge them.

To start using Gitflow we can install git-flow toolset: 

- Windows


    In git packages for windows after 2.5.3 version it extension 
    is already installed


- OSX
    
    
    To install extension you should exicute this command:

    brew install git-flow

- Linux


    To install extension you should exicute this command:

    sudo apt-get install git-flow
    

After installing of git-flow we can use it as a wrapper over the git.
Also, if you don't need any helpers we can use default git commands.

## Main idea

### Main and develop branches

Gitflow workflow uses two branches to record history of the project.

The main branch store official release history

The develop branch store history of develop project

Example:
    
    $ git flow init


    Initialized empty Git repository in ~/project/.git/
    No branches exist yet. Base branches must be created now.
    Branch name for production releases: [main]
    Branch name for "next release" development: [develop]


    How to name your supporting branch prefixes?
    Feature branches? [feature/]
    Release branches? [release/]
    Hotfix branches? [hotfix/]
    Support branches? [support/]
    Version tag prefix? []


    $ git branch
    develop
    main

![alt text](https://wac-cdn.atlassian.com/dam/jcr:a13c18d6-94f3-4fc4-84fb-2b8f1b2fd339/01%20How%20it%20works.svg?cdnVersion=555 "git flow")

### Feature branches 

Every new feature should have own branch.

Feature branch created from develop 

When feature finished we just merge it back to develop

Example:

    /start
    git checkout develop
    git checkout -b feature_branch

    /finish
    git checkout develop
    git merge feature_branch


Example with git-flow extension:

    /start
    git flow feature start feature_branch
    
    /finish
    git flow feature finish feature_branch


![alt text](https://wac-cdn.atlassian.com/dam/jcr:34c86360-8dea-4be4-92f7-6597d4d5bfae/02%20Feature%20branches.svg?cdnVersion=555 "git flow")

### Release branches

Creating this branch starts the next release cycle, so no new features can be added after this point—only bug fixes, 
documentation generation, and other release-oriented tasks should go in this branch.

To start release branch we fork it from develop branch.

After this we can only do release-oriented tasks.

And when we did all necessary tasks release branch gets merged into main and tagged with version number.  

In addition, it should be merged back into develop branch. 

Example:
    
    /start
    git checkout develop
    git checkout -b release/0.1.0

    /finish
    git checkout main
    git merge release/0.1.0

Example with git-flow extension:

    /start
    $ git flow release start 0.1.0
    Switched to a new branch 'release/0.1.0'
    
    /finish
    git checkout main
    git flow release finish '0.1.0'


![alt text](https://wac-cdn.atlassian.com/dam/jcr:8f00f1a4-ef2d-498a-a2c6-8020bb97902f/03%20Release%20branches.svg?cdnVersion=555 "git flow")

### Hotfix branches

Main idea of hotfix branches it's to fix issue in main branch.

Hotfix branch are a lot like feature branches except they are based on main instead of develop.

Example: 

    /start
    git checkout main
    git checkout -b gotfix_branch

    /finish
    git checkout main
    git merge hotfix_branch
    git checkout develop
    git merge hotfix_branch
    git branch -D hotfix_branch

Example with git-flow extension:

    /start
    $ git flow hotfix start hotfix_branch


    /finish
    git flow hotfix finish hotfix_branch

![alt text](https://wac-cdn.atlassian.com/dam/jcr:cc0b526e-adb7-4d45-874e-9bcea9898b4a/04%20Hotfix%20branches.svg?cdnVersion=555 "git flow")
