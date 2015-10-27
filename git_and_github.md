## Introduction ##

** Version Control System: ** Version control is a system that record changes to a file or set of files over time. Each change of those files can be tracked easily. So its is possible to revert back to a previous version etc.

** Git: ** Git is a command line program for distributed version controlling

** GitHub: ** GitHub is a web-based Git repository hosting service. It offers all the distributed version control and software management functionality of Git. It makes it easy to save project remotely, version controlling, collaborate with multiple developers on a project etc.

## Creating & Publishing Repository ##

#### Creating Local Repository ####

To make a local repository first create a folder where all other files & folder of this project will be saved. I am creating a project called ***cheatsheets*** where I will store all my cheatsheets. So first I will create a directory named **cheatsheets**.

`me@my-pc:~$ mkdir cheatsheets`

Now I have to go to in my newly created directory & do `git init` command to initialize git. This will create a hidden folder *.git*, where git will store all its information about this project for tracking.

```
me@my-pc:~$ cd cheatsheets
me@my-pc:~/cheatsheets$ git init
```

Now I will add files of my project to this directory. Lets say I have created a file called *git_and_github.md* which is my cheatsheet about git & github.
```
me@my-pc:~/cheatsheets$ ls
git_and_github.md
me@my-pc:~/cheatsheets$
```

`git status` command gives the current status of the local repository.
```
me@my-pc:~/cheatsheets$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	git_and_github.md

nothing added to commit but untracked files present (use "git add" to track)
```
So its saying there is an untracked file. After adding cotents to my files I have to add the files to staging area using `git add` command, So thet git can track those files & their contents. Now I am adding *git_and_github.md* file to staging area.

`me@my-pc:~/cheatsheets$ git add git_and_github.md`

Now `git status` gives:

```
me@my-pc:~/cheatsheets$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   git_and_github.md
```

To add the files into main repository we have to use `git commit` command. A commit message with `-m` option will have to add with this. Now each time we change project's file we have to use this command to add those changes into main repository.
