# Index

## Structure

```bash
awk 'BEGIN{ACTION} PATTERN{ACTION} END{ACTION}'
```

## Printing

```bash
awk 'BEGIN{print "hello", "world"}'   # hello world
awk 'BEGIN{print "hello" "world"}'   # helloworld
awk 'BEGIN{print "hello"; print "world"}'   # hello\nworld
awk 'BEGIN{printf "%s","hello"; printf "%s","world"}'   # helloworld
```

## Using bash variable inside awk

### Quoting

```bash
#!/bin/bash

var=4
awk 'BEGIN{print '$var'}'
```

### Commandline

```bash
#!/bin/bash

var=4
awk -v v=$var 'BEGIN{print v}'
```

```bash
#!/bin/bash

var=4
car=5
awk -v v=$var -v c=$car 'BEGIN{print v,c}'
```

## Summary of programming constructs in awk

```
if ( conditional ) statement [ else statement ]
while ( conditional ) statement
for ( expression ; conditional ; expression ) statement
for ( variable in array ) statement
break
continue
{ [ statement ] ...}
variable=expression
print [ expression-list ] [ > expression ]
printf format [ , expression-list ] [ > expression ]
next
exit
```

Example:

```bash
#!/bin/bash

echo "AWK example:"

awk '
BEGIN{
    start=1;
    end=10;

    for(i=start; i <= end; i++) {
        if (i % 2 == 0) {
            print i;
        }
    }
}
'
```

## Regular Expression match 

`~` can be used to check if a string matches a regular expression. And `!~` will evaluate to true if a string
doesn't match with a regular expression.

```bash
#!/bin/bash

awk 'BEGIN{word="other";if(word ~ /the/){print "match"}}'
```

## AWK builtin variables

* FS - Input field seperator
* OFS - Output field seperator
* RS - Inpute record field seperator
* ORS - Output record field seperator
* NF - Number of fields/columns
* NR - record number/line number
* FILENAME - Name of the file being read
