---
{"dg-publish":true,"permalink":"/git/git-force-pull/","tags":["git"]}
---


<br ><br >

# Git Force Pull
- Solution
	- get rid of  local changes and reset it to origin master
	```bash
	git fetch origin master
	git reset --hard origin/master
	
	```
	- if you want to get rid of untracked files, you can use the following git command:
	```
	git clean -f -d
	
	```
- Links
	- [Git Pull Force to Overwrite Local Changes - Right Way](https://itsyndicate.org/blog/how-to-use-git-force-pull-properly/)

<br ><br >


