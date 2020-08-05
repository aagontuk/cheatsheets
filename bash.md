## INDEX ##
1. [Introduction](https://github.com/aagontuk/cheatsheets/blob/master/bash.md#introduction)
2. [Commenting](https://github.com/aagontuk/cheatsheets/blob/master/bash.md#commenting)
1. [Conditional Statements](https://github.com/aagontuk/cheatsheets/blob/master/bash.md#conditional-statements)
2. [`case` Statement](https://github.com/aagontuk/cheatsheets/blob/master/bash.md#case-statement)
3. [Looping](https://github.com/aagontuk/cheatsheets/blob/master/bash.md#looping)
    1. [For Loop](https://github.com/aagontuk/cheatsheets/blob/master/bash.md#for-loop)
    2. [While Loop](https://github.com/aagontuk/cheatsheets/blob/master/bash.md#while-loop)
    3. [Until](https://github.com/aagontuk/cheatsheets/blob/master/bash.md#until)
    4. [break and continue statements](https://github.com/aagontuk/cheatsheets/blob/master/bash.md#break-and-continue)
4. [Array](https://github.com/aagontuk/cheatsheets/blob/master/bash.md#array)
5. [Command Line Arguments](https://github.com/aagontuk/cheatsheets/blob/master/bash.md#command-line-arguments)
6. [Exit Staus](https://github.com/aagontuk/cheatsheets/blob/master/bash.md#exit-status)

## Introduction ##

All shell script files start with `#!/bin/bash` line.
This is called a shebang. This tells which interpreter
should call to parse the script. Example of a shell
script file:

```sh
#!/bin/bash

echo "hello, world"
```

## Commenting ##

Any line begin with `#` is a comment.

```sh
#!/bin/bash

# This is a comment
echo "hello, world"     # This is a comment too
```

## Conditional Statements ##

Following example will show conditional statements in shell scripting

```sh
#!/bin/bash

# Structure
#
# if [ Expression ]; then
#       do something
# elif [ Expression ]; then
#       do something else
# else
#       do something else
# fi

number=2

if [ $number -lt "2" ]; then
    echo "Less than 2"
elif [ $number -gt "2" ]; then
    echo "Greater than 2"
else
    echo "Equal to 2"
fi
```

To see how to write the conditional expressions see `man test`.

## `case` Statement ##

case statements has the following form:

```
case $variable in
    pattern1)
        do something
    ;;

    pattern2)
        do something else
    ;;

    pattern3 | pattern4)
        do third important work
    ;;

    *)
        do another thing
    ;;
esac
```

* `|` matches multiple patterns.
* `*` default action if no pattern matches.

Example:

```
#!/bin/bash

# A program to do some usefull things with unix tools

TOOL=shell

case $TOOL in
    shell)
        echo "Throw into the sea."
    ;;

    strip)
        echo "Jump into the water."
    ;;

    time)
        echo "Jump in a black hole"
    ;;

    sleep)
        echo "Now do a interstellar travel"
    ;;

    *)
        echo "You are in a limbo"
    ;;
esac
```

## Looping ##

### For Loop ###
```sh
#!/bin/bash

# Structure of the for loop
#
# for $variable in sequence; do
#	something with the variables
# done

for f in $(ls); do
    echo $f
done
```

### While Loop ###

Executes while a condition is true.

```sh
#!/bin/bash

# Structure of while loop
#
# while [ Expression ]; do
#	do something
# done

number=0

while [ $number -lt 10 ]; do
    echo "Number: $number"
    number=$((number + 1))
done
```

### Until ###

Executes until a condition is true.

```sh
number=0

until [ $number -gt 10 ]; do
    echo "Number $number"
    number=$((number + 1))
done
```

### break and continue ###
Like any other programming languages `break` and `continue`
statement can be applied in a loop to break the loop or continue
the loop on some condition.

## Array ##

Arrays are defined as `array_name=(0 "name" 4)`
where `array_name` is the name of the array
an `0`, `name` are the elements of the array.
Array can be subscripted and iterated in following
way:

```sh
array_name=(0, "name", 4)

# Print first element of the array
echo ${array_name[1]}

# Iterating through the array
# Print all the elements of the array
for elem in ${array_name[@]}; do
    echo $elem
done
```

## Command Line Arguments ##
sample code:
```sh
#!/bin/bash

echo "Number of arguments: '$#'"
echo "All arguments(space seperated): '$@'"
echo "Program name: '$0'"
echo "Argument 1: '$1'"
echo "Argument 2: '$2'"
```
sample output:
```
Number of arguments: '2'
All arguments(space seperated): 'hello world'
Program name: './cmd.sh'
Argument 1: 'hello'
Argument 2: 'world'
```
sample code:
```sh
echo "Number of arguments given: $#"

number=1
while [ "$1" != "" ]; do
    echo "Argument $number: $1"
    number=$((number + 1))      # number+=1
    shift
done
```
sample output:
```
Number of arguments given: '2'
Argument 1: hello
Argument 2: world
```

## Exit Status ##
```sh
touch
echo $?
```
