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
