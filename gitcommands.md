# INDEX #

1. [Frequently used git commands](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#frequently-used-git-commands)
    1. [Configuring git](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#configuring-git)
    2. [Initializing a project](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#initializing-a-project)
    3. [Cloning a repository from remote](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#cloning-a-repository-from-remote)
    4. [Showing status of the project](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#showing-status-of-the-project)
    5. [Adding files to staging area](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#adding-files-to-staging-area)
    6. [Inspect changes of a file](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#inspect-changes-of-a-file)
    8. [Creating and applying patch file](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#creating-and-applying-patch-file)
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

2. [Branching and Merging](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#branching-and-merging)
    1. [Creating a new branch](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#creating-a-new-branch)
    2. [Switching to a branch](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#switching-to-a-branch)
    4. [Deleting a branch](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#deleting-a-branch)
    5. [Renaming a branch](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#renaming-a-branch)
    6. [Merging a branch to another branch](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#merging-a-branch-to-another-branch)

3. [Remote Branches](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#remote-branches)
    1. [Fetching commits from remote repository](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#fetching-commits-from-remote-repository)
    2. [Pushing/fetching a new branch to/from remote repository](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#pushingfetching-a-new-branch-tofrom-remote-repository)
    3. [Tracking Branch](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#tracking-branch)
    4. [Pulling](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#pulling)
    5. [Deleting a remote branch](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#deleting-a-remote-branch)

4. [Rewriting history](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#rewriting-history)
    1. [Removing commits](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#removing-commits)

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

* Adding whole file:

```
git add README.md
```

* Adding portion of a file:

```
git add -p README.md    # This will bring an interactive prompt
```

### Inspect changes of a file ###

`git diff` is used to show changes of a file

```
git diff		# Shows changes between last staged and unstaged
git diff --staged	# Shows changes between the last commit and staged
git diff COMMIT_HASH~ COMMIT_HASH   # Show diff between last commit and its ancestor
```
### Creating and applying patch file ###

For creating patch file use `git diff`:

```
git diff > mypatch.patch
```

If you want add untracked files too first stage them
using `git add` then create the patch file:

```
git diff --cached > mypatch.patch
```

Now you can
[remove those untracked files from staging area](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#removing-files-from-staging-area)
if you don't want to commit them.

If you want to add binary files in the patch:

```
git diff --binary > mypatch.patch
```

To apply a patch:

```
git apply mypatch.patch
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
git log --author=AUTHOR			# Show the logs of a specific author
git log --follow -- FILE        # Show all the commits to a specific file
git log testing                 # Show the logs of testing branch
git log --all                   # Show logs of all branches. By default shows only the logs of checked out branch
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

If you want to remove files that were added in a commit
mistakenly:

```
git reset --soft HEAD~N
```

N is the commit number relative to HEAD. Which is 1 for
the latest commit.

You will see last commit was deleted and all the files
in staging area again. Now you can
[remove unwanted files from there](https://github.com/aagontuk/cheatsheets/blob/master/gitcommands.md#removing-files-from-staging-area).

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

* Dry run merge

```
git merge --no-commit --no-ff $BRANCH_NAME
```

This will stage the changes but won't commit them.
To see the staged changes:

```
git diff --cached
```

To undo the merge:

```
git merge --abort
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

* Creating a annotated tag

```
git tag -a v1.2 -m "Version 1.2"
```

* Creating a lightweight tag

```
git tag v1.2-rc4
```

In annotated tag when shown with `git show` tag information and commit will be shown.
But in lightweight tag only commit information will be shown.

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

Now you can use `git unstage file1` instead of `git reset HEAD -- file1` to unstage file1.

Aliasing a external tool:

```
git config --global alias.mergetool '!meld'
```

## Branching and Meging ##

### Creating a new branch ###

Create a new branch named *testing*:

```sh
git branch testing
```

### Switching to a branch ###

Switch to a branch named *testing*:

```sh
git checkout testing
```

This shortcut can be used to create and checkout to a new branch in one command:

```sh
git checkout -b testing
```

This will create branch *testing* and switch to it.

### Show all the branches ###

```sh
git branch --all
```

### Deleting a branch ###

```sh
git branch -d testing
```

### Renaming a branch ###

For example you want to change your branch name from *bad_branch_name* to *good_branch_name*.

```sh
git branch --move bad_branch_name good_branch_name
```

This will only change the local branch name. To change the remote branch name too
you have do first push the renamed branch to remote:

```sh
git push --set-upstream origin good_branch_name
```

Now there will be two branch in remote *remotes/origin/bad_branch_name* and
*remotes/origin/good_branch_name*. Remove *remote/origin/bad_branch_name*

```sh
git push origin --delete bad_branch_name
```

### Merging a branch to another branch ###

Let's say your are now in testing branch. You have added some changes and now
want to merge the commits of testing branch into master branch:

```sh
git checkout master
git merge testing
```

## Remote Branches ##

Remote branches are named like `<remote_name>/<remote_branch_name>`.
For example `origin/master`. This points to the latest commit of your
remote repository at the time of your last synchronization.

### Fetching commits from remote repository ###

```sh
git fetch <remote_name>/<remote_branch_name>
```

This will synchronize the remote branch with the local repository.
For example if your remote branch name is `origin/master` this will
synchronize `orgin/master` with the local repository. Note that this
will not merge commits from remote branch(`origin/master`) into
your local branch(`master`). You have to do it manually.

### Pushing/fetching a new branch to/from remote repository ###

For example you have created a new branch named `testing` and
added some commits to it. Now you want to upload it to your
remote repository:

```sh
git push origin testing
```

This will create a new branch named `testing` in your remote repository.
If you want to name the remote branch name different from the local
branch name:

```sh
git push origin testing:experimental
```

For the next example lets say you didn't name the differently.
Now if someone who is also forked that remote repository do fetch, a new
remote branch named `origin/testing` will be created in their local
repository. Not this will not create any new local branch to work on for them.
They will have to do it manually:

```sh
git checkout -b testing origin/testing
```

You can also use this shortcut if you keep the local branch name
and remote branch name same:

```sh
git checkout testing
```

If you want to give a different name to the local branch:

```sh
git checkout -b experimental origin/testing
```

### Tracking Branch ###

Checking out a local branch from a remote branch creates
a tracking branch. Tracking branch means that local branch
and the remote branch has a direct relationship with each other. If you
are in that local branch when you do a push git will automatically
push the commits to the remote branch and when you do pull
git will automatically merge all the commits from the remote branch
to that local branch.

For example in above example if your are in `testing` branch, when you do a
pull git will merge all the commits from `origin/testing` to `testing` automatically.
And after working on `testing` when you do push git will automatically push
all the commits to `origin/testing`.

If you have a local branch which don't have a tracking branch or you want to
change the remote tracking branch. For example if you currently on `testing`
branch and want to set `origin/testing` as you remote tracking branch:

```sh
git branch -u origin/testing
```

### Pulling ###

For automatically fetching commits from remote branch and merging with
local tracking branch use:

```sh
git pull
```

It is equivalent to:

```sh
git fetch
git merge
```

### Deleting a remote branch ###

```sh
git push origin --delete testing
```

This will delete branch `testing` from remote repository.

## Rewriting history ##

### Removing commits ###

Lets say your commit history looks like this:

| Number | Commit Hash | Commit Message | 
|--------|-------------|----------------|
|1|4d884d0|Important fix|
|2|5540e24|server fix|
|3|4c5199f|client fix|
|4|7879940|My awesome fix|
|5|2c27f34|minor fix|

If you want to remove consecutive commits you can use `git rebase`. For example
if you want to remove commit 3 and 4 you can do following:

```sh
git rebase --onto <branch_name>~<number of the oldest commit you want to remove> <branch_name>~<number of the oldest commit you want to keep> <branch_name>
```

So if you want to remove 3 and 4 in master branch:

```sh
git rebase --onto master~4 master~2 master
```

Now if you want to remove non-consecutive commits, you can use `git cherry-pick`. For example if you want to
remove commit 2 and 4 you have to do following procedure:

* Go to oldest usable commit(In this case 5)
* Create a new branch
* cherry pick the commits you want to keep(In this case 3 and 1) after that commit(In this case 5).
* Checkout to the previous branch you were in.
* Do a hard reset to the last usable commit(In this case 5)
* Merge the new branch in this branch

So lets say in our case you were in master branch and want to remove commit 2 and 4:

```sh
git checkout 2c27f34
git checkout -b new_branch
git cherry-pick 4c5199f
git cherry-pick 4d884d0
git checkout master
git reset --hard 2c27f34
git merge new_branch
```

After deleting the commit(s) you have to force push in the remote repository:

```sh
git push --force origin master
```

Note that deleting commits can introduce merge conflicts.
