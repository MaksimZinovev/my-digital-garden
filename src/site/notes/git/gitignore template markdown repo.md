---
{"dg-publish":true,"permalink":"/git/gitignore-template-markdown-repo/","tags":["git"]}
---


```.gitignore
#.gitignore
# Ignore everything recursively
*


# Don't ignore .gitignore
!.gitignore


# Now exclude markdown and txt files
!**.md
!**/*.md

!**.txt
!**/*.txt

# Don't ignore  excluded files
# even if they are in subdirectories
!*/


# Now you can push to remote repo to have a backup of all your md files on GitHub.
# You can also write script for crontab to sync regularly
```
