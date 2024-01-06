---
{"dg-publish":true,"permalink":"/git/git-create-new-alias/"}
---

links:: [[git/git commands most used\|git commands most used]]

# Git create new alias

## Git create new alias

```bash

git config --global alias.c '!git '

```

Now type `alias` to call the above command

```bash
$ git config --global alias.co checkout
$ git config --global alias.br branch
$ git config --global alias.ci commit
$ git config --global alias.st status
$ git config --global alias.pu pull
$ git config --global alias.ma 'merge --abort'
$ git config --global alias.me merge

### View last command
git config --global alias.last 'log -1 HEAD'
```

Now type `git co` to call the above command