---
{"dg-publish":true,"permalink":"/git/remove-add-add-new-git-remote-replace-remote-with-new-url/","tags":["git","github"]}
---


<br ><br >

# Remove Add Add New Git Remote Replace Remote With New Url


```bash
~/repos/p4-python-aerofiler  master ✔                                                                                                    0m
▶ gpf!
remote: Repository not found.
fatal: repository 'https://github.com/MaksimZinovev/aerofiler-pytest/' not found

~/repos/p4-python-aerofiler  master ✔                                                                                                   0m  ⍉
▶ git remote add origin https://github.com/MaksimZinovev/p4-aerofiler
fatal: remote origin already exists.

~/repos/p4-python-aerofiler  master ✔                                                                                                   5m  ⍉
▶ git remote -v
origin	https://github.com/MaksimZinovev/aerofiler-pytest (fetch)
origin	https://github.com/MaksimZinovev/aerofiler-pytest (push)

~/repos/p4-python-aerofiler  master ✔                                                                                                    6m
▶ git remove https://github.com/MaksimZinovev/aerofiler-pytest
git: 'remove' is not a git command. See 'git --help'.

The most similar command is
	remote

~/repos/p4-python-aerofiler  master ✔                                                                                                   7m  ⍉
▶ git remote remove https://github.com/MaksimZinovev/aerofiler-pytest
fatal: No such remote: 'https://github.com/MaksimZinovev/aerofiler-pytest'

~/repos/p4-python-aerofiler  master ✔                                                                                                   7m  ⍉
▶ git remote remove origin

~/repos/p4-python-aerofiler  master ✔                                                                                                    8m
▶ git remote -v

~/repos/p4-python-aerofiler  master ✔                                                                                                    8m
▶ git remote add origin https://github.com/MaksimZinovev/p4-aerofiler

~/repos/p4-python-aerofiler  master ✔                                                                                                    8m
▶ gpf!
fatal: The current branch master has no upstream branch.
To push the current branch and set the remote as upstream, use

    git push --set-upstream origin master


~/repos/p4-python-aerofiler  master ✔                                                                                                   8m  ⍉
▶ git push --set-upstream origin master
Enumerating objects: 791, done.
Counting objects: 100% (791/791), done.
Delta compression using up to 4 threads
Compressing objects: 100% (760/760), done.
Writing objects: 100% (791/791), 5.95 MiB | 1.64 MiB/s, done.
Total 791 (delta 416), reused 0 (delta 0)
remote: Resolving deltas: 100% (416/416), done.
To https://github.com/MaksimZinovev/p4-aerofiler
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.



```

<br ><br >


