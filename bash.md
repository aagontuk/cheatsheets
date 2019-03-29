## INDEX ##

## Command Line Arguments ##
```
echo "Number of arguments given: $#"

number=1
while [ "$1" != "" ]; do
    echo "Argument $number: $1"
    number=$((number + 1))
    shift
done
```

## Conditional Statement ##
```
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

## Switch-Case ##
```
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
```
# Structure of the for loop
# for $variable in sequence; do
#	something with the variables
# done

for f in $(ls); do
		echo $f
done
```

### While Loop ###
```
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
```
number=0

until [ $number -gt 10 ]; do
		echo "Number $number"
		number=$((number + 1))
done
```

## Exit Status ##
```
touch
echo $?
```
