## Python Object Types ##

### Python Data Types ###

Numbers		- 1.23, 123, 3+4i
Strings		- "hello, world"
Lists		- [1, 'hello', ['I', 'am', 'list', 'in', 'a', 'list'], 4.5]
Dictionary	- {"key":"value", 'foo':0, 'bar':'drink'}
Tuples		- (4, 'hello', 3.14)
Others		- set, types, booleans, none

*Numbers, Strings, Tupples are immutable. Means they can't be changed after creation*
*Lists and Dictionaries are mutable*

### Strings ###

Example: 'hello, world', "I am me" etc

`len()` function gives the length of the string.
```python
>>> str = "Hello, World"
>>> print len(str)
12
```

Individual character can be indexed from a string. Index can be negative. Negative index will return chars backword.
```python
>>> print str[0]
H
>>> print str[-1]
d
>>> print str[-2]
l
```

**Slicing:** Extract a section of a string in one step. str[m:n] will produce 'str[m]str[n-1]'. Default value of m is 0 and n is the length of the string.
```python
>>> print str[7:10]
'Wor'
>>> str[:]
'Hello, World'
>>> str[:4]
'Hell'
>>> str[:-1]
'Hello, Worl'
```

Strings can be concatenated using + sign and repeated using * sign.
```python
>>> foo = "I am little bunny foo foo"
>>> bar = " and bar is with me"
>>> foo + bar
'I am little bunny foo foo and bar is with me'
>>> foo * 3
'I am little bunny foo fooI am little bunny foo fooI am little bunny foo foo'
```

**Every operation we have performed on string can be performed other sequence objects like lists and tupples**

#### Some methods ####

```python
>>> string = "foo bar"
>>> string.find('o')
1
>>> string.replace('oo', 'uu')
'fuu bar'
>>> string
'foo bar'	# String itself unchanged as immutable
>>> bands = "Warfaze, Black, Artcell, Bangla"
>>> bands.split(',')	# Split according to the argument and return as list
['Warfaze', ' Black', ' Artcell', ' Bangla']
string = "Hello, how are you\n\n\n"
>>> string = string.rstrip()	# Remove whitespaces from the rigth most side
>>> string
'Hello, how are you'
```

`ord()` function returns ASCII value of a character.

```python
>>> ord('A')
65
```

**\0 or null terminator doesn't end python strings**
```python
>>> s = 'A\0B\0C'
>>> s
'A\x00B\x00C'
>>> print s
ABC
>>> len(s)
5
```

Multiline strings can be specified using three " or '.
```python
>>> str = """
... When this form is used
... all the lines are concatenated togather
...     and end-of-the line characters are added
... where line breaks appear
... """
>>> str
'\nWhen this form is used\nall the lines are concatenated togather\n\tand end-of-the line characters are added\nwhere line breaks appear\n'
>>> print str

When this form is used
all the lines are concatenated togather
	and end-of-the line characters are added
where line breaks appear
```


































