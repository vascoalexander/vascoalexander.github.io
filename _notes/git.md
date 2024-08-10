---
category: cheatsheets
mermaid: true
---

| Command                                        | Short Description                                        |
| ---------------------------------------------- | -------------------------------------------------------- |
| git init                                       | # Initialize repository                                  |
| git clone <repo_url>                           | # Clone repository                                       |
| git status                                     | # View repository status                                 |
| git add \<file\>                                 | # Stage changes of <file>                                |
| git add .                                      | # Stage all changes                                      |
| git reset \<file\>                               | # Unstage a file while retaining other changes           |
| git rm \<file\>                                  | # Delete file and stage the removal                      |
| git commit -m "message"                        | # Commit Changes                                         |
| git branch                                     | # List branches                                          |
| git branch \<branch\>                            | # Create branch                                          |
| git checkout \<branch\>                          | # Switch to branch                                       |
| git merge \<branch\>                             | # Merge branch                                           |
| git remote -v                                  | # View remotes                                           |
| git pull origin \<branch\>                       | # Pull changes                                           |
| git push origin \<branch\>                       | # Push changes                                           |
| git log                                        | # View commit history                                    |
| git log --oneline                              | # View short commit history                              |
| <br>git log --oneline --decorate --graph --all | # View commit history with graphical layout (q to quit)  |
| git revert \<commit\>                            | # Revert commit                                          |
| git reset \<commit\>                             | # Reset to commit                                        |
| git reset --hard \<commit\>                      | # Clear staging area, rewrite working tree from [commit] |
| git diff                                       | # Diff of what is changed but not staged                 |
| git diff --staged                              | # diff of what is staged but not committed               |
| git tag                                        | # List tags                                              |
| git config --global user.name "name"           | # Set global username                                    |
| git config --global user.email "email"         | # Set global email                                       |

#### THE STAGING AREA

1. **Working Directory**: The working directory is where you make edits and create new files. It represents the current state of your project.
2. **Staging Area**: Once you've made changes in your working directory that you wish to save, you first add these changes to the staging area. This area captures a snapshot of the modifications and prepares them for committing.
3. **Repository**: When you're ready to finalize your changes, you commit the modifications from the staging area. This action saves a permanent snapshot of the changes in your Git repository, along with metadata such as who made the changes and when.


{% include img.html source="staging.svg" alt="staging" class="center img-sm" %}

```bash
git add <file>    # adds changes in a file to the staging area
git add .         # adds all changes to the staging area
git diff          # shows unstaged changes in the working directory
git dif --staged  # shows changes that are staged for the next commit
git commit        # commits the staged changes
git reset <file>  # removes file from the staging area
```

#### UNSTAGE (Reverse) A FILE / ALL FILES

```bash
git restore --staged <file-path>   # unstage specified file
git restore --staged .             # unstage all files
```

#### DISCARD LOCAL UNCOMMITTED CHANGES

```bash
git restore .            # discard all uncommitted changes
git restore path/to/file # discard changes to specified file
git checkout -- .        # revert working directory to last commit
```

#### GIT PULL vs GIT FETCH

git fetch is used to download updates from a remote repository to your local repository without merging or modifying your local branches. This command allows you to review the changes before integrating them into your local branch.

```bash
git fetch <remote>
```

git pull is a combination of git fetch and git merge. It downloads changes and merges them into the current branch.

```bash
git pull <remote> <branch>
```

#### GIT RESET --soft

When you use git reset --soft, Git moves the **HEAD** pointer to the specified commit while leaving the staging area and working directory unchanged. This means that all changes from commits after the specified one will remain in the staging area, ready to be recommitted.

```bash
git reset --soft HEAD~1
```

This command moves the HEAD pointer one commit back. Changes made in the latest commit are transferred to the staging area:

{% include img.html source="soft-reset.svg" class="center" alt="reset-soft" %}

#### GIT RESET --mixed

Resets the HEAD pointer to the specified commit. Adjusts the staging area to match this commit while leaving the working directory unchanged. Changes made after the specified commit will remain in the working directory but will be left unstaged.

#### GIT RESET --hard

The git reset --hard option can be thought of as a nuclear option. It moves the HEAD pointer to the specified commit, updates the staging area to match this commit, and also adjusts the working directory to exactly match the commit. Any changes from commits made after the specified commit will be completely discarded.

#### GIT REBASE

Rebasing effectively saves the changes in your current branch, temporarily “removes” the commits you’ve made on your branch, applies the new commits from the other branch, and then reapplies your changes one commit at a time on top of these.

It’s important to note that rebasing rewrites commit history by generating new commits for each original commit. This process can result in a cleaner and more understandable project history.

{% include img.html source="git-rebase.svg" class="center img-xl" alt="git-rebase" %}

Above Situation:
git checkout feature
git rebase main

After the rebase the Feature branch includes the commits from main and keeps the commits that have been commited earlier to the feature branch. The main branch is untouched, but the commitment history has changed.

If a conflict arises, Git will show you which files are conflicting. You’ll have to open these files, resolve the conflicts, and then continue the rebase like so:

```bash
# After resolving conflicts
git add .
git rebase --continue
```

If you want to abort the rebase for any reason, you can do so with the following command:

```bash
git rebase --abort
```

#### GIT MERGE

Once your feature is ready and tested, you’ll want to merge it back into the main project. First, switch back to the branch you want to merge your changes into. Assuming you want to merge your changes to main branch:

```bash
git checkout master
```

Then, merge your feature branch:

```bash
git merge <feature-branch>
```

After merging your changes locally, push them to the remote repository to make them available to your teammate and update the live version of the website:

```bash
git push origin master
```

#### ADDING EMPTY DIRECTORIES TO REPOSITORY

Create a placeholder file named .gitkeep in the empty directory. The **.gitkeep** file has no special meaning to Git, but it’s a widely-accepted convention that signals the intention to keep the directory in the repository.

```
echo "" .gitkeep                                    # create .gitkeep file
git add .gitkeep                                    # stage the file
git commit -m "add empty directory with .gitkeep"   # commit the changes
```

#### REMOVE DIRECTORY FROM REPOSITORY

```bash
git rm -r <directory> # removes a dir from git repository recursively
```

#### CHANGE REMOTE REPOSITORY URL

```bash
git remote -v                        # verify current remote repository
git remote set-url origin <new-url>  # set new url of origin
git remote -v                        # verify new remote repository url
git fetch origin                     # sync local repository to new remote
```

[tecadmin.net - terms of service](https://tecadmin.net/term-of-services/)  

#### ADDITIONAL RESOURCES

[GitHub Documentation](https://docs.github.com/en)  
[GitHub Skills](https://skills.github.com/ )  
[Git Visualization](https://git-school.github.io/visualizing-git/)  
[Generate gitignore fiel online](https://www.toptal.com/developers/gitignore)   
*Note: In VS Code there is an extension for this*  

**Sources:**  

[https://tecadmin.net/git-staging-area-explained/)](https://tecadmin.net/git-staging-area-explained/)  
[https://tecadmin.net/reversing-git-add-before-commit/](https://tecadmin.net/reversing-git-add-before-commit/)  
[https://tecadmin.net/git-discard-uncommitted-changes/](https://tecadmin.net/git-discard-uncommitted-changes/)  
[https://tecadmin.net/difference-between-git-pull-and-git-fetch/](https://tecadmin.net/difference-between-git-pull-and-git-fetch/)  
[https://tecadmin.net/difference-between-git-reset-soft-mixed-and-hard/](https://tecadmin.net/difference-between-git-reset-soft-mixed-and-hard/)  
[https://tecadmin.net/git-rebase/](https://tecadmin.net/git-rebase/)  
[https://tecadmin.net/git-branches-create-list-switch-merge-push-delete/](https://tecadmin.net/git-branches-create-list-switch-merge-push-delete/)  
[https://tecadmin.net/adding-empty-directories-in-your-git-repository/](https://tecadmin.net/adding-empty-directories-in-your-git-repository/)  

