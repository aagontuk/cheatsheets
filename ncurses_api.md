# NCURSES API #

## Index ##

* [Initializing Functions](https://github.com/aagontuk/cheatsheets/blob/master/ncurses_api.md#initialization-functions)
* [Input / Output Functions](https://github.com/aagontuk/cheatsheets/blob/master/ncurses_api.md#input--output-functions)
  * [Output Functions](https://github.com/aagontuk/cheatsheets/blob/master/ncurses_api.md#output-functions)
  * [Input Functions](https://github.com/aagontuk/cheatsheets/blob/master/ncurses_api.md#input-functions)
* [Attributes](https://github.com/aagontuk/cheatsheets/blob/master/ncurses_api.md#attributes)
* [Managing Windows](https://github.com/aagontuk/cheatsheets/blob/master/ncurses_api.md#managing-windows)
* [Links](https://github.com/aagontuk/cheatsheets/blob/master/ncurses_api.md#links)

### Initialization Functions ###

* `initscr()` - Start curses mode.

* `raw()` and `cbreak()` - Normally the terminal driver buffers the characters a user types until a new line or carriage return is encountered. But most programs require that the characters be available as soon as the user types them. The above two functions are used to disable line buffering. The difference between these two functions is in the way control characters like suspend (CTRL-Z), interrupt and quit (CTRL-C) are passed to the program. In the raw() mode these characters are directly passed to the program without generating a signal. In the cbreak() mode these control characters are interpreted as any other character by the terminal driver.

* `echo()` and `noecho()` - if noecho() is used key press will not echoed in the screen. other do the oposite.

* `keypad(stdscr, TRUE)` - To get special inputs like F1, F2, Arrow keys etc.

### Input / Output Functions ###

For each input/output functions there are four types of function.

* Normal		: `printw(string)` - print in the current position of the cursor in the standard screen(stdscr).
* w less mv type: `mvprintw(y, x, string)` - move cursor to x, y then print in that position in the stdscr.
* w type		: `wprintw(window, string)` - print string in the current cursor position of the specified window.
* w ed mv type	:` mvwprintw(window, y, x, string)` - move to x, y and then print string in the specified window.

#### Output Functions ####

* `printw(string)` - print string.
* `addch(ch, attributes)` - print single character.
* `addstr(string)` - print string.

**NB:** Each function has corresponding mv, w, mvw functions.

#### Input Functions ####

* `ch = getch()` - to get a character from keyboard.
* `scanw()` - `scanf()` like function.
* `getstr(str)` - to get a string.

**NB:** Each function has corresponding mv, w, mvw functions.


### Attributes ###

Attributes are used to set different text properties. Like Bold, Underlined, Italic etc.

* `attron(attribute1 | attrubute2 | ...)` - To set some attribute on.
* `attroff(attr1 | attr2 | ...)` - to set some attribute off.
* `attrset(attr1 | attr2 | ...)` - Remove any prevoius attributes and set specified attributes.

Here is a list of some attributes:

| Attribute    | Effect 								|
| :----------: | :------------------------------------: |
| A_NORMAL	   | Normal Output							|
| A_STANDOUT   | Best highlighting mode of the terminal |
| A_UNDERLINE  | Underlined								|
| A_REVERSE    | Reverse video							|
| A_BLINK      | Blinking								|
| A_DIM        | Half bright							|
| A_BOLD       | Extra bright or bold					|
| A_PROTECT    | Protected mode							|
| A_INVIS      | Invisible or blank mode				|
| A_ALTCHARSET | Alternate character set				|
| A_CHARTEXT   | Bit-mask to extract a character		|
| COLOR_PAIR(n)| Color-pair number n					|

**NB:** There is also corresponding w functions like `wattron()` which work on specific window.

* `chgat(nChar, attribute, color_pair_token, null)` - This function set an attribute on texts without changing cursor position. `nChar` is the number of char on which `attribute` will be set. Negative `nChar` means end of the line. `color_pair_token` is for color pair. last is always null.

* `mvchgat(y, x, nChar, attribute, color_pair_token, null)` - `chgat()` from x, y position.

### Managing Windows ###

* `WINDOW *newwin(height, width, starty, startx)` - To create a new window. It takes height and width of the window as argument. Also takes x, y position of the window. Returns a WINDOW pointer.

* `delwin(WINDOW *win)` - To remove a window.
* `box(window, vchar, hchar)` - vchar & hchar is ther char which will be used to draw boxes vertical and horizontal lines.
* `wborder(window, ls, rs, ts, bt, tl, tr, bl, br)` - 2 - 8 arguments are character for drawing ls(left side), rs(right side) of the box.

### Links ###

* [Ncurses Programming HOWTO](http://www.tldp.org/HOWTO/NCURSES-Programming-HOWTO/)
* [Ncurses Manual Pages](http://invisible-island.net/ncurses/man/ncurses.3x.html)
