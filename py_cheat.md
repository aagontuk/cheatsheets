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

`repr()` display numbers as in code.
`str()` coverts into more user friendly looks.
`oct()` converts decimal into octal
`hex()` converts decimal into hexadecimal
`int(string, base)` converts strings into numbers.


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
---
1. Single Quotes: 'he said, "hello"'
2. Double Quotes: "Robin's book"
3. Block of strings: """string block""", '''String Block'''
4. Raw strings: r'\thello, world\n'
5. Unicode strings: u'\u0986\u09AE\u09BE\u09B0'
---

```python
>>> print 'he said, "hello"'
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
`chr(value)` convert from ASCII to character.

#### String Formating ####

```python
>>> print "%s:%d\t%s:%d" % ("Alice", 40, "Bob", 50)
Alice:40	Bob:50
>>>
>>>print "My List: %s" % [1, 2, 3]
My List: [1, 2, 3]
```



















