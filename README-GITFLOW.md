### GIT FLOW INSTALLATION
1. OSX - Homwbrew
    `$ brew install git-flow-avh`
2. OSX - Macports
    `$ ports install git-flow-avh`
3. Linux
    `$ apt-get install git-flow`
4. Windows (Cygwin)
    `$ wget -q -O - --no-check-certificate https://github.com/nvie/gitflow/raw/develop/contrib/gitflow-installer.sh | bash`

### IMPORTANT BRANCHES in GIT FLOW
1. `develop` or `qa` => this the base branch for development, it contains the stable code ready to release
2. `release` => this is the temporary branch created when we start release and will be deleted automatically when release done
3. `master` => this branch contains 

### GIT FLOW USAGE
1. Available subcommands are:
   `init`      Initialize a new git repo with support for the branching model.
   `feature`   Manage your feature branches.
   `bugfix`    Manage your bugfix branches.
   `release`   Manage your release branches.
   `hotfix`    Manage your hotfix branches.
   `support`   Manage your support branches.
   `version`   Shows version information.
   `config`    Manage your git-flow configuration.
   `log`       Show log deviating from base branch.

2. Init Git flow configurations
    - Go to the local folder of Git repository and run this command: `git flow init`
    - Then, setting the configs following these steps (re-enter the name inside `[]` or use your own name, but should follow the convention of your team/company):
        
        Branch name for production releases: [main] => enter `master`
        Branch name for "next release" development: [develop] => enter `qa` (following the rule of Carro)

        How to name your supporting branch prefixes?
        Feature branches? [feature/] => enter `feature/` or any names for prefix of feature branches
        Bugfix branches? [bugfix/] => enter `bugfix/` or any names for prefix of bugfix branches
        Release branches? [release/] => enter `bugfix/` or any names for prefix of bugfix branches
        Hotfix branches? [hotfix/] => enter `hotfix/` or any names for prefix of hotfix branches
        Support branches? [support/] => enter `hotfix/` or any names for prefix of support branches => but it
        Version tag prefix? [] => enter the tag prefix used to create a git tag

3. Working with feature branch
    3.1. Creating a feature branch
    - Without the git-flow extensions:
        `git checkout qa`
        `git checkout -b feature/<feature_branch_name>`
    - When using the git-flow extensions:
        `git flow feature start <feature_branch_name>` => this command will run automatically 2 commands above, create the feature branch with prefix `feature/` from `qa` branch
    
    3.2.  Push/Publish a feature branch
        `git flow feature start` command just create local branch, you need to push it to remote server
    - Without the git-flow extensions:
            `git push feature/<feature_branch_name>`
    - When using the git-flow extensions:
        `git flow feature publish <feature_branch_name>`

    3.3.  Finish a feature
    - Without the git-flow extensions:
        `git checkout qa`
        `git merge feature/<feature_branch_name>`
        `git branch -d feature/<feature_branch_name>`
    - When using the git-flow extensions:
        `git flow feature finish <feature_branch_name>` => this command will run automatically 3 commands above, merge feature branch into `qa` and delete automatically feature branch.
    - But following our flow, all code need to create the PRs to review first, so we don't care about `finish` command

    3.4. Get a feature published by another user
        `git flow feature pull origin <feature_branch_name>`

    3.5. Track a feature on origin by using
        `git flow feature track <feature_branch_name>`
    
4. Working with bugfix branch => The same with feature branch
5. Working with hotfix branch
    5.1. Creating a hotfix branch
    - Without the git-flow extensions:
        `git checkout master`
        `git checkout -b hotfix/<hotfix_branch_name>`
    - When using the git-flow extensions:
        `git flow hotfix start <hotfix_branch_name>` => this command will run automatically 2 commands above, create the hotfix branch with prefix `hotfix/` from `master` branch
    
    5.2.  Push/Publish a hotfix branch
    - Without the git-flow extensions:
        `git push hotfix/<hotfix_branch_name>`
    - When using the git-flow extensions:
        `git flow hotfix publish <hotfix_branch_name>`

    5.3.  Finish a feature
    - Without the git-flow extensions:
        `git checkout master`
        `git merge hotfix/<hotfix_branch_name>`
        `git checkout qa`
        `git merge hotfix/<hotfix_branch_name>`
        `git branch -d hotfix/<hotfix_branch_name>`
    - When using the git-flow extensions:
        `git flow hotfix finish <feature_branch_name>` => this command will run automatically 4 commands above, and then delete hotfix branch automatically.
    - If you need to do code review by PR, don't care about the finish command

6. Working with release branch
    The release branch is the temporary branch created when we do the release production
    
    6.1. Start a release
    - Without the git-flow extensions:
        `git checkout qa`
        `git checkout -b release/0.1.0`
    - When using the git-flow extensions:
        `git flow release start 0.1.0`
        => now local is switched to a new branch 'release/0.1.0'
    6.2. Finish a release branch
    - Without the git-flow extensions:
        `git checkout master`
        `git merge release/0.1.0`
        `git tag 0.1.0`
        `git branch -d release/0.1.0`
    - With the git-flow extension:
        `git flow release finish '0.1.0'`


### References
https://www.atlassian.com/git/tutorials/comparing-workflows/gitflow-workflow
http://danielkummer.github.io/git-flow-cheatsheet



