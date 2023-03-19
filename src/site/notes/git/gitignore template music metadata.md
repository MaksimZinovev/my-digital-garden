---
{"dg-publish":true,"permalink":"/git/gitignore-template-music-metadata/","tags":["git"],"created":"","updated":""}
---


```txt
#.gitignore
# Ignore everything recursively
*


# Don't ignore .gitignore
!.gitignore


# Track  markdown and txt files
!**.md
!**/*.md


!**.txt
!**/*.txt


# Track  metadata files
!**/._*
!._*

```
