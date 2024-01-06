---
{"dg-publish":true,"permalink":"/git/git-merge-another-branch-into-mine/"}
---

links:: [[git/git commands most used\|git commands most used]]

# git merge another branch into mine

## git merge another branch into mine

Let's say you are currently working on branch feature/feature_a and you want to merge the changes made in another branch called feature/feature_b to feature/feature_a. The following commands should do the trick:

```bash

git checkout feature/feature_b
git pull
git checkout feature/feature_a
git merge feature/feature_b

```