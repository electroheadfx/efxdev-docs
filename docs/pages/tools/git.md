# Github Master commands

## Github base

**List the actual Config setup from current directory**

```bash
$ git config -l
```

**Setup the Global Config**

```bash
# Exemple
$ git config --global user.name electroheadfx
$ git config --global user.email "laurent@efxdesign.fr"
```

**Setup the local Config (per project)**

```bash
# Exemple
$ git config user.name efx
$ git config user.email "laurent@electroheadfx.fr"
```

## Setup for mac lf/cr

```bash
git config --global core.autocrlf input
```

## Setup for windows lf/cr

```bash
git config --global core.autocrlf true
```

## Setup for rebase

```bash
git config --global credential.helper store
git config --global pull.rebase true
git config --global merge.ff true
```

## Create a git project

```bash
# Create a folder
$ mkdir folder && cd folder
# init git (when the project is new)
$ git init
# Add origin url from remote
$ git remote add origin https://github.com/electroheadfx/test.git
# Now you can push the code after you will add file then commit
$ git push -u origin master
```

**Add file and commit**

```bash
# add folder, files
$ git add [folders] [file1] [file2]
# or add all from current directory
$ git add .
# commit the added file with a message
$ git commit -m ”msg”
# Push on server to origin from master
$ git push -u origin master
```

**Git status and log**

```bash
# Commit status
$ git status
# See all the commits done
$ git log
# See all the i commits
$ git log -n i
# See All the diff before git add
$ git diff
```

**Revert a file to last comit**

```bash
git checkout file
```

## Git Branches

```bash
# créé une branche au repo
$ git branch myfeature
# see all branchs list
$ git branch
# switch to myfeature branch
$ git checkout myfeature
# see the diff between 2 branch
$ git diff master...myfeature
# Create master branch
$ git branch master
# merge branch my feature on master
$ git merge myfeature
# delete myfeature branch
$ git branch -d myfeature
```

## Get a GIT repository

```bash
# Create a test folder with the repo
$ git clone https://github.com/electroheadfx/test.git
```

**Delete/add a folder and commit**

```bash
# Remove a folder
$ git rm -rf <folder>
# Remove files
$ git rm file1 file2
# Commit with a message
$ git commit -m “msg“
# Push the commit on server to master like origin, after just do git push
$ git push -u origin master
# Add a folder or file
$ git add <folder> file1 file2
# commit again
$ git commit -m “msg“
# Push to the server a new version
$ git push -u origin master
# You can do the shorter version if its always master
$ git push
```

**Push branch commits to github**

```bash
# Setuo origin remote
$ git remote add origin https://github.com/electroheadfx/test.git
$ git push -u origin master
# list the remote
$ git remote -v
# if a problem, you can remove it with:
$ 
```

**Add `gitignore` git commit**

```bash
# Create gitignore
$ touch .gitignore
# Edit it in vs code for add files to ignore
$ code .gitignore
# Add it to repo
$ git add .gitignore
# Commit it
$ git commit -m "add gitignore"
```

### **Update Your repo**

> There 2 ways to do it :

```bash
# 1- In old day we get the repo with fetch and merge FETCH_HEAD
$ git fetch https://github.com/electroheadfx/test.git
$ git merge FETCH_HEAD

# 2- Now its easier to pull directely :
$ git pull https://github.com/electroheadfx/test.git
# If there is conflit, fix them in code and does a :
$ git commit -m "update"
```

## **GIT Rebase process**

**Setup to do on the repo before**

```bash
git config --global credential.helper store
git config --global pull.rebase true
git config --global merge.ff true
```

> **Switch on develop :**

```bash
git checkout develop
```

> **Create your own branch**

```bash
git checkout -b feature/name_of_the_feature
```

> **We flat a commit series where `N`is the number of previous commit to squash**

```bash
git rebase -i HEAD~N
```

> **Before to commit, we switch on develop branch and update it:**

```bash
git checkout develop
git pull
```

> **We switch back to feature branch**

```bash
git checkout feature/name_of_the_feature
```

> **we update the branch from develop rebase command :**

```bash
git rebase develop
```

> **`feature/name_of_the_feature` is update, we swich on develop for merge the branch**

```bash
git checkout develop
git merge feature/name_of_the_feature
```

> **Push all on the server**

```bash
git push
```

> **We can destroy the `feature/name_of_the_feature`**

```bash
git branch -D feature/name_of_the_feature
```

## Branch commands

> **Rename a branch (g.g. main to master)**

```bash
git branch -m main master
```

> **Copy a branch (main to dev branch)**

```bash
git branch -c main dev
```

> **Delete branch**

```bash
git branch -d dev
```

## Git Tools - Restore and reset

```bash
git restore <a-file-or-a-folder>

git reset <pathspec>
# is the opposite of :
git add <pathspec>

# equivalent to :
git restore [--source=<tree-ish>] --staged <pathspec>
```

[Git - git-reset Documentation](https://git-scm.com/docs/git-reset)

## Git Tools - Stashing and Cleaning

```bash
git status
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
   modified:   index.html

git stash
git status
# On branch master
nothing to commit, working directory clean

# list stored stashes
git stash list
stash@{0}: WIP on master: 049d078 Create index file
stash@{1}: WIP on master: c264051 Revert "Add file_size"
stash@{2}: WIP on master: 21d80a5 Add number to log

# apply the previous stash
git stash apply
# apply the stash@{2}
git stash apply stash@{2}
# Drop any stash
git stash drop stash@{2}
```

[Git - Stashing and Cleaning](https://git-scm.com/book/en/v2/Git-Tools-Stashing-and-Cleaning)

## Git subtree : Publish a folder to a branch in github

```bash
# for exemple you add dist (static files) to our repo
git add dist && git commit -m "Initial dist subtree commit"
# Push dist folder to github gh-pages branch
git subtree push --prefix dist origin gh-pages
# then at each normal push to the main branch, dist is pushed to gh-pages
```

## Git subtree script for gh-deploy

> I create a script called `gh-deploy` for automate the subtree push:

```bash
#!/bin/sh
if [ -z "$1" ]
then
  echo "Which folder do you want to deploy to GitHub Pages?"
  exit 1
fi
git subtree push --prefix $1 origin gh-pages
```

> and use the script in this way:

```bash
git gh-deploy path/to/your/site
```
