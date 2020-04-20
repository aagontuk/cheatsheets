# INDEX #

1. [Frequently used git commands](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#frequently-used-git-commands)
    1. [Configuring git](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#configuring-git)
    2. [Initializing a project](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#initializing-a-project)
    3. [Cloning a repository from remote](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#cloning-a-repository-from-remote)
    4. [Showing status of the project](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#showing-status-of-the-project)
    5. [Adding files to staging area](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#adding-files-to-staging-area)
    6. [Inspect changes of a file](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#inspect-changes-of-a-file)
    7. [Commiting](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#commiting)
    8. [Removing files](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#removing-files)
    9. [Moving/Renaming files](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#movingrenaming-files)
    10. [Viewing logs](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#view-logs)
    11. [Modifying last commit](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#modifying-last-commit)
    12. [Removing from staging area](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#removing-files-from-staging-area)
    13. [Unmodifying a modified file](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#unmodifying-a-modified-file)
    14. [Managing remote](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#managing-remote)
    15. [Tagging](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#tagging)
    16. [Aliasing](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#aliasing)

## Frequently Used Git Commands ##

### Configuring Git ###

`git config` is used to create and modify system/user/repo git configuration file.

**Options:**
* *--system* - will set the config system wide. for all user's
all repos in the system. System wide git config file is
stored generally in /etc/gitconfig

* *--global* - will set the config user wide. For a specific user's
all git repos. stored in ~/.config/git/config or user's home directory.

* *--local* - will set the config for a specific repo. Stored in .git/config

* *--list* - Show all the list of current config variables and their values.

**Examples:**

```
git config --global user.name 'aagontuk'
git config --global user.email 'aagontuk@mail.com'
git config --global core.editor vim
git config user.name	# will show value of user.name
```

### Initializing a project ###

`git init` is used to initialize a project as git repository.

```
git init
```

### Cloning a repository from remote ###

`git clone` is used for cloning a remote repository into local system.

```
git clone https://github.com/aagontuk/cheatsheets mycheatsheets
```

### Showing status of the project ###

`git status` is used to see status of the project files. Untracked/tracked/modified/staged.

```
git status	# Show details status
git status -s	# Show brief status
```

### Adding files to staging area ###

`git add` is used to add untracked/modified files to staging area and prepare for commit.
If a directory is added, its contents will be added recursively.

```
git add README.md
```

### Inspect changes of a file ###

`git diff` is used to show changes of a file

```
git diff		# Shows changes between last staged and unstaged
git diff --staged	# Shows changes between the last commit and staged
git diff COMMIT_HASH~ COMMIT_HASH   # Show diff between last commit and its ancestor
```

### Commiting ###

`git commit` is used for commiting changes that are staged

```
git commit			        # To commit changes that are staged.
git commit -m "COMMIT_MSG"	# Commit with inline commit message.
git commit -a			    # stage all tracked modified files and commit.
git commit -v			    # will add diff of changes in the commit message.
```

### Removing files ###

`git rm` is used to remove files.

Following command will remove a file from tracking and also remove from system(HDD).
```
git rm project_file
```

If the file is already modified or staged, then to remove -f have to be used.
```
git rm -f project_file
```

To remove only from git but not from the system(HDD). So that git no longer track
the file.
```
git rm --cached project_file
```

### Moving/Renaming files ###

`git mv` is used to rename files/folders

```
git mv project_file my_project_file
```

### View logs ###

`git log` is used to view commit logs/history

```
git log					# Show entire commit log of the repo
git log -n				# Show last n commit logs
git log -p -n				# Show last n commit log including change/patch/diff in those commits
git log --stat				# Commit log witch list of modified files and stat of the changes in those files
git log --pretty=oneline		# show each commit log in one line with only full SHA and subject
git log --pretty=short			# Log with SHA, author and subject
git log --pretty=full			# Log with SHA, author, commiter, subject, message body
git log --pretty=fuller			# Log with SHA, author, commiter, subject, message body, write and commit dates
git log --oneline			# Show first 7 characters of SHA value, Heading
git log --format="%h - %an, %ad: %s"	# Custom log output format
git log --graph				# Will show a ascii graph of commit history
git log --relative-date			# Will show relative date(days, weeks etc) rather than exact date
git log --since=2.weeks			# Show all commits since a specific date or relative date
git log --until=2.weeks			# Show all commit before a specific date or relative date
got log --author=AUTHOR			# Show the logs of a specific author
```

### Modifying last commit ###

After a commit, to redo that commit for additional changes
`git commit --amend` can be used. This is useful when accidentally
forgot to add files to a commit. 

```
git commit -m "Serious bugfix"		# Accidentally commited without forgotten_files
git add forgotten_files			# forgotten_files is added
git commit --amend			# Previous commit will be modified by adding forgotten_files
```

If this command is used just after a commit, editor will show up to edit
the commit message. So this can be used to modify minor changes in the latest
commit message.

```
git commit -m "Serious busfix"
git commit --amend			# Edit busfix -> bugfix
```

### Removing files from staging area ###

After files are staged in the staging are using `git add` command, to
remove the file from the staging area:

```
git reset HEAD file_name
```

### Unmodifying a modified file ###

When a file is modified which is tracked by git, git show the modified
flag in `git status`. Following command can be used to discard the modification.
If this is used, git will no longer show it as modified, also modifications
to that file will be gone.

```
git checkout -- file_name
```

### Managing Remote ###

* Adding a remote repository to local

```
git remote add <shortname> <url>
git remote add origin git@github.com:aagontuk/cheatsheets.git
```

* View the list of remote

```
git remote show
```

* View details of a remote

```
git remote show <shortname>
git remote show origin
```

* Fetching data from remote. Fetching will only download data
from remote but will not merge automatically. After fetching
you have to manually merge.

```
git fetch <remote>
git fetch origin
```

* Pulling will fetch data and merge automatically

```
git pull
```

* Pushing local to remote

```
git push <remote> <branch>
git push origin master
```

* Renaming a remote

```
git remote rename back backports
```

* Changing URL of a remote

```
git remote set-url <remote_name> <new_url>
git remote set-url origin https://github.com/aagontuk/cheatsheets.git
```

* Removing a remote

```
git remote remove paul
```

### Tagging ###

* View tags

```
git tag
```

* Search for tags

```
git tag -l "v1.1.*"
```

* Creating a annoted tag

```
git tag -a v1.2 -m "Version 1.2"
```

* Creating a lightwight tag

```
git tag v1.2-rc4
```

* Tagging later in a specific commit

```
git tag <tag> <sha>
git tag v1.2 a02fed6
```

* Viewing tag information

```
git show <tag>
git show v1.2
```

* Tags have to be pushed separately in the remote.
To push tags:

```
git push origin v1.2	# will push tag v1.2
git push origin --tags	# will push all tags
```

* To delete a tag from local:

```
git tag -d v1.2-rc4
```

This will only delete from local. To also delete from remote:

```
git push origin :refs/tags/v1.2-rc4
```

* To checkout in a tag following command have to be used.

```
git checkout v1.1
```

Checkout in a tag will leave the repo in detached HEAD state.
After checking out to make further commits to this a new
branch have to be created.

```
git checkout -b version1.1 v1.1
```

### Aliasing ###

Creating command aliases:

```
git config --global alias.unstage 'reset HEAD --'
```

Aliasing a external tool:

```
git config --global alias.mergetool '!meld'
```
