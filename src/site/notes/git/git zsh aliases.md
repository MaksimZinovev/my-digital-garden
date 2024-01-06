---
{"dg-publish":true,"permalink":"/git/git-zsh-aliases/"}
---

links:: [[git/git commands most used\|git commands most used]]

# git zsh aliases

## git zsh aliases

The commands below will be available after enabling "alias" plugin in zsh shell.

- `acs`: show all aliases by group

- `acs -h/--help`: print help mesa

- `acs <keyword(s)>`: filter and highlight aliases by `<keyword>`

- `acs -g <group>/--group <group>`: show only aliases for group `<group>`. Multiple uses of the flag show all groups

- `acs --groups`: show only group names

```bash


history = omz_history

[cd]

- = cd -
1 = cd -1
2 = cd -2
3 = cd -3
4 = cd -4

[git]

gss = git status --short
gco = git checkout
gst = git status
glo = git log --oneline --decorate
gl = git pull
gp = git push
ga = git add
gb = git branch
gcb = git checkout -b
gm = git merge
gca = git commit --verbose --all
gcount = git shortlog --summary --numbered
gpsup='git push --set-upstream origin $(git_current_branch)'
ggpull = git pull origin "$(git_current_branch)
ggpush = git push origin "$(git_current_branch)
ggsup = git branch --set-upstream-to=origin/$(git_current_branch)
glgg = git log --graph
glgga = git log --graph --decorate --all
glgm = git log --graph --max-count=10
glgp = git log --stat --patch
gma = git merge --abort
gcm = git checkout $(git_main_branch)

alias gcm="git  commit -m"
alias gcof="git checkout -f"
alias reshh="git reset --hard HEAD"
### reset local repository branch to be like remote branch
alias reshu="git reset --hard @{u}"
alias aa="git add -A"
alias editconfig="!git config --global -e"
alias save= !git add -A && git commit -m SAVEPOINT
### Resets the index but not the working tree (i.e., the changed files are preserved but not marked  for commit)
alias unsave="git reset HEAD~1 --mixed"
### alias amend= commit -a --amend
### alias wipe= !git add -A && git commit -qm 'WIPE SAVEPOINT' && git reset HEAD~1 --hard



[ls]
l = ls -lah
la = ls -lAh
ll = ls -lh
ls = ls --color=tty
lsa = ls -lah
```