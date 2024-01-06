---
{"dg-publish":true,"permalink":"/git/git-reset-local-repository-branch-to-be-like-remote-branch/"}
---

links:: [[git/git commands most used\|git commands most used]]

# Git reset local repository branch to be like remote branch

## Git reset local repository branch to be like remote branch

The advantage of specifying @{u} or its verbose form @{upstream} is that the name of the remote repo and branch don't have to be explicitly specified. On Windows or with PowerShell, specify "@{u}" (with double quotes).

```bash
git reset --hard @{u}

```