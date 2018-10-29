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

For cloning a remote repository into local system.

```
git clone https://github.com/aagontuk/cheatsheets mycheatsheets
```

### Showing status of the project ###

To see status of the project files. Untracked/tracked/modified/staged.

```
git status	# Show details status
git status -s	# Show brief status
```

### Adding files to staging area ###

To add untracked/modified files to staging area and prepare for commit.
If a directory is added, its contents will be added recursively.

```
git add README.md
```

### Inspect changes of a file ###

Show changes of a file

```
git diff		# Shows changes between last staged and unstaged
git diff --staged	# Shows changes between the last commit and staged
```

### Commiting ###

For commiting changes that are staged

```
git commit			# To commit changes that are staged.
git commit -m "COMMIT_MSG"	# Commit with inline commit message.
git commit -a			# stage all modified files and commit.
git commit -v			# will add diff of changes in the commit message.
```

### Removing files ###

To remove files.

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

To rename files/folders

```
git mv project_file my_project_file
```

### View logs ###

To view commit logs/history

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
