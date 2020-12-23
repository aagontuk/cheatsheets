# Regular Expression #

## Basic Regular Expression ##

* `^A` - Match with any line starts with A
* `A$` - Match with any line ends with A
* `A^` - Match with any line containging A^
* `$A` - Match with any line containging $A
* `^^` - Match with any line containging ^^
* `$$` - Match with any line containging $$
* `[XYZ]` - Match with any line containging X, Y or Z
* `[0-9]` - Match wiht any line containging 0,1,...,9
* `[^A-Z]` - Matches that doesn't contain A-Z.
* `.` - Matches any character
* `*` - Matches zero or more time
* `\{m\}` - Matches if pattern repeats exactly m times.
* `\{m,n}` - Matches if the pattern repeats m to n times.
* `\{,n}` - Matches if the pattern repeats less or equal n times.
* `\{m,}` - Matches if the pattern repeats more or equal to m times.
* `\<[tT]he\>` - Matches exactly the/The.

* `\(a\)\1` - \(PATTERN\) remembers the pattern and the pattern can be used again by \n where n=[1,9].
So total nine patterns can be remembered and backreferenced. Another example: `\([a-z]\)\([a-z]\)[a-z]\2\1`
matches with any 5 letter palindrome.

## Extended Regular Expression ##

* `?` - Matches zero or one time.
* `+` - Matches one or more time.
* `(abc|def)` - Matches abc or def.

## grep example

```bash
echo -e "(123)-451-789\n(123)457-869" | grep "([0-9]\{3\})-[0-9]\{3\}-[0-9]\{3\}"
```
