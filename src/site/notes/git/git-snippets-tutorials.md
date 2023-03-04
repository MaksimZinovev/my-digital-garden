---
{"dg-publish":true,"permalink":"/git/git-snippets-tutorials/","tags":["git"]}
---



# Links
- [ Become a Git pro in just one blog.](https://medium.com/sysf/become-a-git-pro-in-just-one-blog-a-thorough-guide-to-git-architecture-and-command-line-interface-93fbe9bdb395) 
A thorough guide to Git architecture and command-line interface Become a Git pro in just one blog.

&nbsp;
# Snippets 

## Gitignore template file for syncing only .md files  recursively and ignoring everything else

```shell
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

# Don't ignore 
# ...even if they are in subdirectories
!*/


# Now you can push to remote repo to have a backup of all your md files on GitHub.
# You can also write script for crontab to sync regularly
						
```
links:
- [git - .gitignore exclude folder but include specific subfolder - Stack Overflow](https://stackoverflow.com/questions/5533050/gitignore-exclude-folder-but-include-specific-subfolder)
- [git - Make .gitignore ignore everything except a few files - Stack Overflow](https://stackoverflow.com/questions/987142/make-gitignore-ignore-everything-except-a-few-files)

Here is the result
```
▶ git ls-tree -r master --name-only
.gitignore
folder1/folder3/resources MOC.md
folder1/notes.md
folder2/notes.md

```
