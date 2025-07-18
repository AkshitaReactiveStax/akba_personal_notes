

how to push a new project on a already created branch in git??


To push a new project to an already created branch in Git, follow these steps:

  

**Step 1: Initialize Git in Your New Project**

Navigate to your project’s root directory and initialize Git if it is not already initialized:

```
git init
```

  
This creates a .git directory to manage your project as a Git repository.

  

**Step 2: Link to the Remote Repository**

Add the remote repository URL if it’s not already set:

```
git remote add origin <REMOTE_REPOSITORY_URL>
```

  

You can find the repository URL from the Git hosting service (e.g., GitHub, GitLab, Bitbucket).

  
To confirm the remote is added correctly:

```
git remote -v
```

  

**Step 3: Fetch the Remote Branch**

  Fetch the branch you want to push your project to:

```
git fetch origin <BRANCH_NAME>
```

  

**Step 4: Switch to the Target Branch**

Check out the branch to make it your working branch:


```
git checkout <BRANCH_NAME>
```


If the branch doesn’t exist locally but exists in the remote, you can create a tracking branch:


```
git checkout -b <BRANCH_NAME> origin/<BRANCH_NAME>
```

  

**Step 5: Stage and Commit Your Project**

  Add all the files in your project to the staging area:


```
git add .
```

  

Then commit your changes:

```
git commit -m "Initial commit for the project"
```

  

**Step 6: Push the Project to the Branch**

Finally, push your project to the remote branch:

```
git push origin <BRANCH_NAME>
```

  

**Common Errors and Fixes**

  

1. **Error:** fatal: remote origin already exists

• If the remote already exists, you don’t need to add it again. Just skip Step 2.

2. **Error:** Updates were rejected because the tip of your current branch is behind

• Pull the latest changes from the remote branch before pushing:


```
git pull origin <BRANCH_NAME> --rebase
```


3. **Error: Authentication Issues**

• Ensure you have the correct credentials or SSH keys configured.

This process will push your new project to the existing branch in your remote repository.




or 
go to the location where you want to clone your project locally 
and then 
run command 
git clone https://github.com/FullStackLabsCa/boca-spring-boot-app.git



1. **Create the Branch** (if it doesn’t exist):

If the branch doesn’t exist, you can create it and push it:

git checkout -b boutique_project_monolith_v1
git push -u origin boutique_project_monolith_v1



### Git Commands

The following table shows the most commonly used Git Commands:

| S. No | Command Name                                  | Use                                                                                                                                              |
| ----- | --------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| 1     | git init                                      | Initialise a local Git Repository                                                                                                                |
| 2     | git add.                                      | Add one or more files to the staging area                                                                                                        |
| 3     | git commit -m “Commit Message”                | Commit changes to the head but not to the remote repository.                                                                                     |
| 4     | git status                                    | Check the status of your current repository and list the files you have changed.                                                                 |
| 5     | git log                                       | Provides a list of all commits made on a branch                                                                                                  |
| 6     | git diff                                      | View the changes you have made to the file                                                                                                       |
| 7     | git push origin <branch name>                 | Push the branch to the remote repository so that others can use it.                                                                              |
| 8     | git config --global user.name “Name”          | Tell Git who you are by configuring the author name                                                                                              |
| 9     | git config --global user.email user@email.com | Tell Git who you are by configuring the author email id.                                                                                         |
| 10    | git clone <repository_name>                   | Creates a Git repository copy from a remote source                                                                                               |
| 11    | git remote add origin <server>                | Connect your local repository to the remote server and add the server to be able to push it.                                                     |
| 12    | git branch <branch_name>                      | Create a new branch                                                                                                                              |
| 13    | git checkout <branch_name>                    | Switch from one branch to another                                                                                                                |
| 14    | git merge <branch_name>                       | Merge the branch into the active branch                                                                                                          |
| 15    | git rebase                                    | Reapply commits on top of another base tip                                                                                                       |
| 16    | git checkout -b <branch_name>                 | Creates a new branch and switch to it                                                                                                            |
| 17    | git stash                                     | Stash changes into a dirty working directory                                                                                                     |
| 18    | git pull                                      | Update local repository to the newest commit                                                                                                     |
| 19    | git revert <commit_id>                        | Revert commit changes                                                                                                                            |
| 20    | git clean -n                                  | Shows which files would be removed from working directory. Use the -f flag in place of the -n flag to execute the clean.                         |
| 21    | git log --summary                             | View changes (detailed)                                                                                                                          |
| 22    | git diff HEAD                                 | Show difference between working directory and last commit.                                                                                       |
| 23    | git log --oneline                             | View changes (briefly)                                                                                                                           |
| 24    | git reflog                                    | Show a log of changes to the local repository’s HEAD. Add --relative-date flag to show date info or --all to show all refs.                      |
| 25    | git rebase -i <base>                          | Interactively rebase current branch onto <base>. Launches editor to enter commands for how each commit will be transferred to the new base.      |
| 26    | git restore --staged <file_name>              | Resetting a staged file                                                                                                                          |
| 27    | git rm -r [File_name]                         | Remove a file (or folder)                                                                                                                        |
| 28    | git config --list                             | List all variables set in config file, along with their values                                                                                   |
| 29    | git branch -d <local_branch>                  | Delete local branch in Git                                                                                                                       |
| 30    | git push -d <remote_name> <branch_name>       | Delete remote branch in Git                                                                                                                      |
| 31    | git stash pop                                 | Unstash the changes                                                                                                                              |
| 32    | git commit -am                                | The -am along with the command is to write the commit message on the command line for already staged files.                                      |
| 33    | git commit -ammend                            | The amend is used to edit the last commit. Incase we need to change the last committed message, this command can be used.                        |
| 34    | git rm                                        | The git rm command is used to remove or delete files from working tree and index.                                                                |
| 35    | git pull --rebase                             | Git rebase is used to rewrite commits from one branch to another branch.                                                                         |
| 36    | git merge --squash                            | The squash along with git merge produces the working tree. It indexes in the same way as that of the real merge, but discards the merge history. |
| 37    | git revert -e <commit_id>                     | edit the commit mesage before reverting, -e is used for the same.                                                                                |
| 38    | git bisect                                    | Git bisect goes through all the previous commit and uses binary search to find the bugged commit.                                                |
| 39    | git blame                                     | git blame is used to know who/which commit is responsible for the lastest changes in the repository.                                             |
| 40    | git cherry-pick                               | Choosing a commit from one branch and applying it to another is known as cherry picking in Git.                                                  |