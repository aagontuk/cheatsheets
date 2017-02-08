## Index ##
1. [Python Object Types](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#python-object-types)
  1. [Python Data Types](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#python-data-types)
  2. [Strings](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#strings)
  3. [Lists](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#lists) 
  4. [Dictionary](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#dictionary)
  5. [Tuples](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#tuples)
  6. [Sets](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#sets)

2. [Python Data Types In Details](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#python-data-types-in-details)
  1. [Numbers](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#numbers)
  2. [Strings](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#strings-1)
  3. [Lists](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#lists-1)
  4. [Dictionaries](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#dictionaries)
  5. [Tuples](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#tuples-1)
  6. [File](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#file)
  7. [Boolean Values In Python](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#boolean-values-in-python) 

3. [Python Statements and Syntax](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#python-statements-and-syntax)
  1. [Notes About Python Statements And Syntax](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#notes-about-python-statements-and-syntax)
  2. [Assignment Statement](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#assignment-statement)
  3. [Print Statement](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#print-statement)
  4. [Python If Statement](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#pyhton-if-statement)
  5. [Python While And For Loops](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#python-while-and-for-loops)

4. [Python Keywords and Symbols](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#python-keywords-and-symbols)
  1. [At a Glance](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#at-a-glance)

5. [Tricks](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#tricks)
  1. [List All Attributes of an Object](https://github.com/aagontuk/cheatsheets/blob/master/py_cheat.md#list-all-attributes-of-an-object)

## Python Object Types ##

### Python Data Types ###

| Object Type | Example                                                   |
| :---------- | --------------------------------------------------------: |
| Numbers     | 1.23, 123, 3+4j											  |
| Strings     | "hello, world"											  |
| Lists       | [1, 'hello', ['I', 'am', 'list', 'in', 'a', 'list'], 4.5] |
| Dictionary  | {"key":"value", 'foo':0, 'bar':'drink'}					  |
| Tuples      | (4, 'hello', 3.14)										  |
| Others      | set, types, booleans, none								  |

*Numbers, Strings, Tupples are immutable. Means they can't be changed after creation*
</br>
*Lists and Dictionaries are mutable*

### Strings ###

Example: 'hello, world', "I am me" etc

`len()` function gives the length of the string.
```python
>>> str = "Hello, World"
>>> print len(str)			# Python 2
12
>>> print(len(str))			# Python 3
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

#### Slicing ####

Extract a section of a string in one step. str[m:n] will produce 'str[m]str[n-1]'. Default value of m is 0 and n is the length of the string.

```python
>>> print str[7:10]		# Slice from 7 to 10(non-inclusive)
'Wor'

>>> str[:]				# Slice from start to end */
'Hello, World'

>>> str[:4]				# Slice from start upto 4
'Hell'

>>> str[:-1]			# Slice from start upto last item
'Hello, Worl'
```

General format of slicing is x[i:j:k]. Where k is the step size from i upto j.
k can be negative, in that case slice will occur from i upto j in reverse order. Default value of k is 1.

```python
>>> "12345678"[1:6:2]	# From index 1 upto index 6 and step size 2
'246'

"hello"[::2]			# Entire string, step size 2
'hlo'

"hello"[::-1]			# Entire string. Step size 1. But as the step
'olleh'					# size is negetive, slicing will be done in reverse order
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

*Every operation we have performed on string can be performed other sequence objects like lists and tupples*

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

`chr()` function converts ASCII value to character.
```python
>>> chr(65)
'A'
```

*\0 or null terminator doesn't end python strings*
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

### Lists ###

List object is sequence object. They are mutable.

```python
>>> list = [1, 2.3, 'foo']	# Creating list object
>>> len(list)				# Finding length
3
>>> list[0]					# Can be indexed
1
>>> list[-1]
'foo'
>>> list[1:3]				# Slicing
[2.3, 'foo']
>>> list + ['bar']			# Concatenation
[1, 2.3, 'foo', 'bar']
>>> list = list + ['bar']	# Mutability
>>> list
[1, 2.3, 'foo', 'bar']
```

#### Type specific operations ####

1. Can hold different types of object
2. No fixed size
3. Mutable.

```python
>>> list = [1, 'foo']
>>> list.append('bar')		# Add an item at the end of the list
>>> list
[1, 'foo', 'bar']
>>> list.insert(1, 'baz')	# Insert an item at a specific index
>>> list
[1, 'baz', 'foo', 'bar']
>>> list.pop(1)				# return and remove an item from a specific
'baz'						# index
>>> list
[1, 'foo', 'bar']
>>> list.remove('bar')		# remove first occurance of an item found
>>> list					# in the list
[1, 'foo']
```

As list is a mutable object there are methods that can change a list object in place.

```python
>>> list = ['heaven', 'and', 'hell']
>>> list.sort()							# Sort List
>>> list
['and', 'heaven', 'hell']
>>> list.reverse()						# Reverse sort List
>>> list
['hell', 'heaven', 'and']
```

Lists can be nested.

```python
matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
>>> matrix[0]
[1, 2, 3]
>>> matrix[0][0]
1
```

#### List Comprehensions ####

List comprehension is a way to build a new list running an expression on each item in a sequence, once at a time.

```python
>>> matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
>>> col2 = [row[1] for row in matrix]
>>> col2
[2, 5, 8]
>>> list = [var for var in range(0, 11)]
>>> list
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
[num for num in range(0, 11) if num % 3 == 0]	# Filtering
[0, 3, 6, 9]
```

### Dictionary ###

Dictionaries are used to store value in a key value pair.

1. Mutable
2. Values are stored in a key value pair
3. Stores any type of objects
4. Can be nested

```python
band = {'name':'Bangla', 'albums':2}			# Creation
>>> band
{'albums': 2, 'name': 'Bangla'}
>>> band['name']								# Indexing by key
'Bangla'
>>> band['started'] = 1999						# Mutable
>>> band
{'started': 1999, 'albums': 2, 'name': 'Bangla'}
```

**Type Specific Methods:**

```python
>>> dic = {'c':1, 'a':2, 'b':3}
>>> dic
{'a': 2, 'c': 1, 'b': 3}
>>> dic.keys()					# Returns List of the keys
['a', 'c', 'b']
```

**Iterating over a Dictionary:**

```python
>>> dic = {'c':1, 'a':2, 'b':3}
>>> dic
{'a': 2, 'c': 1, 'b': 3}
>>> for key in dic.keys():
...     print "key: %s\tValue: %s" % (key, dic[key])
... 
key: a	Value: 2
key: c	Value: 1
key: b	Value: 3
```

### Tuples ###

Python tuples are list like sequence object. But they are immutable.

```python
>>> T = (1, 2, 3, 4)
>>> T
(1, 2, 3, 4)
>>> T[0]
1
>>> len(T)
4
>>> T[1] = 10
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: 'tuple' object does not support item assignment
```

### Sets ###

Collection of unique elements. Supports usual mathematical set operations.

```python
>>> x = set('hello')
>>> x
set(['h', 'e', 'l', 'o'])
>>> y = set(['w', 'o', 'r', 'l', 'd'])
>>> y
set(['d', 'r', 'o', 'w', 'l'])
>>> x & y
set(['l', 'o'])
>>> x | y
set(['e', 'd', 'h', 'l', 'o', 'r', 'w'])
>>> x - y
set(['h', 'e'])
```

## Python Data Types In Details ##

### Numbers ##

#### Numeric Display Formats ####

`repr()` display numbers as in code.					</br>
`str()` Convert numbers into string.					</br>
`oct()` converts decimal into octal						</br>
`hex()` converts decimal into hexadecimal				</br>
`int(string, base)` - converts strings into numbers.	</br>
`float()` - Coverts strings into floating point number.	</br>
`bin()` - Converts integer to binary					</br>

#### Decimal Object ####

Fixed precision representation of numbers.

```python
>>> 0.1 + 0.2 - 0.3
5.551115123125783e-17							# The problem
>>> from decimal import Decimal
>>> Decimal(0.1) + Decimal(0.2) - Decimal(0.3)	# Solution
Decimal('2.775557561565156540423631668E-17')
>>> Decimal('0.1') + Decimal('0.2') - Decimal('0.3')
Decimal('0.0')
>>> Decimal(1) / Decimal(7)
Decimal('0.1428571428571428571428571429')
>>> decimal.getcontext().prec = 4				# Precision
>>> Decimal(1) / Decimal(7)
Decimal('0.1429')
```

### Strings ###

Different Forms:

1. Single Quotes: 'he said, "hello"'
2. Double Quotes: "Robin's book"
3. Block of strings: """string block""", '''String Block'''
4. Raw strings: r'\thello, world\n'. Take each characters leterally, omits escape
   sequences. e.g. r"C:\new\values". But raw string won't work for a string ended
   with backslash. r"...\"; This is invalid.
5. Byte Strings: b'spam'	**(Python 3)**
6. Unicode strings: u'\u0986\u09AE\u09BE\u09B0' **(in 2.6 only)**

In python 3 there are three string types. `str` is used for unicode text(ASCII and others). `bytes` is used
for bynary data. `bytearray` is mutable variant of bytes.


```python
>>> print 'he said, "hello"'	# Python 2.6
he said, "hello"

>>> print ('he said, "hello"')	# Have to use brackets in python 3
he said, "hello"

>>> print "Robin's book"
Robin's book

>>> print """Once upon a time
... there was a         man
... one day"""
Once upon a time
there was a		man
one day

>>> print r'\thello, world\n'
\thello, world\n

>>> print u'\u0986\u09AE\u09BE\u09B0'
আমার
```

#### Character Code Conversions ####

`ord('char')` convert char into ints ASCII value.
</br>
`chr(value)` convert from ASCII to character.
</br>
`eval(str)` - convert a string into python executable code.

```python
>>> list = [1, 2, 3]

>>> str = '%s' % list	# List is converted into a string

>>> str
'[1, 2, 3]'

>>> eval(str)			# String is converted back to list
[1, 2, 3]
```

#### String Formating ####

##### String Formating Expression ######

```python
>>> print("%s:%d\t%s:%d" % ("Alice", 40, "Bob", 50))
Alice:40	Bob:50
>>>
>>>print("My List: %s" % [1, 2, 3])
My List: [1, 2, 3]
```

| Type Code	| Meaning 					|
| :------------ | ------------------------: |
| %s			| String					|
| %r			| Raw string				|
| %c			| Character					|
| %d			| Integer					|
| %i			| Integer					|
| %u			| Unsigned Integer			|
| %o			| Octal						|
| %x			| Hexadecima(lower)			|
| %X			| Hexadecimal(Upper)		|
| %e			| Floating point Exponent	|
| %E			| e, but uppercase			|
| %f			| Floating point decimal	|
| %g			| e or f					|
| %G			| E or f					|
| %%			| literal %					|

General conversion code structure: %[(name)][flags][width][.precision]typecode </br>

**Dictionary base string formating:** "%(name)s has %(value)d taka" % {'name':'ashik', 'value':50}

##### String Formating Method Calls #####

```python
>>> 'Distance between {0} and {1} is {2} km'.format('Dhaka', 'Khulna', 279.6)
'Distance between Dhaka and Khulna is 279.6 km'
```

#### String Methods ####

`string.replace('old', 'new')` - replce old substring with new substring from string and return new string.
```python
>>> str  = "hello, world"
>>> str.replace('world', 'bob')
'hello, bob'
>>> str
'hello, world'
>>>
>>>
>>> str = 'FooBarFooBar'
>>> str
'FooBarFooBar'
>>> str.replace('Bar', 'Baz')		# Replace all occurance
'FooBazFooBaz'
>>> str.replace('Bar', 'Baz', 1)	# Replace only first occurance
'FooBazFooBar'
>>>
```

`string.find('substring')` - Find the index of the first occurance of the substring from string.
```python
>>> str = 'hello, world'
>>> str
'hello, world'
>>> where = str.find('ello')
>>> where
1
>>> str = str[:where] + 'ola' + str[(where + 4):]	# Replace trick
>>> str
'hola, world'
```

`list(string)` - convert string into list.

```python
>>> str
'FooBarFooBar'
>>> L = list(str)
>>> L
['F', 'o', 'o', 'B', 'a', 'r', 'F', 'o', 'o', 'B', 'a', 'r']
```

`string.join(list)` - join list items with string.

```python
>>> ''.join(L)	# Join list item of L with empty string
'FooBarFooBar'
```

`string.split(delimiters)` - split string into a list according to specified delimiters. Default delimiter is whitespaces if nothing specified.

```python
>>> str = 'Sing me song you are a singer'
>>> str.split()		# No delimiters specified. Default whitespaces.
['Sing', 'me', 'song', 'you', 'are', 'a', 'singer']
>>>
>>>
>>> str = 'Warfaze, Black, Artcell'
>>> str.split(', ')	# Used ', ' as delimiter
['Warfaze', 'Black', 'Artcell']
```

`string.rstrip()` - remove whitespaces from the end of the string.
</br>
`string.upper()` - Convert all characters into uppercase.
</br>
`string.endswith(substring)` - Check if the string ends with specified substring.

### Lists ###

* Some basic operations.
```python
>>> len([1, 2, 3])			# Length
3
>>>
>>> [1, 2, 3] + [4, 5, 6]	# Concatenation
[1, 2, 3, 4, 5, 6]
>>>
>>> [1, 2] * 3				# Repetition
[1, 2, 1, 2, 1, 2]
>>>
>>> 2 in [1, 2, 3]			# Membership Check
True
>>>
>>> for i in [1, 2, 3]:		# Iteration
...     print i
... 
1
2
3
```

* Indexing, Slicing, Nesting
```python
>>> list = [1, 2, 3]
>>> list[0]				# Indexing
1
>>>
>>> list[1:3]			# Slicing
[2, 3]
>>> matrix = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]	# Nesting
>>> matrix[0][0]
1
```

* Mutability
```python
>>> list = [1, 'foo', 2, 'bar']
>>> list[3] = 'baz'				# Changing in place using indexing
>>> list
[1, 'foo', 2, 'baz']
>>> list[1:3] = [2, 3]			# Changing in place using slicing
>>> list
[1, 2, 3, 'baz']
>>>
>>> del list[0]					# Delete one item from list
>>> list
[2, 3, 'baz']
>>>
>>> del list[1:]				# Delete a section from list
>>> list
[2]
>>>
>>> list = [1, 2, 3, 4]
>>> list[1:3] = []				# Another way of deleting a section
>>> list
[1, 4]
```

#### List Methods ####

* `list.append(item)` - To append item at the end of the list.
* `list.extend(argList)` - Append multiple items at the end of the list at once.
* `list.insert(index, item)` - To insert item at index index of the list.
* `list.pop([index])` - Remove item from list at index index. If index isn't specified default is the last item.
* `list.remove(item)` - Remove first occurence of the item from the list.
* `list.sort()` - Sort List.
* `list.reverse()` - Reverse sort the list.

```python
>>> mList = [1, 2]
>>> mList.append(3)			# Append at the end of the list
>>> mList
[1, 2, 3]
>>>
>>>
>>> mList.extend([4, 5])	# Extend list with multiple items
>>> mList
[1, 2, 3, 4, 5]
>>>
>>>
>>> mList.insert(1, 9)		# Insert at specific index
>>> mList
[1, 9, 2, 3, 4, 5]
>>>
>>>
>>> mList.pop()
5
>>> mList
[1, 9, 2, 3, 4]
>>> mList.pop(1)
9
>>> mList
[1, 2, 3, 4]
>>>
>>>
>>> mList.remove(4)
>>> mList
[1, 2, 3]
>>>
>>>
>>> mList.reverse()
>>> mList
[3, 2, 1]
>>> mList.sort()
>>> mList
[1, 2, 3]
```

### Dictionaries ###

* Creation:
```python
>>> dic = {'foo':0, 'bar':1, 'baz':2}
>>> dic
{'baz': 2, 'foo': 0, 'bar': 1}			# Notice Order Scambled
>>>
>>> dic['foo']							# Fetching value using key
0
```

* Some basic operations
```python
>>> dic
{'baz': 2, 'foo': 0, 'bar': 1}
>>> len(dic)					# Length
3
>>>
>>> 'foo' in dic				# Key membership check
True
>>> dic.has_key('bar')			# Key membership check
True
>>> dic.keys()					# Gives a list of all keys
['baz', 'foo', 'bar']
>>>
>>> dic
{'goo': 3, 'foo': 5, 'bar': 1}
>>> for key in dic.keys():		# Iterating
...     print dic[key]
... 
3
5
1
```

* Mutability
```python
>>> dic
{'baz': 2, 'foo': 0, 'bar': 1}
>>> dic['goo'] = 3							# Adding new entry
>>> dic
{'baz': 2, 'goo': 3, 'foo': 0, 'bar': 1}
>>>
>>>
>>> dic['foo'] = 5							# Changing existing entry
>>> dic
{'baz': 2, 'goo': 3, 'foo': 5, 'bar': 1}
>>>
>>>
>>> del dic['baz']							# Deleting an entry
>>> dic
{'goo': 3, 'foo': 5, 'bar': 1}
```

* Some methods
```python
>>> dic
{'goo': 3, 'foo': 5, 'bar': 1}
>>> dic.keys()							# Returns a list of all keys
['goo', 'foo', 'bar']
>>>
>>> dic.values()						# Returns a list of all values
[3, 5, 1]
>>>
>>> dic.items()							# Returns a list of tupples of 
[('goo', 3), ('foo', 5), ('bar', 1)]	# key/value pair
>>>
>>> dic.get('foo')						# Fetching
5
>>>
>>> dic2 = {'zoo':10, 'loo':40}
>>> dic.update(dic2)					# Exteding multiple items
>>> dic
{'goo': 3, 'bar': 1, 'foo': 5, 'loo': 40, 'zoo': 10}
>>>
>>> dic.pop('zoo')						# Deliting item
10
>>> dic
{'goo': 3, 'bar': 1, 'foo': 5, 'loo': 40}
```

### Tuples ###

Almost all properties are same as list, except tupples are immutable.
```python
>>> t = (0, 1, 2)			# Creation
>>> t
(0, 1, 2)
>>> tt = (2,)				# Single element tupple
>>>
>>> t[1]					# Indexing
1
>>> t + (3, 4)				# Concatenation
(0, 1, 2, 3, 4)
>>> (1, 2) * 3				# Repeatition
(1, 2, 1, 2, 1, 2)
>>> t
(0, 1, 2)
>>> t[1:]					# Slicing
(1, 2)
```

### File ###

`open(path, mode, buffering)` function opens a file and returns a file object which can be used to read and write files.
</br>

Open modes:

| Mode   | Effect													|
| :----: | -------------------------------------------------------: |
| r      | open file in read mode. Default, if nothing specified.	|
| w		 | Open file in write mode.									|
| a		 | Open file in append mode									|

#### Methods ####

* `file.write(str)` - write a string to a file.
```python
>>> outf = open('myfile', 'w')		# Creates a file object
>>> outf.write('hello, world\n')
>>> outf.close()
```

* `file.read()` - Reads whole file.
```python
>>> fin = open('myfile')	# Default read mode
>>> print fin.read()

hello, world!
I am foo.
I am bar.

>>>
```

* `file.readline()` - Returns a line from a file including \n.

```python
>>> fin.seek(0)
>>> fin.readline()
'hello, world!\n'
```

* `file.readlines()` - Returns a list of all lines from a file.

```python
>>> fin = open('myfile')
>>> fin.read()
'hello, world!\nI am foo.\nI am bar.'
>>> fin.seek(0)
>>> fin.readlines()
['hello, world!\n', 'I am foo.\n', 'I am bar.']
```

#### Python Pickles ####

Tool to store python object in a file directly with no to-or-from string conversion.

```python
# Storing Object

>>> list = [1, 2, 3]
>>> list
[1, 2, 3]
>>> fobj = open("file.bin", "wb")
>>> pickle.dump(list, fobj)
>>> fobj.close()

# Restoring object from file

>>> fobj = open("file.bin", "rb")
>>> l = pickle.load(fobj)
>>> l
[1, 2, 3]
```

#### Python Shelve ####

#### Packed Binary ####

### Boolean Values In Python ###

Boolean values are two constant objects **True** and **False**.

* Non zero numbers are true.
* Non empty objects are true.

Example:
```python
>>> bool(0)
False
>>> bool(1)
True
>>> bool(50)
True
>>> 
>>> bool([])
False 
>>> bool([1, 2])
True
>>>
>>> bool({})
False
>>> bool({'spam': '2$'})
True
>>>
>>> bool(None)
False
```

## Python Statements And Syntax ##

### Notes about python statements and syntax ###

* Python statements are ended by new lines. No semicolon is needed.
```python
a = 40			# Statement
x = a + 10		# Another Statement
```

* Semicolons can be used to use multiple statements in a single line.
```python
a = 40; b = 60; print(a + b)
```

* Brackets (first, second or third) are used to span single statement in multiple
lines.
```python
x = (a + b +
	 c + d)

list = [1, 2, 3,
	    4, 5, 6]
```

* Also `\` can be used to span single statement in multiple lines.
```python
x = a + b + \
	 c + d
```

* In python colons are used for compound statements (Statements which have nested
blocks)
```python
if x > y:
	print("%d is larger" % x)
```

* Nested blocks are nested using indentations. Curly braces are not needed.
```python
if x > y:
	a = x
	b = y
```

* For single line block statement can be placed right after colon.
```python
if x > y: print(x)
```

### Assignment Statement ###

* Assignments create object references.
* Names are created when first assigned.
* Names must be assigned before being referenced.

#### Different types of assignment statement: ####
```python
>>> spam = 'hello, world'				# Basic form
>>> spam
'hello, world'
>>> spam, ham = 'hello', 'world'		# Tupple assignment(Positional)
>>> spam, ham
('hello', 'world')
>>> [spam, ham] = ['hello', 'world']	# List assignment(Positional)
>>> spam, ham
('hello', 'world')
>>> 
>>> a, b, c, d = 'spam'					# Sequence assignment
>>> a, b, c, d
('s', 'p', 'a', 'm')
>>> 
>>> a, *b = 'spam'						# Extended sequence unpacking
>>> a
's'
>>> b
['p', 'a', 'm']
>>> spam = ham = 'launch'				# Multiple assignment
>>> spam, ham
('launch', 'launch')
```

In case of multiple assignment all the variables point to the same object(same piece of memory)
```python
>>> spam = ham = [1, 2, 3]	# spam & ham are pointing to same object
>>> spam
[1, 2, 3]
>>> ham
[1, 2, 3]
>>> spam[1] = 4				# spam changed
>>> spam
[1, 4, 3]
>>> ham						# ham changed too as they are pointing to same object
[1, 4, 3]
```

#### Concatenation VS In-place assignment: ####

In case of concatenation must create a new object, copy it in the object on the
left, then copy it on the right. So it is slower. On the other hand in case of
in-place  assignment new item is just added at the end of the memory block.

```python
>>> L = [1, 2]
>>> L = L + [3, 4]		# Concatenation: Slower
>>> L
[1, 2, 3, 4]
>>> L.extend([5, 6])	# In-place assignment: Faster
>>> L
[1, 2, 3, 4, 5, 6]
>>> L += [7, 8]			# Python automaticaly use the faster method
```

```python
>>> L = [1, 2]
>>> M = L			# M & L are shared object
>>> M
[1, 2]
>>> L
[1, 2]
>>> 
>>> L = L + [3]		# Concatenation
>>> L
[1, 2, 3]			# L changed
>>> M
[1, 2]				# But M isn't as concatenation creates new object
>>>
>>> M = L			# M is pointing to L
>>> M
[1, 2, 3]
>>> 
>>> L += [4]		# In-place assignment
>>> L
[1, 2, 3, 4]		# L is changed
>>> M
[1, 2, 3, 4]		# M is changed too as augmented assignmets are in-place
```

#### Python variable naming convension ####

* Names that begin with single underscore(`_X`) are not imported by from module
import * statement

* Names that begin with two leading and trailing underscore(`__X__`) are system
defined and have special meaning to interpreter.

* Names that begin with two leading underscore(`__X`) are localized to enclosing
classes

* Class names usually starts with uppercase letters.

* Module names starts with lowercase letters.

### Print Statement ###

#### Printing To A File ####

Using `file` argument of the print() function:
```python
>>> print("hello, world", file = open("hello.txt", "w"))
>>> open("hello.txt").read()
'hello, world\n'
```

Using `sys.stdout`:
```python
>>> import sys
>>> tmp = sys.stdout
>>> 
>>> sys.stdout = open("hello.txt", "w")
>>> print("hello, world!")
>>> 
>>> sys.stdout = tmp
>>> open("hello.txt").read()
'hello, world!\n'
```

### Pyhton If Statement ###

Structure:
```
if <test1>:
	<statement1>
elif <test2>:
	<statement2>
else:
	<statement3>
```

**No switch case** in python. Work around with if:
```python
>>> choice = 'gam'
>>> 
>>> if choice == 'spam':
...     print("0$")
... elif choice == 'ham':
...     print("1$")
... elif choice == 'gam':
...     print("2$")
... else:
...     print("Bad Choice!")
... 
2$
```

Example:
```python
>>> if 1:
...     print("One!")
... 
One!
>>> 
>>> if not 1:
...     print("One!")
... else:
...     print("None!")
... 
None!
```

Dictionary based work around (Less typing!):
```python
>>> choice = 'jam'
>>> 
>>> print({'spam': '0$',
...        'ham': '1$',
...        'gam': '2$'}.get(choice, 'Bad choice!'))
Bad choice!
```

#### Logical Operators in Python ####

`and` operator:
```python
if X and Y:			# True if X and Y both True
	# Do something
```

Return Value: `and` didn't return True or False. Returns first object which is
false(zero or empty) from left to right. If expression is true returns right most 
object.
```python
>>> 1 and 2
2
>>> [] and 2
[]
>>> 1 and [] and 2
[]
```

`or` operator:
```python
if X or Y:			# True if X or Y is True
	# Do something
```

Return value: `or` didn't return True or False. Returns first object which is true
(non-zero / non-empty) from left to right.
```python
>>> 2 or 3
2
>>> [] or 3
3
>>> {} or 3 or [] 
3
```

`not` operator:
```python
if not X:			# Invert logic
	# Do something
```

Return value: Returns True or False

#### if/else Ternary Expression ###

Consider following code:
```python
if X:
	A = Y
else:
	A = Z
```

**Ternary alternative:**
```python
A = Y if X else Z
```

### Python While Loop ###

#### While loop's general format ####

```
while <test1>:
	<statement1>
	if <test2>: break		# Exit loop now. Skip else part
	if <test3>: continue	# Continue to test1

else:						# Execute only if loop is exited without break
	<statement2>
```

**pass:** Do nothing. Just an empty statement place holder.

### Python For Loop ###

#### For loop's general format ####

```
for <target> in <object>/<sequence>:
	<statements>
	if <test>: break
	if <test>: continue
else:
	<statements>
```

* Any sequence works in for loop

```python
>>> for i in [1, 2, 3]:
...     print(i, end = '\t')
... else:
...     print("")
... 
1	2	3	
>>> 
>>> for ch in "abc":
...     print(ch, end = '\t')
... else:
...     print("")
... 
a	b	c
```

#### Tupple assignment / Sequence Unpacking in for loop ####

```python
>>> for (a, b) in [(1, 2), (3, 4)]:
...     print("%d, %d" % (a, b))
... 
1, 2
3, 4
```

#### Some sequence unpacking example ####

```python
>>> for ((a, b), c) in [((1, 2), 3), ((4, 5), 6)]:
...     print(a, b, c)
... 
1 2 3
4 5 6
>>> for ((x, y), z) in [((1, 2), 3), ("XY", 'Z')]:
...     print(x, y, z)
... 
1 2 3
X Y Z
```

#### Using for loop for iterating through dictionary ####

```python
>>> dict = {1: 'a', 2: 'b', 3: 'c'}
>>> for key in dict.keys():
...     print("Key: %d\tValue: %c" % (key, dict[key]))
... 
Key: 1	Value: a
Key: 2	Value: b
Key: 3	Value: c
>>> 
>>> for key, value in list(dict.items()):
...     print(key, value)
... 
1 a
2 b
3 c
```

#### Using Range ####

`range(FROM, UPTO, STEP)` - Create a list of numbers FROM to UPTO in python 2.0. In python 3.0 it's an iterator.

**Example:**
```python
# Python 2.0

>>> range(0, 10)
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>>
>>> range(0, 10, 2)
[0, 2, 4, 6, 8]

# Python 3.0

>>> list(range(0, 10))
[0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
>>>
>>> list(range(0, 10, 2))
[0, 2, 4, 6, 8]
```

Range items can be negative numbers and can be in reverse order.

```python
>>> list(range(8, 0, -1))
[8, 7, 6, 5, 4, 3, 2, 1]
>>>
>>> list(range(4, -4, -1))
[4, 3, 2, 1, 0, -1, -2, -3]
```

Range can be used as a iterator in for loops.

```python
>>> X = "abcdefgh"
>>> for i in range(0, len(X), 2):
...     print(X[i], end = '')
... else:
...     print()
... 
aceg

# Alternative good solution is with sclicing

>>> X
'abcdefgh'
>>> for ch in X[::2]:
...     print(ch, end = '')
... else:
...     print()
... 
aceg
```

## Python Keywords and Symbols ##

### At a Glance ###

* `[]`    - Make a list.
* `{}`    - Make a dictionary.
* `()`    - Make a Touple.
* `if`    - if block
* `else`  - else block
* `while` - While loop
* `in`    - Membership check
* 'not'   - Logical not
* 'and'   - Logical and
* 'or'    - Logical or


## Tricks ##

### List All Attributes of an Object ###

`dir()` function returns a list of all the attributes of an objetc.
```python
>>> s = "I am a string"
>>> dir(s)
['__add__', '__class__', '__contains__', '__delattr__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__getnewargs__', '__getslice__', '__gt__', '__hash__', '__init__', '__le__', '__len__', '__lt__', '__mod__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__rmod__', '__rmul__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '_formatter_field_name_split', '_formatter_parser', 'capitalize', 'center', 'count', 'decode', 'encode', 'endswith', 'expandtabs', 'find', 'format', 'index', 'isalnum', 'isalpha', 'isdigit', 'islower', 'isspace', 'istitle', 'isupper', 'join', 'ljust', 'lower', 'lstrip', 'partition', 'replace', 'rfind', 'rindex', 'rjust', 'rpartition', 'rsplit', 'rstrip', 'split', 'splitlines', 'startswith', 'strip', 'swapcase', 'title', 'translate', 'upper', 'zfill']
```

details of an object's methods or attributes can be found using `help()` function.

```python
>>> help(s.join)
Help on built-in function join:

join(...)
    S.join(iterable) -> string

    Return a string which is the concatenation of the strings in the
    iterable.  The separator between elements is S.
