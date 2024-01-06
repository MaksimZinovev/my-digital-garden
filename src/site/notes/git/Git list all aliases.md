---
{"dg-publish":true,"permalink":"/git/git-list-all-aliases/"}
---

links:: [[git/git commands most used\|git commands most used]]

# Git list all aliases

## Git list all aliases

```bash

git config --global alias.alias "! git config --get-regexp
{ #alias}
\. | sed -e s/^alias\.// -e s/\ /\ =\ /"

```

This will create a permanent git alias named alias which gets stored in your ~/.gitconfig file. Using it will list all of your git aliases, in nearly the same format as they are in the ~/.gitconfig file. To use it, type:

```bash
git alias
```