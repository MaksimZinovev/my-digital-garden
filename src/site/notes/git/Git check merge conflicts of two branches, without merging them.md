---
{"dg-publish":true,"permalink":"/git/git-check-merge-conflicts-of-two-branches-without-merging-them/"}
---

links:: [[git/git commands most used\|git commands most used]]

# Git check merge conflicts of two branches, without merging them

## Git check merge conflicts of two branches, without merging them?

Suppose you are on the master branch and you would like to test if the dev branch can be merged without conflict into the master.

```bash
### In the master branch
git merge dev --no-ff --no-commit
```

```
 git merge b2c-dashboard-enrolled --no-ff --no-commit

### No conflicts 

Automatic merge went well; stopped before committing as requested

```

To return in a normal situation, just abort the merge:

```bash

git merge --abort
```