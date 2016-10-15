## Python Object Types ##

### Python Data Types ###

| Object Type | Example                                                   |
| :---------- | --------------------------------------------------------: |
| Numbers     | 1.23, 123, 3+4i											  |
| Strings     | "hello, world"											  |
| Lists       | [1, 'hello', ['I', 'am', 'list', 'in', 'a', 'list'], 4.5] |
| Dictionary  | {"key":"value", 'foo':0, 'bar':'drink'}					  |
| Tuples      | (4, 'hello', 3.14)										  |
| Others      | set, types, booleans, none								  |

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

## Python Data Types In Detail ##

### Numbers ##

#### Numeric Display Formats ####

`repr()` display numbers as in code.				</br>
`str()` coverts into more user friendly looks.		</br>
`oct()` converts decimal into octal					</br>
`hex()` converts decimal into hexadecimal			</br>
`int(string, base)` converts strings into numbers.	</br>


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
4. Raw strings: r'\thello, world\n'
5. Byte Strings: b'spam'	**(Python 3)**
6. Unicode strings: u'\u0986\u09AE\u09BE\u09B0' **(in 2.6 only)**

In python 3 there are three string types. `str` is used for unicode text(ASCII and others). `bytes` is used
for bynary data. `bytearray` is mutable variant of bytes.


```python
>>> print 'he said, "hello"'	\\ Python 2.6
he said, "hello"
>>> print ('he said, "hello"')	\\ Have to use brackets in python 3
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

```python
>>> print "%s:%d\t%s:%d" % ("Alice", 40, "Bob", 50)
Alice:40	Bob:50
>>>
>>>print "My List: %s" % [1, 2, 3]
My List: [1, 2, 3]
```

| Format Code	| Meaning 					|
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

**Dictionary base string formating:** "%(name)s has %(value)d taka" % {'name':'ashik', 'value':50}

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

### Tupples ###

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
|: ----: | -------------------------------------------------------- |
| r      | open file in read mode. Default, if nothing specified.	|
| w		 | Open file in write mode.									|
| a		 | Open file in append mode									|

#### Methods ####

* `file.write(str)` - write a string to a file.
```python
>>> outf = open('myfile', 'w')
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

#### Python Shelve ####

#### Packed Binary ####












