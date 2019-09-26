## INDEX ##
1. [Command Line Arguments](https://github.com/aagontuk/cheatsheets/blob/master/bash.md#command-line-arguments)
2. [Conditional Statement](https://github.com/aagontuk/cheatsheets/blob/master/bash.md#conditional-statement)
3. [`case` Statement](https://github.com/aagontuk/cheatsheets/blob/master/bash.md#case-statement)
4. [Looping](https://github.com/aagontuk/cheatsheets/blob/master/bash.md#looping)
    1. [For Loop](https://github.com/aagontuk/cheatsheets/blob/master/bash.md#for-loop)
    2. [While Loop](https://github.com/aagontuk/cheatsheets/blob/master/bash.md#while-loop)
    3. [Until](https://github.com/aagontuk/cheatsheets/blob/master/bash.md#until)
    4. [break and continue statements](https://github.com/aagontuk/cheatsheets/blob/master/bash.md#break-and-continue)
5. [Exit Staus](https://github.com/aagontuk/cheatsheets/blob/master/bash.md#exit-status)

## Command Line Arguments ##
```sh
echo "Number of arguments given: $#"

number=1
while [ "$1" != "" ]; do
    echo "Argument $number: $1"
    number=$((number + 1))
    shift
done
```

## Conditional Statement ##
```sh
# if-else structure
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

## `case` Statement ##
```sh
# if-else structure
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

## Looping ##

### For Loop ###
```sh
# Structure of the for loop
# for $variable in sequence; do
#	something with the variables
# done

for f in $(ls); do
		echo $f
done
```

### While Loop ###
```sh
# Structure of while loop
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
```sh
number=0

until [ $number -gt 10 ]; do
		echo "Number $number"
		number=$((number + 1))
done
```

### break and continue ###
Like any other programming languages `break` and `continue`
statement can be applied in a loop

## Exit Status ##
```sh
touch
echo $?
```
