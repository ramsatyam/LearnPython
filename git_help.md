# Git
Welcome, this guide provide basic information required for using git in your project.
![image](https://i.sstatic.net/XwVzT.png)
```
$ which git
$ git --version
```
# Basic Configuration
```
$ git config --global user.name "username"
$ git config --global user.email "email@gmail.com
$ git config --global push.default "simple"
```
# Clone the central repository
```
$ git clone <source-central-repo> <dest-localrepo>
```
if no folder or path is given, it will create a clone in the current working directory
```
$ echo "firstline" > 1.java
$ git status
$ git add .                   => Complete directory to staging area
$ git add <file name>         => To add a particular file to staging area
$ git commit -m "Comment here with epic or jira or ticket no"
```
# Check status
```
$ git status                   => To check status
$ git show                     => To see the changes done in the file. 
$ git log                      => To get all the commit id's
$ git log -1                   => To check last commit id
$ git log -3                   => To see last 3 commits id's
$ git log --oneline            => give details in one line
$ git log --oneline -1         => Give details in one line for last commit only
```
# Branching
```
$ git branch                       => To see which branch we are working on
$ git branch <new_branch_name>     => To create a branch
$ git checkout < branch_name >     => To navigate to the specific branch     
```
# Merge 
* Merge will merge the change done on the feature branch to the [main branch as a commit.](https://www.freecodecamp.org/news/the-ultimate-guide-to-git-merge-and-git-rebase/)
* Always checkout while residing in the destination branch (in that case there no need to mention the dest_branch.)
* Please read [This article for some difference between Merge Vs Cherrypick Vs Rebase](https://stackoverflow.com/questions/9339429/what-does-cherry-picking-a-commit-with-git-mean)
```
$ git merge <src_branch> <dest_branch>      
```
Selective Merge: Select the required commitID to merge on to destination branch.
```
$ git cherrypick <commit_id>
```
# REBASE
Rebase will re-create the branch, with all the changes in the master branch
# Stash
* If we modified a file while residing in the working directory and have not put the file in staging area.
* Now at this point if you want to take a backup of the changes done to the file and rollback the changes. Then stash will help us do it.
```
$ git stash
$ git stash list            => It will show the backups
  stash@{0}
  stash@{1}
$ git stash apply stash@{1} => To apply the changes again
$ git stash clear           => will delete the stash backups
```
* We cannot do a apply on a modified file ie working directory should be unmodified.
# Git Reset (Before committing)
* If you want to undo the changes from either in 
    * working directory
    * Staging area
    * Head reference in the repo
* with git reset we can only undo the changes, we cannot take the backup.
```
$ git reset --soft      => repository reference
$ git reset --mixed     => repo + staging area
$ git reset --hard      => repo + S.A + W.D  
```
* soft  - will undo the temporary reference ( when we change contents of a file, HEAD internally points a temporary reference)
* mixed - staging files will be unstaged
* hard  - files will be unstages and changes will be rolled backed to previous version.
# Git Revert (After Committing)
To undo the change after doing a commit. In git if the changes are committed we cannot remove a commit.
* Any thing that is stored on a repository will be permanant because git it not storing it as a content but it is storing it as a checksum.
```
$ git revert <commitID>
ex.
$ git revert ea10ad5
$ git log --oneline -3
  bd23a03               => 
  ea10ad5               =>  and made itlatest
  f3da46e
```
we reverted ea10ad5 because we dont want it, So git took previous commit f3da46e and committed again resulting in a new commit id with older changes.
# TAGGING
Git can tag a commit in the repository history so that you find it easier at a later point of time.
* Syntax: `git push <REMOTE-NAME> <TAG-NAME>`
* To push all tags: `git push <REMOTE-NAME> --tags`
```
# Apply a tag
    $ git tag -a <pattern> -m "Comment" < commitID>
# Contents of a tag
    $ git show <pattern>
# Display list of tags
    $ git tag
# Push the tags
    # git push --tags
# Delete a tag
    # git tag -d <tag>
```
# PUSH/PULL to central repos
* Git Push Syntax: `git push <REMOTE-NAME> <BRANCH-NAME>`
* To rename branch name :`git push <REMOTE-NAME> <LOCAL-BRANCH-NAME>:<REMOTE-BRANCH-NAME>`
```
$ git remote add origin "<repository_url.git>"
$ git remote -v             => To check if remote is working or not ( lists the remote reference)

$ git clone <central_repo_url.git>

$ git push origin master    
$ git pull                  => Take commit ids from central repo which are not available in local repository
```
# Ignoring File and Viewing Logs
```
$ echo *.class > .gitignore
$ git commit -m "Adding git ignore"
```
All the file with class extensions will be ignored.
* To delete all the untracked files and runtime files.
```
$ git clean -n
        # will show what files will be deleted
$ git clean -f
        # will remove all untracked files.
```