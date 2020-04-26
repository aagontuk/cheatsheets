## INDEX ##

1. [Setting/Unsetting values](https://github.com/aagontuk/cheatsheets/blob/master/vim_cheatsheet.md#settingunsetting-values)
2. [Saving session](https://github.com/aagontuk/cheatsheets/blob/master/vim_cheatsheet.md#saving-session)
3. [Auto complete](https://github.com/aagontuk/cheatsheets/blob/master/vim_cheatsheet.md#auto-complete)
4. [File Explorer](https://github.com/aagontuk/cheatsheets/blob/master/vim_cheatsheet.md#file-explorer)
5. [Repeating commands](https://github.com/aagontuk/cheatsheets/blob/master/vim_cheatsheet.md#repeating-commands)
6. [Bookmarks](https://github.com/aagontuk/cheatsheets/blob/master/vim_cheatsheet.md#bookmarks)

### Setting/Unsetting Values ###

```
set number      # set
set nonumber    # unset
set number!     # toggle

set numberwidth=3           # key=value
set number numberwidth=3    # Multiple setting at once
```

### Saving session ###

```
mksession my-work-session.vim
```

### Auto complete ###

Press `Ctrl+n` in insert mode.

### File Explorer ###

Give `::Explore` command

### Repeating commands ###

* Press `qX` where X=any letter to start recording.
* Use some commands
* Press `@X` where X=previously used letter.

You can use `@@` after using `@X` once.

### Bookmarks ###

* mX where X=a-z for setting local bookmarks(In same file).
* mX where X=A-Z for setting global bookmarks(In any file).
* 'X where X=a-zA-Z to go to the bookmarks.
* :marks to show all the bookmarks.
