---
{"dg-publish":true,"permalink":"/git/git-command-alias/","tags":["git"]}
---

Git provides alias creation for most commonly used commands.

```bash
git add -A && git commit -m "new changes"
```

You can make an alias to this command in the Git using command below. Ensure you use **SINGLE QUOTES**

```bash
git config --global alias.c '!git add -A && git commit -m'
```

This will create a global alias `c` for command `git add -A && git commit -m`. Now you can use the command below

```bash
git c "new changes"
```

You can delete an alias with `git config --global --unset alias.c` or `git config --global --unset-all` command.

![[test1\|test1]]

```bash
git config --get-regexp
{ #alias}

```

```bash
maksim@DESKTOP-RFLIR6R MINGW64 ~/work (master)
$ git config --get-regexp
{ #alias}

alias.c git log --oneline add -A && git commit -m
```

---
Link to original note: [[git/git commands most used\|git commands most used]]