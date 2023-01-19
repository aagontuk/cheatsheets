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
  Loop labels must begin with a single quote.

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
		// Loop label have to start with '
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

## Ownership in Rust ##

### Ownership Rules ###

* Each value in Rust has an owner.
* There can only be one owner at a time.
* When the owner goes out of scope, the value will be dropped.

In rust the memory is automatically returned
once the variable that owns it goes out of scope.
When a variable goes out of scope rust calls a special
method `drop()`. This is implemented on the specific type.
This function is responsible for cleaning up memory
for that type.

### Variables and Data Interacting with Move ###

Rust always do shallow copy.

```rs
	let s1 = String::from("hello");
	// s1 and s2 are pointing to the same data
	// as data isn't copied.
	//
	// s1's ownership is moved to s2. s1 no longer valid
	let s2 = s1;

	println!("{}, world!", s1); // Won't compile s1 not valid
```

### Variables and Data Interacting with Clone ###

It is possible to do deep copy with `clone()` method.

```rs
	let s1 = String::from("hello");
	let s2 = s1.clone();

	println!("s1 = {}, s2 = {}", s1, s2);
```

### Ownership and Functions ###

Ownership is also move in function parameters:

```rs
fn main() {
    let s = String::from("hello");  // s comes into scope

    takes_ownership(s);             // s's value moves into the function...
                                    // ... and so is no longer valid here

    let x = 5;                      // x comes into scope

    makes_copy(x);                  // x would move into the function,
                                    // but i32 is Copy, so it's okay to still
                                    // use x afterward

		// This won't compile as ownership is moved
		println!("String {s}");

} // Here, x goes out of scope, then s. But because s's value was moved, nothing
  // special happens.

fn takes_ownership(some_string: String) { // some_string comes into scope
    println!("{}", some_string);
} // Here, some_string goes out of scope and `drop` is called. The backing
  // memory is freed.

fn makes_copy(some_integer: i32) { // some_integer comes into scope
    println!("{}", some_integer);
} // Here, some_integer goes out of scope. Nothing special happens.
```

### Return Values and Scope ###

* Return values can also transfer ownership

```rs
fn main() {
    let s1 = gives_ownership();         // gives_ownership moves its return
                                        // value into s1

    let s2 = String::from("hello");     // s2 comes into scope

    let s3 = takes_and_gives_back(s2);  // s2 is moved into
                                        // takes_and_gives_back, which also
                                        // moves its return value into s3
} // Here, s3 goes out of scope and is dropped. s2 was moved, so nothing
  // happens. s1 goes out of scope and is dropped.

fn gives_ownership() -> String {             // gives_ownership will move its
                                             // return value into the function
                                             // that calls it

    let some_string = String::from("yours"); // some_string comes into scope

    some_string                              // some_string is returned and
                                             // moves out to the calling
                                             // function
}

// This function takes a String and returns one
fn takes_and_gives_back(a_string: String) -> String { // a_string comes into
                                                      // scope

    a_string  // a_string is returned and moves out to the calling function
}
```

### Reference and Borrowing ###

To use functions with parameters you need
to give ownership of the parameters to the
function and then return it back:

```rs
fn main() {
    let s1 = String::from("hello");

    let (s2, len) = calculate_length(s1);

    println!("The length of '{}' is {}.", s2, len);
}

fn calculate_length(s: String) -> (String, usize) {
    let length = s.len(); // len() returns the length of a String

    (s, length)
}
```

To remove this hassle one can use references to refer
to some value without taking ownership. This is called
borrowing in rust terminology.

```rs
fn main() {
    let s1 = String::from("hello");

    let len = calculate_length(&s1);

    println!("The length of '{}' is {}.", s1, len);
}

fn calculate_length(s: &String) -> usize {
    s.len()
}
```

`&` is used to specify references.

To change the value of the variable that
a reference is pointing to, the reference also
need to be mutable. For example following code
won't compile:

```rs
fn main() {
    let s = String::from("hello");

    change(&s);
}

// The reference some_string isn't mutable
// so it won't compile as it is changing
// the value of the variable it is poiting to.
fn change(some_string: &String) {
    some_string.push_str(", world");
}
```

Use `mut` keyword to specify mutable reference:

```rs
fn main() {
    let mut s = String::from("hello");

    change(&mut s);

		println!("{}", s);
}

fn change(some_string: &mut String) {
    some_string.push_str(", world");
}
```

Rules for mutable references:
* There can be as many as immutable references.
* There can be only one mutable reference simultaneously.
* Mutable reference can't be mixed up with immutable reference
	as immutable reference is expecting value won't change.
* This restrictions are given to remove data race at compile time.

Example 1: This won't compile as two mutable reference
of the same variable.
```rs
fn main() {
    let mut s = String::from("hello");

    let r1 = &mut s;
    let r2 = &mut s;

    println!("{}, {}", r1, r2);
}
```

Example 2:
```rs
fn main() {
    let mut s = String::from("hello");

    {
        let r1 = &mut s;
    } // r1 goes out of scope here, so we can make a new reference with no problems.

    let r2 = &mut s;
}
```

Example 3:
```rs
fn main() {
    let mut s = String::from("hello");

    let r1 = &s; // no problem
    let r2 = &s; // no problem
    let r3 = &mut s; // BIG PROBLEM

    println!("{}, {}, and {}", r1, r2, r3);
}
```

Example 4:
```rs
fn main() {
    let mut s = String::from("hello");

    let r1 = &s; // no problem
    let r2 = &s; // no problem
    println!("{} and {}", r1, r2);
    // variables r1 and r2 will not be used after this point

    let r3 = &mut s; // no problem
    println!("{}", r3);
}
```

### Dangling References ###

It is not possible to create dangling references
in rust. Compiler does a lifetime analysis and will
be caught.

This will not compile and give compiler error:
```rs
fn main() {
    let reference_to_nothing = dangle();
}

fn dangle() -> &String {
    let s = String::from("hello");

    &s
}
```

### The Rules of References ###

* At any given time, you can have either one mutable
reference or any number of immutable references.

* References must always be valid.

## Slice Type ##

Slices are a kind of reference which points
to a portion of a value.

`&str` - type of string slice.
`&[i32]` - Type of i32 array slice.
`&[T]` - Type of slice of array of type T.

### String Slices ###

Type of string slice is `&str`

Example 1:
```rs
#![allow(unused)]
fn main() {
    let s = String::from("hello world");

    let hello = &s[0..5];
    let world = &s[6..11];
}
```

Example 2:
```rs
#![allow(unused)]
fn main() {
let s = String::from("hello");

let slice = &s[0..2];
let slice = &s[..2];
}
```

Example 3:
```rs
#![allow(unused)]
fn main() {
let s = String::from("hello");

let len = s.len();

let slice = &s[3..len];
let slice = &s[3..];
}
```

Example 4:
```rs
#![allow(unused)]
fn main() {
let s = String::from("hello");

let len = s.len();

let slice = &s[0..len];
let slice = &s[..];
}
```

Example 5:
```rs
fn first_word(s: &String) -> &str {
    let bytes = s.as_bytes();

    for (i, &item) in bytes.iter().enumerate() {
        if item == b' ' {
            return &s[0..i];
        }
    }

    &s[..]
}

fn main() {
    let mut s = String::from("hello world");

    let word = first_word(&s);

    s.clear(); // error!

    println!("the first word is: {}", word);
}
```

## Structs ##

### Defining and Instantiating Structs ###

Definition:
```rs
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}
```

Using the struct:
```rs
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn main() {
    let user1 = User {
        email: String::from("someone@example.com"),
        username: String::from("someusername123"),
        active: true,
        sign_in_count: 1,
    };
}
```

Specific field is specified using the dot notation:
```rs
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn main() {
		// All the fields are mutable now
    let mut user1 = User {
        email: String::from("someone@example.com"),
        username: String::from("someusername123"),
        active: true,
        sign_in_count: 1,
    };

    user1.email = String::from("anotheremail@example.com");
}
```

* It's not possible to set a specific field as mutable.
All the fields have to be mutable.

Struct instantiation is an expression so it is possible to use
as functions return:
```
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn build_user(email: String, username: String) -> User {
    User {
        email: email,
        username: username,
        active: true,
        sign_in_count: 1,
    }
}

fn main() {
    let user1 = build_user(
        String::from("someone@example.com"),
        String::from("someusername123"),
    );
}
```

### Using the Field Init Shorthand ###

If field name and parameter name is same
then you don't need to specify field names:

```rs
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn build_user(email: String, username: String) -> User {
    User {
        email,
        username,
        active: true,
        sign_in_count: 1,
    }
}

fn main() {
    let user1 = build_user(
        String::from("someone@example.com"),
        String::from("someusername123"),
    );
}
```

### Creating Instances From Other Instances With Struct Update Syntax ###

The syntax .. specifies that the remaining fields
not explicitly set should have the same value as
the fields in the given instance:
```rs
struct User {
    active: bool,
    username: String,
    email: String,
    sign_in_count: u64,
}

fn main() {
    // --snip--

    let user1 = User {
        email: String::from("someone@example.com"),
        username: String::from("someusername123"),
        active: true,
        sign_in_count: 1,
    };

    let user2 = User {
        email: String::from("another@example.com"),
        ..user1
    };
}
```

**Update syntax uses move semantics. So if any of the fields
uses move semantic then the ownership will be moved.
For example user1 will be invalid
after using the update syntaxt on user2.
as email and username field ownership will be moved**

### Using Tuple Structs without Named Fields to Create Different Types ###

```rs
struct Color(i32, i32, i32);
struct Point(i32, i32, i32);

fn main() {
    let black = Color(0, 0, 0);
    let origin = Point(0, 0, 0);
}
```

### Unit-Like Structs Without Any Fields ###

Unit-like structs can be useful when you need to
implement a trait on some type but don’t have any data
that you want to store in the type itself

```rs
struct AlwaysEqual;

fn main() {
    let subject = AlwaysEqual;
}
```

### Ownership of Struct Data ###

To use a reference in a struct field you
need to specifiy lifetime to make sure
that the reference will be valid as long as
the struct is valid.

### Defining methods of a struct ###

```rs
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
		// &self is short for self: &self
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };

    println!(
        "The area of the rectangle is {} square pixels.",
        rect1.area()
    );
}
```

**Rust doesn’t have an equivalent to the -> operator;
instead, Rust has a feature called automatic referencing and dereferencing.**

### Methods with More Parameters ###

```
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }

    fn can_hold(&self, other: &Rectangle) -> bool {
        self.width > other.width && self.height > other.height
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };
    let rect2 = Rectangle {
        width: 10,
        height: 40,
    };
    let rect3 = Rectangle {
        width: 60,
        height: 45,
    };

    println!("Can rect1 hold rect2? {}", rect1.can_hold(&rect2));
    println!("Can rect1 hold rect3? {}", rect1.can_hold(&rect3));
}
```

### Associated Functions ###

* All functions defined within an impl block are called
associated functions because they’re associated with
the type named after the impl.

* We can define associated functions that don’t have
self as their first parameter.

* Associated functions that aren’t methods are often
used for constructors that will return a new instance of the struct.

* To call this associated functions we use :: after struct name.

```rs
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn square(size: u32) -> Self {
        Self {
            width: size,
            height: size,
        }
    }
}

fn main() {
    let sq = Rectangle::square(3);
}
```

It is allowed to have multiple impl block for the
same struct.

```rs
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn area(&self) -> u32 {
        self.width * self.height
    }
}

impl Rectangle {
    fn can_hold(&self, other: &Rectangle) -> bool {
        self.width > other.width && self.height > other.height
    }
}

fn main() {
    let rect1 = Rectangle {
        width: 30,
        height: 50,
    };
    let rect2 = Rectangle {
        width: 10,
        height: 40,
    };
    let rect3 = Rectangle {
        width: 60,
        height: 45,
    };

    println!("Can rect1 hold rect2? {}", rect1.can_hold(&rect2));
    println!("Can rect1 hold rect3? {}", rect1.can_hold(&rect3));
}
```
