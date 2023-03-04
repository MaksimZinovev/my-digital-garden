---
{"dg-publish":true,"permalink":"/git/how-to-create-a-new-git-repository/","tags":["git"]}
---

Links: [[github MOC\|github MOC]], [[git/git MOC\|git MOC]]
<br ><br >

# How To Create A New Git Repository


![Image of How to Create a New Git Repository | Start a Github Repo](https://initialcommit.com/img/initialcommit/git-create-repository.png "How to Create a New Git Repository | Start a Github Repo")

## Table of Contents

-   [Introduction](https://initialcommit.com/blog/git-create-repository#introduction)
-   [What is a Git Repository?](https://initialcommit.com/blog/git-create-repository#what-is-a-git-repository)
-   [What is git init?](https://initialcommit.com/blog/git-create-repository#what-is-git-init)
-   [Connecting your Local Repo to GitHub](https://initialcommit.com/blog/git-create-repository#connecting-your-local-repo-to-github)
-   [Cloning an Existing Repository: git clone](https://initialcommit.com/blog/git-create-repository#cloning-an-existing-repository-git-clone)
-   [Configuration & Set Up: git config](https://initialcommit.com/blog/git-create-repository#configuration--set-up-git-config)
-   [Saving Changes to the Repository: git add and git commit](https://initialcommit.com/blog/git-create-repository#saving-changes-to-the-repository-git-add-and-git-commit)
-   [Repo-to-repo collaboration: git push](https://initialcommit.com/blog/git-create-repository#repo-to-repo-collaboration-git-push)
-   [Bare vs Non-Bare Git Repository](https://initialcommit.com/blog/git-create-repository#bare-vs-non-bare-git-repository)
-   [Summary](https://initialcommit.com/blog/git-create-repository#summary)
-   [Next Steps](https://initialcommit.com/blog/git-create-repository#next-steps)
-   [References](https://initialcommit.com/blog/git-create-repository#references)

## Introduction

Git is by far the most popular [distributed version control system (DVCS)](https://initialcommit.com/blog/Technical-Guide-VCS-Internals), which allows us to track changes to files over time and collaborate with other developers. Git is an extremely powerful tool for software development for everyone from large software dev teams working on enterprise projects to solo programmers working on their local filesystem.

After installing Git, the first thing you must do is create a Git repository. In this article, you will learn how to create a new Git repository, configure it, and commit changes to it.

## What is a Git Repository?

A Git repository is a collection of files and folders that represent the history of changes made to your codebase. This is incredibly useful for development teams since it allows developers to maintain a single view of the project codebase, backup the entire history of a project, easily retrieve older versions of the whole codebase or individual files, debug code, look up the author of a specific change, and much more.

Developers can create a new repository for a new empty project, clone an existing repository and continue development on it, or create a new repository for an existing project that hasn't been tracked using version control yet.

## What is git init?

The `git init` command is used to initialize a new Git repository in the project root directory of your codebase. If you a starting a brand new project, this might be a new empty folder, or it might contain a simple README. To create a new folder for your project you can use the mkdir command on the command-line:

```
$ mkdir <project-root>
```

Next browse into it and run the git init command:

```
$ cd <project-root>
$ git init
Initialized empty Git repository in /path/to/project/root/.git/
```

The message `Initialized empty Git repository in /path/to/project/root/.git/` indicates that you successfully initialized a new Git repo!

If you have an existing project, your project root probably already contains some code files and subdirectories. In that case skip the \`mkdir\` step and simply browse into the folder and run the \`git init\` command as indicated above.

The `git init` command performs a one-time setup to initialize a Git repository. This creates a new empty shell of a Git repository. The result is that Git creates a hidden subfolder called `.git/` in the project root folder. The `.git/` directory contains all the data and configuration that Git uses to track the history of your code changes.

As you work with Git in your project, the Git commands that you run will interact with the contents of the `.git/` folder automatically. If you'd like you can browse into it using `cd .git/` and take a peek around to familiarize yourself with the contents. But as a beginner, it's not advisable to manually change anything in the `.git/` folder yourself.

If you'd like to initialize a Git repo in a specific folder instead of the current directory, simply include it as a parameter after the git init command:

```
git init path/to/project/root
```

Where `path/to/project/root` is the location you want to initialize the repository (and create the `.git/` folder). If the directory name is not specified, Git assumes the current directory is where you want to initialize the repository.

Here is the full sequence of commands needed to create a project root folder and initialize a new Git repo inside it:

```
$ mkdir project_folder
$ cd project_folder 
$ git init
Initialized empty Git repository in /path/to/project_folder/.git/
$ ls -a 
....git
```

In this example, we created the new folder `project_folder` to contain our codebase, changed the current directory to `project_folder` and ran git init. This gives us a success message, and we used the `ls -a` command to confirm that the hidden `.git/` folder was created.

## Connecting your Local Repo to GitHub

To connect your local repository to GitHub, you have to first go to [https://github.com](https://github.com/). Then you can complete these steps:

1.  Log In to your GitHub account. Create a new account if you don't have one.
2.  Navigate to your repositories page, and click the "New" button, which will take you to the "Create a new Repository" page.
3.  Then type a name for your repo.
4.  Select Public or Private. Public repositories can be viewed by anyone on the internet, while Private repositories can only be viewed by you and people you share access to the repository with.
5.  Finally you can click "Create Repository"

There is also an option to add a README file, which will initialize the README directly in GitHub. But, since you are connecting your local repo to GitHub you can skip this step.

After, you click "Create Repository" GitHub will redirect to a page, which will show you the commands for creating a new repo or pushing an existing repo from the command line. So you can quickly get to work on your project.

You can connect your local repository to your GitHub repository using the `git remote add` command which will map your remote repository by HTTPS/URL to the default name `origin`:

```
git remote add origin https://github.com/[github_username]/example-project.git
git branch -M main
```

The command git branch -M main is often used to rename the default "master" branch to "main", but note you must have at made at least 1 commit in your repo for this to work.

Now you have successfully connected your local repo to GitHub!

## Cloning an Existing Repository: git clone

If the project you want to work with already has a Git repo associated with it on GitHub or some other version control hosting site, you don't need to run git init for your existing project.

Instead, you can clone an existing remote Git repository with the `git clone` command. Git clone essentially copies and downloads a remote Git repo to a folder on your local machine. You can use the either the HTTPS or SSH network protocol to clone a repo. Let's look at an example:

```
$ git clone https://github.com/githubtraining/hellogitworld.git
Cloning into 'hellogitworld'...
remote: Enumerating objects: ..., done.
remote: Counting objects: 100% (x/x), done.
remote: Compressing objects: 100% (y/y), done.
remote: Total z (delta z), reused z (delta z), pack-reused z
Receiving objects: 100% (z/z), n MiB | n MiB/s, done.
Resolving deltas: 100% (z/z), done.

$ ls
hellogitworld/
```

Here, we clone a public Git repository called `hellogitworld` from the HTTPS URL `https://github.com/githubtraining/hellogitworld.git`. This create a directory on your filesystem called `hellogitworld` and will download the latest version of the remote repo files including the hidden `.git/` directory containing all Git's internal information.

You can get a full history of the commits within the repository by using the [git log](https://initialcommit.com/blog/Git-Cheat-Sheet-Beginner) command.

## Configuration & Set Up: git config

After creating a new local Git repo or cloning one down from a remote, you'll want to use the `git config` command to configure some default Git settings such as your name and email address. These will be associated with each commit you make in your Git repository.

The [git config](https://initialcommit.com/blog/git-config) command can be operated at three different scope levels:

1.  \--local: Local scope is configuration for the current repository, which is stored in the file `path/to/project/root/.git/config`
2.  \--global: Global scope is configuration for the user, applies across repositories for the operating system user. This configuration is stored in the user's home directory `~/.gitconfig`
3.  \--system: System configuration is configuration for the entire system, for every user on the computer, in the /etc/gitconfig file.

It is common to set your Git username globally using the command:

```
git config --global user.name <name>
```

You can set your Git email address locally (in case you need a specific email address for different repos) using the command:

```
git config --local user.email <email>
```

You can set your Git text editor at the system level using the command:

```
git config --system core.editor <editor>
```

Another common early task in your Git repo is to create a `README.md` file describing your project's purpose and usage. This is displayed on the GitHub page of your repository.

It is also good practice to great a [.gitignore](https://git-scm.com/docs/gitignore) file, which contains a list of files or types of files you don't want Git to track.

## Saving Changes to the Repository: git add and git commit

Now that you have created a configured your Git repo, you're ready to make your [first commit](https://initialcommit.com/blog/What-Is-An-Initial-Commit-In-Git). You can think of a commit as a set of changes that you're ready to save to your Git repository.

The set of files and folders that you see in your project structure at any given time are referred to as Git's working directory or working tree. This is the revision of the codebase that is currently checked out for you to work on.

You can save changes to your repository using the `git add` and `git commit` commands. The [git add](https://initialcommit.com/blog/git-add) command adds file changes from the working directory to Git's staging area. You can think of the staging area (or staging index as it's also called) as a temporary place your changes are stored before being committed to the repo.

The git commit command saves the changes built up in the staging area as a commit in your local Git repository. You can think of this as a new revision or changeset being saved. The `git add` and `git commit` command are used in sequence, as follows:

```
> touch README.md
> git add README.md
> git commit -m "Initial Commit"
```

In the example, we create a `README.md` file, add it to the staging area using the syntax `git add <filename>`. Then we commit the change with the `-m` flag along with a descriptive [commit message](https://initialcommit.com/blog/git-commit-messages-best-practices) "Initial Commit". Once changes have been committed, they can be viewed in Git's log with the `git log` command.

## Repo-to-repo collaboration: git push

After making one or more commits to your local repository, you often want to share your changes with your team as well as remotely back up your work. You can push commits made in your local repo to the remote repo using the `git push` command. The remote repository doesn't necessarily have to be a GitHub repository, it can be hosted anywhere, even in a different folder on your local machine, or a friend's repo on their server.

The syntax for git push is:

```
git push <remote> <branch>
```

Here we push changes in the specified [Git branch](https://initialcommit.com/blog/git-branches) to the specified remote repository. For our example, we can push the first commit we made to our remote repo using the command:

```
git push -u origin main
```

This will push any new commits on the local branch `main` to the remote repository `origin`.

Remember that "origin" is the Git's reference to the default remote repository.

## Bare vs Non-Bare Git Repository

A bare Git repository is one that doesn't have a working directory. That means a files from the codebase can't be checked out and worked on in a bare repo. Since there is no working directory in a bare repo, files can't be viewed, edited, or deleted by users. Bare repositories simply contain the contents of the `.git/` directory, which includes all of the data needed to reconstruct any revision of the project's codebase. Bare repo directories can be quickly identified because they typically end in a `.git` extension.

You can create a bare Git repo using the `--bare` option with the git init command:

```
$ git init --bare
```

Bare repositories are most commonly used as remote repos hosted on platforms such as GitHub. When multiple developers are collaborating on a project, they often need a central repository where the commit history of their codebase is stored. Any repo you create on GitHub is a bare repo, and you might have noticed that the URL you use with the git clone command ends in a directory with the .git extension.

A non-bare Git repository is the default when initializing a new repo, which includes project files in the working directory and the .git folder. Developers can code directly in this repository since it has a working tree.

## Summary

In this article, you learned how to [create a new Git repository](https://docs.github.com/en/get-started/quickstart/create-a-repo) in a few different scenarios and connect your local repo to a remote repo on GitHub.

You started by learning what a Git repository is. Second, you saw how to initialize a Git repo with git init or use git clone to copy an existing remote repo to your local machine.

Next, you learned various ways to configure your Git repository by using the git config command, creating a README.md file, and creating a .gitignore file. You continued by learning to save changes using the git add and git commit commands.

Finally, you learned how to push change to the default Git remote and the difference between a bare and non-bare git repository.

## Next Steps

If you're interested in learning more about how Git works under the hood, check out our [Baby Git Guidebook for Developers](https://initialcommit.com/store/baby-git-guidebook-for-developers), which dives into Git's code in an accessible way. We wrote it for curious developers to learn how Git works **at the code level**. To do this we documented the first version of Git's code and discuss it in detail.

We hope you enjoyed this post! Feel free to shoot me an email at [jacob@initialcommit.io](mailto:jacob@initialcommit.io) with any questions or comments.

## References

1.  Git Ignore, Git SCM - https://git-scm.com/docs/gitignore
2.  Create a Repo, GitHub Documentation - https://docs.github.com/en/get-started/quickstart/create-a-repo

## Final Notes
<br ><br >


