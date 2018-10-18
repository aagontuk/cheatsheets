## Introduction ##

**Version Control System:** Version control is a system that records changes to a file or set of files over time. Each change of those files can be tracked easily. So its is possible to revert back to a previous version etc.

**Git:** Git is a command line program for distributed version controlling

**GitHub:** GitHub is a web-based Git repository hosting service. It offers all the distributed version control and software management functionality of Git. It makes it easy to save project remotely, version controlling, collaborate with multiple developers on a project etc.

## Configuring Git ##

**Configure Name & Email:** First we have to add name and email. If no name or email is added pc's username will be used as username and host name will be used as email. This username and email is for your local repository and have no relation with remote repository's(like github) username and email.

```
me@my-pc:~$ git config --global user.name 'name'
me@my-pc:~$ git config --global user.email 'me@example.com'
```

**Configure color:** Configure git so that terminal output becomes color coded.

`git config --global color.ui 'auto'`

## Creating & Publishing Repository ##

#### Creating Local Repository ####
---

**Creating repository:** To make a local repository first create a folder where all other files & folder of this project will be saved. I am creating a project called ***cheatsheets*** where I will store all my cheatsheets. So first I will create a directory named **cheatsheets**.

`me@my-pc:~$ mkdir cheatsheets`

**initializing:** Now I have to go to in my newly created directory & do `git init` command to initialize git. This will create a hidden folder *.git*, where git will store all its information about this project for tracking.

```
me@my-pc:~$ cd cheatsheets
me@my-pc:~/cheatsheets$ git init
```

Now I will add files of my project to this directory. Lets say I have created a file called *git_and_github.md* which is my cheatsheet about git & github.

`me@my-pc:~/cheatsheets$ ls`
`git_and_github.md`

**Checking status:** `git status` command gives the current status of the local repository.

`me@my-pc:~/cheatsheets$ git status`
```
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	git_and_github.md

nothing added to commit but untracked files present (use "git add" to track)
```
**Add to staging area:** So its saying there is an untracked file. After adding contents to my files I have to add the files to staging area using `git add` command, So that git can track those files & their contents. Now I am adding *git_and_github.md* file to staging area.

`me@my-pc:~/cheatsheets$ git add git_and_github.md`

Now `git status` gives:

`me@my-pc:~/cheatsheets$ git status`
```
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   git_and_github.md
```

**Commiting:** To add the files into main repository we have to use `git commit` command. A commit message with `-m` option will have to add with this. Now each time we change project's files we have to use this command to add those changes into main repository. Commit message can be anything you want. Usually it is used for specifying what has been added or changed in a specific version of a file. It will also your github commit message when we will upload our local repository to remote github repository.

`me@my-pc:~/cheatsheets$ git commit git_and_github.md -m "Commit Message"`
```
[master (root-commit) f779fa4] Commit Message
 1 file changed, 63 insertions(+)
 create mode 100644 git_and_github.md
```

**Updating changes:** After modifying a file, changes will have to send into staging area issuing `git add` again. And commit changes to repository using `git commit`. Adding & commiting can be done in a single command issuing `git commit -a`.

`me@my-pc:~/cheatsheets$ git commit -a -m "updated content"`
```
[master 318a1c2] updated content
 1 file changed, 53 insertions(+), 5 deletions(-)
```

**Summary:**

| Command | Description |
| ------- | ----------- |
| git init | initialize a local git repository |
| git status | See current status of a git repository |
| git add | Adding files to staging area |
| git commit | Commit changes to repository |
#### Publishing Local Repository ####
---

Now I will publish my local repository to a remote repository like GitHub.

**Setup GitHub:** Create GitHub accout. [Set up ssh](https://help.github.com/articles/generating-ssh-keys/) (optional) etc.

**Creating a remote repository:** Now I have to create a repository in GitHub which will be the remote repository for my local repository. My local repository will be synced in this remote repository. Repositories can be public or private.

I am creating a repository named *cheatsheets* in GitHub. The repository URL of github are in this form *github.com/USERNAME/REPOSITORYNAME.git*. So my newly created repository's URL will be: https://github.com/rashfaqur/cheatsheets.git. For SSH it will be *git@github:USERNAME/REPOSITORYNAME.git*. In my case it is *git@github.com:rashfaqur/cheatsheets.git*

*Note:* If you want to use SSH you have to use SSH type URL for SSH to work.

**Adding remote repository into local repository:** Now I have to add my remote repository URL / address using `git remote add URL_ALIAS URL` command, so that my local repository can know my remote repository. Were URL is my remote repository's URL and URL_ALIAS is a sudo name for remote repository URL so that I don't have to type URL in future. URL_ALIAS can be any name. Commonly  *origin* is used. I am using *origin* & SSH URL.

`me@my-pc:~/cheatsheets$ git remote add origin git@github.com:rashfaqur/cheatsheets.git`

This will have to do only once.

**Pushing local repository:** `git push -u URL_ALIAS BRANCH_NAME` command is used to push / publish local repository into remote Repositorie. Where BRANCH_NAME is the branch name. Main branch is called *master*. There can be several branch. I will add my porject into *master* branch.

`me@my-pc:~/cheatsheets$ git push -u origin master`
```
Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 1.24 KiB | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:rashfaqur/cheatsheets.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
```

Next time after commiting changes I can only issue `git push` to push all the changes into remote repository.

## Branches ##
---

### Creating a new branch ###

* Show current branches
```sh
me@mypc:~/cheatsheets$ git branch
```

* Create a new branch with name feature
```sh
me@mypc:~/cheatsheets$ git branch feature
```

* Active / Checkout new branch
```sh
me@mypc:~/cheatsheets$ git checkout feature
```
