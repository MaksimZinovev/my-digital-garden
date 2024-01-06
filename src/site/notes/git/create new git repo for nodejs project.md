---
{"dg-publish":true,"permalink":"/git/create-new-git-repo-for-nodejs-project/","tags":["git"]}
---


Links: [[git/git MOC\|git MOC]]

<br ><br >

# Create New Git Repo For Nodejs Project

links: [[sample gitignore nodejs project\|sample gitignore nodejs project]], [How to Create a New Git Repository | Start a Github Repo](https://initialcommit.com/blog/git-create-repository)

```Shell
mkdir project
git init 
touch .gitignore
# add patterns to gitignore file
git add. 
git commit -m "initial commit"
git ls-tree -r master --name-only

# create repo in github
git remote add origin URL
git branch -M main
git push -uf origin main


```

> The command `git branch -M main` is often used to rename the default "master" branch to "main", but note you must have at made at least 1 commit in your repo for this to work

## Check Existing Remote URL

```bash
git remote -v
```

## Change Existing Remote URL

```Shell
# Remove the existing remote URL
git remote remove origin

# Add the new remote URL
git remote add origin {{new_remote_url}}
```
