## Intro ##

### Hello world! ###

```rs
fn main() {
	println!("Hello, world!");
}
```

### Language Overview ###

Overview of the language with a guessing game program:

```rs
use std::io;
use rand::Rng;
use std::cmp::Ordering;

fn main() {
    println!("NEW GAME: Guess a number!");

    let rnum = rand::thread_rng().gen_range(1..=100);

    println!("Secret number: {rnum}");

    loop {
        println!("Enter your number:");

        let mut guess = String::new();
        io::stdin().read_line(&mut guess).expect("Failed to read line");

        let guess: u32 = match guess.trim().parse() {
           Ok(num) => num,
           Err(_) => continue,
        };

        match guess.cmp(&rnum) {
            Ordering::Less => println!("Too small!"),
            Ordering::Greater => println!("Too big!"),
            Ordering::Equal => {
                println!("You win!");
                break;
            }
        }
    }
}
```

## Common Programming Concepts ##

### Variables and mutability ###

* Variables are by default immutable. Use `mut` keyword to make it mutable.

```rs
let x = 5;
x = x + 1 // Error: x is immutable

let mut y = 10;
y = y * 2 // Correct
```

* Use const keyword to specify constants. Must annotate type.

```rs
fn main() {
    const LIGHT_SPEED: f64 = 3e8;
    println!("Light speed: {LIGHT_SPEED}");
}
```

* Redefining variables shadows the old variable.

```rs
fn main() {
    let x = 5;

    let x = x + 1; // Shadowed old x. x is now 6 and still immutable

    {
        let x = x * 2;
        println!("The value of x in the inner scope is: {x}"); // Will print 12
    }

    println!("The value of x is: {x}"); // Will print 6 as outer scopped value is 6
}
```

### Data Types ###

#### Scalar Types ####

* Integer data types: i8, u8, i32, u32, i64, u64, i128, u128, isize, usize.
	Default i32.
* Floating point types: f32, f64. Default f64.
* Boolean type: true, false.
* Char type: 'x'. 4 bytes, so unicode char is also supported. `let x: char = 'x'`.

#### Compound Types ####

Tuples:

* Fixed size in compile time.
* Can contain different types.
* Use `vaiable_name.INDEX` to specify individual elements: INDEX starts from 0.

```rs
let tup = (500, 'x', 10.5);
let (x, y, z) = tup; // Destructuring

println!("2nd value is {y}");

// You can also index specific elements
let second_value = tup.1;
println!("2nd value is {second_value}");
```

Array:

* Contains elements of fixed types.

```rs
let a = [1, 2, 3, 4, 5];
let a: [i32; 5] = [1, 2, 3, 4, 5]; // With size and type annotated
let a = [3; 5]; // 5 elements as 3
```

### Functions ###

```rs
fn main() {
    let x = plus_one(5);

    println!("The value of x is: {x}");
}

fn plus_one(x: i32) -> i32 {
    x + 1
}
```

#### Statements vs Expressions ####

* Expressions evaluate to values.
* Expressions doesn't end with semicolon.
* Expressions can be converted to statements by using semicolon at the end.
* Function return is specified using expressions in rust.

### Control Flow ###

#### if/else ####

* Condition must be boolean

```rs
fn main() {
    let number = 6;

    if number % 4 == 0 {
        println!("number is divisible by 4");
    } else if number % 3 == 0 {
        println!("number is divisible by 3");
    } else if number % 2 == 0 {
        println!("number is divisible by 2");
    } else {
        println!("number is not divisible by 4, 3, or 2");
    }
}
```

* If is an expression so can be used in let statement

```rs
fn main() {
    let condition = true;
    let number = if condition { 5 } else { 6 };

    println!("The value of number is: {number}");
}
```

#### Looping ####

`loop` keyword:

* Loops indefinitely.
* break can use expression to return value.
* Loops can be named and used in break

Example: `break` with expression
```rs
fn main() {
    let mut counter = 0;

    let result = loop {
        counter += 1;

        if counter == 10 {
            break counter * 2;
        }
    };

    println!("The result is {result}");
}
```

Example: named loop

```rs
fn main() {
    let mut count = 0;
    'counting_up: loop {
        println!("count = {count}");
        let mut remaining = 10;

        loop {
            println!("remaining = {remaining}");
            if remaining == 9 {
                break;
            }
            if count == 2 {
                break 'counting_up;
            }
            remaining -= 1;
        }

        count += 1;
    }
    println!("End count = {count}");
}
```

`while` keyword:

```rs
fn main() {
    let mut number = 3;

    while number != 0 {
        println!("{number}!");

        number -= 1;
    }

    println!("LIFTOFF!!!");
}
```

`for` keyword:

* Used to loop through a collection:

Example 1:
```rs
fn main() {
    let a = [10, 20, 30, 40, 50];

    for element in a {
        println!("the value is: {element}");
    }
}
```

Example 2:
```rs
fn main() {
    for number in (1..4).rev() {
        println!("{number}!");
    }
    println!("LIFTOFF!!!");
}
```
