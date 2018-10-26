## Frequently Used Git Commands ##

### git config ###

To create and modify system/user/repo git configuration file.

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

### git init ###

To initialize a project as git repository.

```
git init
```

### git clone ###

For cloning a remote repository into local system.

```
git clone https://github.com/aagontuk/cheatsheets mycheatsheets
```

### git status ###

To see status of the project files. Untracked/tracked/modified/staged.

```
git status	# Show details status
git status -s	# Show brief status
```

### git add ###

To add untracked/modified files to staging area and prepare for commit.
If a directory is added, its contents will be added recursively.

```
git add README.md
```

### git diff ###

Show changes of a file

```
git diff		# Shows changes between last staged and unstaged
git diff --staged	# Shows changes between the last commit and staged
```

### git commit ###

For commiting changes that are staged

```
git commit			# To commit changes that are staged.
git commit -m "COMMIT_MSG"	# Commit with inline commit message.
git commit -a			# stage all modified files and commit.
```
