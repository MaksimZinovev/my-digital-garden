---
{"dg-publish":true,"permalink":"/git/git-config-global-core-autocrlf-true-crlf-and-lf/"}
---

links:: [[git/git commands most used\|git commands most used]]

# git config --global core.autocrlf true. CRLF and LF

## git config --global core.autocrlf true. CRLF and LF 


Links

- [Git Newline Checking Crlf And Lf - Alibaba Cloud](https://www.alibabacloud.com/tech-news/developer/4l1w5hzp1ii-git-newline-checking-crlf-and-lf#:~:text=CRLF%20is%20a%20two%2Dcharacter,of%20text%20in%20a%20file.)
- [CRLF vs. LF: Normalizing Line Endings in Git | Aleksandr Hovhannisyan](https://www.aleksandrhovhannisyan.com/blog/crlf-vs-lf-normalizing-line-endings-in-git/)

It  appears that LF causes the issue with reading CSV file in TC. File is not read correctly.

What is CRLF and LF?

CRLF stands for Carriage Return Line Feed, and LF stands for Line Feed. CRLF is a two-character sequence used to indicate the end of a line of text in a file. It is represented by the characters CR (carriage return) and LF (line feed). CRLF is used in Windows-based systems, while LF is used in Unix-based systems. In Git, CRLF and LF are used to indicate the end of a line of text in a file.

What is correct settings in GIT on Windows, CRLF or LF?

If you are using Windows, you should set the core.autocrlf option to true.

Check eol git settings. In that example, i/lf means that the file uses lf in the index, and w/crlf means it uses crlf in the working directory.

```bash  

git ls-files --eol

i/lf    w/lf    attr/                   dataStore.csv
i/crlf  w/crlf  attr/                   dataStoreThisWorks.txt
i/none  w/none  attr/                   jobCreated.csv

```

Set  the core.autocrlf option to true:

```bash  

git config --global core.autocrlf true

```

```
core.autocrlf=true = > CRLF

```

View current git settings

```bash  
git config --list

```