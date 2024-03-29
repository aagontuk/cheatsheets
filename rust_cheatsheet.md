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

## Enum and Pattern Matching ##

### Defining Enum ###

```rs
enum IpAddrKind {
    V4,
    V6,
}

fn main() {
    let four = IpAddrKind::V4;
    let six = IpAddrKind::V6;

    route(IpAddrKind::V4);
    route(IpAddrKind::V6);
}

fn route(ip_kind: IpAddrKind) {}
```

Enum's can have data in them.
Consider following example:

```rs
fn main() {
    enum IpAddrKind {
        V4,
        V6,
    }

    struct IpAddr {
        kind: IpAddrKind,
        address: String,
    }

    let home = IpAddr {
        kind: IpAddrKind::V4,
        address: String::from("127.0.0.1"),
    };

    let loopback = IpAddr {
        kind: IpAddrKind::V6,
        address: String::from("::1"),
    };
}
```

This same program can be expresses with:

```rs
fn main() {
    enum IpAddr {
        V4(String),
        V6(String),
    }

    let home = IpAddr::V4(String::from("127.0.0.1"));

    let loopback = IpAddr::V6(String::from("::1"));
}
```

### Methods on Enums ###

Similar to structs it is possible to implement
method on enums:

```rs
fn main() {
    enum Message {
        Quit,
        Move { x: i32, y: i32 },
        Write(String),
        ChangeColor(i32, i32, i32),
    }

    impl Message {
        fn call(&self) {
            // method body would be defined here
        }
    }

    let m = Message::Write(String::from("hello"));
    m.call();
}
```

### The `Option` Enum and Its Advantages Over Null Values ###

* Rust doesn't have NULL

* The `Option` type encodes the scenario in which
a value could be something or it could be nothing.

* Expressing this concept in terms of the type system
means the compiler can check whether you’ve handled
all the cases you should be handling

* `Option` is implemented as following enum:
```rs
enum Option<T> {
    None,
    Some(T),
}
```

Example:
```rs
fn main() {
    let some_number = Some(5);
    let some_char = Some('e');

    let absent_number: Option<i32> = None;
}
```

* `Option<T>` can be used with `T`. `Option<T>` can
be converted to `T` by handling null case.

Example:
```rs
fn main() {
    let five = Some(5);
    let six = plus_one(five);
    let none = plus_one(None);
}
    
fn plus_one(x: Option<i32>) -> Option<i32> {
		match x {
				None => None,
				Some(i) => Some(i + 1),
		}
}
```

### The `match` Control Flow Construct ###

* Can be used to compare a value agains a
series of patters and execute code based
on the pattern matched.

* This confirms the compiler that all possible
cases are handled.

* Each pattern is called an arm

Example:
```rs
enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter,
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter => 25,
    }
}

fn main() {}
```

Another Example 2:
```rs
#[derive(Debug)]
enum UsState {
    Alabama,
    Alaska,
    // --snip--
}

enum Coin {
    Penny,
    Nickel,
    Dime,
    Quarter(UsState),
}

fn value_in_cents(coin: Coin) -> u8 {
    match coin {
        Coin::Penny => 1,
        Coin::Nickel => 5,
        Coin::Dime => 10,
        Coin::Quarter(state) => {
            println!("State quarter from {:?}!", state);
            25
        }
    }
}

fn main() {
    value_in_cents(Coin::Quarter(UsState::Alaska));
}
```

* Matches are exhaustive. You have to handle
all the possible cases.

### Catch-all Patterns and the `_` Placeholder ###

Example 1:
```rs
fn main() {
    let dice_roll = 9;
    match dice_roll {
        3 => add_fancy_hat(),
        7 => remove_fancy_hat(),
        other => move_player(other),
    }

    fn add_fancy_hat() {}
    fn remove_fancy_hat() {}
    fn move_player(num_spaces: u8) {}
}
```

* Rust will warn if any arm is specified after the catch all
pattern.

* It is possbile to use `_` to add a catch all pattern
but don't use the value.

```rs
fn main() {
    let dice_roll = 9;
    match dice_roll {
        3 => add_fancy_hat(),
        7 => remove_fancy_hat(),
        _ => reroll(),
    }

    fn add_fancy_hat() {}
    fn remove_fancy_hat() {}
    fn reroll() {}
}
```

* It also possible to take no action
for an arm:

```rs
fn main() {
    let dice_roll = 9;
    match dice_roll {
        3 => add_fancy_hat(),
        7 => remove_fancy_hat(),
        _ => (),
    }

    fn add_fancy_hat() {}
    fn remove_fancy_hat() {}
}
```

### Concise Control Flow with if let ###

* Works like reduced `match`. Only handle one case
and ignore all the other case.

Consider following code:
```rs
fn main() {
    let config_max = Some(3u8);
		// if config_max has value then print it
		// if it is None do nothing
    match config_max {
        Some(max) => println!("The maximum is configured to be {}", max),
        _ => (),
    }
}
```

This can be expressed more consciously with if/let combo:
```rs
fn main() {
    let config_max = Some(3u8);
		if let Some(max) = config_max {
				println!("Maximum value {max}");
		}
		else {
				println!("Maximum isn't set");
		}
}
```

## Common Collection ##

### Vectors ###

* Stores values of same type
* You must annotate the type while creating
a new vector.

```rs
let v: Vec<i32> = Vec::new();
```

* If initial values are provided rust will infer the type.

```rs
let v = vec![1, 2, 3];
```

* Updating a vecotr:

```rs
fn main() {
    let mut v = Vec::new();

    v.push(5);
    v.push(6);
    v.push(7);
    v.push(8);
}
```

* There are two ways to reference a value stored in a vector:
via indexing or using the get method. If get method is used
Option<&T> is returned.

```rs
fn main() {
    let v = vec![1, 2, 3, 4, 5];

    let third: &i32 = &v[2];
    println!("The third element is {third}");

    let third: Option<&i32> = v.get(2);
    match third {
        Some(third) => println!("The third element is {third}"),
        None => println!("There is no third element."),
    }
}
```

* Ownership and borrowing rules are applicable for references
to a vector. Following code won't compile:

```rs
fn main() {
    let mut v = vec![1, 2, 3, 4, 5];

    let first = &v[0];

    v.push(6);

    println!("The first element is: {first}");
}
```

* Iterating over the values of a vector:

Immutable reference:
```rs
fn main() {
    let v = vec![100, 32, 57];
    for i in &v {
        println!("{i}");
    }
}
```

Mutable reference: To change the value that the mutable reference
refers to, we have to use the * dereference operator to get to the value .
```rs
fn main() {
    let mut v = vec![100, 32, 57];
    for i in &mut v {
        *i += 50;
    }
}
```

* Using Enum to store multiple types: Vectors can only store values
that are the same type. Enums can be used as workaround for this.
With enum definitions different types can coexists in a vector.

```rs
fn main() {
    enum SpreadsheetCell {
        Int(i32),
        Float(f64),
        Text(String),
    }

    let row = vec![
        SpreadsheetCell::Int(3),
        SpreadsheetCell::Text(String::from("blue")),
        SpreadsheetCell::Float(10.12),
    ];
}
```

### Hashmap ###

* All keys have to be same type and
all values have to same type.

```rs
fn main() {
    use std::collections::HashMap;

    let mut scores = HashMap::new();

    scores.insert(String::from("Blue"), 10);
    scores.insert(String::from("Yellow"), 50);
}
```

* Accesing values in a hashmap: Values can be accesed
with `get` method. Get method returns `Options<&T>`.
`copied` method can be used to convert to `Options<T>`.
In the following example `unwrap_or` is used to convert
the value to 0 if returned value is None (If no such key).

```rs
fn main() {
    use std::collections::HashMap;

    let mut scores = HashMap::new();

    scores.insert(String::from("Blue"), 10);
    scores.insert(String::from("Yellow"), 50);

    let team_name = String::from("Blue");
    let score = scores.get(&team_name).copied().unwrap_or(0);
}
```

* Hashmap and ownership: For types that implement the Copy trait,
like i32, the values are copied into the hash map.
For owned values like String, the values will be moved and
the hash map will be the owner of those values

```rs
fn main() {
    use std::collections::HashMap;

    let field_name = String::from("Favorite color");
    let field_value = String::from("Blue");

    let mut map = HashMap::new();
    map.insert(field_name, field_value);
    // field_name and field_value are invalid at this point, try using them and
    // see what compiler error you get!
}
```

* Inserting a value for the same key will overwrite it's value

* Adding a Key and Value Only If a Key Isn’t Present:
`entry` method returns an enum `Entry` that represents
a value that might or might not exist. The `or_insert`
method on Entry is defined to return a mutable reference
to the value for the corresponding Entry key if that key exists,
and if not, inserts the parameter as the new value
for this key and returns a mutable reference to the new value.

```rs
fn main() {
    use std::collections::HashMap;

    let mut scores = HashMap::new();
    scores.insert(String::from("Blue"), 10);

    scores.entry(String::from("Yellow")).or_insert(50);
    scores.entry(String::from("Blue")).or_insert(50);

    println!("{:?}", scores);
}
```

* Updating a Value Based on the Old Value:

```rs
fn main() {
    use std::collections::HashMap;

    let text = "hello world wonderful world";

    let mut map = HashMap::new();

    for word in text.split_whitespace() {
        let count = map.entry(word).or_insert(0);
        *count += 1;
    }

    println!("{:?}", map);
}
```

## Error Handling ##

* Rust doesn't have execptions.
* `Result<T, E>` for recoverable errors.
* `panic!()` macro for unrecoverable erros.

### Recoverable Errors with Result ###

* Result Enum:
```rs
enum Result<T, E> {
		Ok(T),
		Err(E),
}
```

Example 1:
```rs
use std::fs::File;

fn main() {
    let greeting_file_result = File::open("hello.txt");

    let greeting_file = match greeting_file_result {
        Ok(file) => file,
        Err(error) => panic!("Problem opening the file: {:?}", error),
    };
}
```

Example 2:
```rs
use std::fs::File;
use std::io::ErrorKind;

fn main() {
    let greeting_file_result = File::open("hello.txt");

    let greeting_file = match greeting_file_result {
        Ok(file) => file,
        Err(error) => match error.kind() {
            ErrorKind::NotFound => match File::create("hello.txt") {
                Ok(fc) => fc,
                Err(e) => panic!("Problem creating the file: {:?}", e),
            },
            other_error => {
                panic!("Problem opening the file: {:?}", other_error);
            }
        },
    };
}
```

* Using closures to write above program without match syntax
```rs
use std::fs::File;
use std::io::ErrorKind;

fn main() {
    let greeting_file = File::open("hello.txt").unwrap_or_else(|error| {
        if error.kind() == ErrorKind::NotFound {
            File::create("hello.txt").unwrap_or_else(|error| {
                panic!("Problem creating the file: {:?}", error);
            })
        } else {
            panic!("Problem opening the file: {:?}", error);
        }
    });
}
```

### Shortcuts for Panic on Error: `unwrap` and `expect` ###

The unwrap method is a shortcut method implemented
just like the match expression. If the Result value is
the Ok variant, unwrap will return the value inside the Ok.
If the Result is the Err variant, unwrap will call the panic! macro

```rs
use std::fs::File;

fn main() {
    let greeting_file = File::open("hello.txt").unwrap();
}
```

* `expects` works like same but gives the ability
to write custom panic message:

```rs
use std::fs::File;

fn main() {
    let greeting_file = File::open("hello.txt")
        .expect("hello.txt should be included in this project");
}
```

### Propagating erros ###

Instead of handling function returns
error to the caller to handle:

```rs
#![allow(unused)]
fn main() {
use std::fs::File;
use std::io::{self, Read};

fn read_username_from_file() -> Result<String, io::Error> {
    let username_file_result = File::open("hello.txt");

    let mut username_file = match username_file_result {
        Ok(file) => file,
        Err(e) => return Err(e),
    };

    let mut username = String::new();

    match username_file.read_to_string(&mut username) {
        Ok(_) => Ok(username),
        Err(e) => Err(e),
    }
}
}

```

### A Shortcut for Propagating Errors: the `?` Operator ###

The ? placed after a Result value is defined to work
in almost the same way as the match expressions is
defined to handle the Result values.
If the value of the Result is an Ok,
the value inside the Ok will get returned from this expression,
and the program will continue. If the value is an Err,
the Err will be returned from the whole function as if
the return keyword is used so that the error value gets
propagated to the calling code.

There is a difference between what the match expression does
and what the ? operator does: error values that have the ? operator
called on them go through the from function, defined in the From trait
in the standard library, which is used to convert values from
one type into another. When the ? operator calls the from function,
the error type received is converted into the error type
defined in the return type of the current function.
This is useful when a function returns one error type to represent
all the ways a function might fail,
even if parts might fail for many different reasons.

```rs
#![allow(unused)]
fn main() {
use std::fs::File;
use std::io::{self, Read};

fn read_username_from_file() -> Result<String, io::Error> {
    let mut username_file = File::open("hello.txt")?;
    let mut username = String::new();
    username_file.read_to_string(&mut username)?;
    Ok(username)
}
}
```

This code can be made even shorter:

```rs
#![allow(unused)]
fn main() {
use std::fs::File;
use std::io::{self, Read};

fn read_username_from_file() -> Result<String, io::Error> {
    let mut username = String::new();

    File::open("hello.txt")?.read_to_string(&mut username)?;

    Ok(username)
}
}
```

> The ? operator can only be used in functions
whose return type is compatible with the value the ? is used on. 
This operator can be used in a function that returns Result, Option,
or another type that implements FromResidual.

> ? operator can be used on a Result in a function that returns Result,
and you can be use on an Option in a function that returns Option.

> To use ? in `main()` return type of main needs to be `Result<(), E>`:
```rs
std::error::Error;
use std::fs::File;

fn main() -> Result<(), Box<dyn Error>> {
    let greeting_file = File::open("hello.txt")?;

    Ok(())
}
```

## Generic Data Types ##

### In Function Definitions ###

Example 1: This won't compile as std::cmp::PartialOrd
trait isn't implemented:

```rs
fn largest<T>(list: &[T]) -> &T {
    let mut largest = &list[0];

    for item in list {
        if item > largest {
            largest = item;
        }
    }

    largest
}

fn main() {
    let number_list = vec![34, 50, 25, 100, 65];

    let result = largest(&number_list);
    println!("The largest number is {}", result);

    let char_list = vec!['y', 'm', 'a', 'q'];

    let result = largest(&char_list);
    println!("The largest char is {}", result);
}
```

### In Struct Definitions ###

Example 1:
```rs
struct Point<T> {
    x: T,
    y: T,
}

fn main() {
		// Both x and y have to be same type
		// as the struct definition has same
		// type T for both fields
    let wont_work = Point { x: 5, y: 4.0 };
}
```

Example 2:
```rs
struct Point<T, U> {
    x: T,
    y: U,
}

fn main() {
    let both_integer = Point { x: 5, y: 10 };
    let both_float = Point { x: 1.0, y: 4.0 };
    let integer_and_float = Point { x: 5, y: 4.0 };
}
```

### In Enum Definitions ###

Example 1:
```rs
#![allow(unused)]
fn main() {
enum Option<T> {
    Some(T),
    None,
}
}
```

Example 2:
```rs
#![allow(unused)]
fn main() {
enum Result<T, E> {
    Ok(T),
    Err(E),
}
}
```

### In Method Definitions ###

Example 1:
```rs
struct Point<T> {
    x: T,
    y: T,
}

impl<T> Point<T> {
    fn x(&self) -> &T {
        &self.x
    }
}

fn main() {
    let p = Point { x: 5, y: 10 };

    println!("p.x = {}", p.x());
}
```

It is possible to implement method on a concrete type.
This will restrict the method for that specific type.
If a method is implemented on `P<f64>` that method will
only be implemented for `P<f64>`. Other `P<T>` won't
have that method.

```rs
struct Point<T> {
    x: T,
    y: T,
}

impl<T> Point<T> {
    fn x(&self) -> &T {
        &self.x
    }
}

impl Point<f32> {
    fn distance_from_origin(&self) -> f32 {
        (self.x.powi(2) + self.y.powi(2)).sqrt()
    }
}

fn main() {
    let p = Point { x: 5, y: 10 };

    println!("p.x = {}", p.x());
}
```

Example 2: A more generic example
```rs
struct Point<X1, Y1> {
    x: X1,
    y: Y1,
}

impl<X1, Y1> Point<X1, Y1> {
    fn mixup<X2, Y2>(self, other: Point<X2, Y2>) -> Point<X1, Y2> {
        Point {
            x: self.x,
            y: other.y,
        }
    }
}

fn main() {
    let p1 = Point { x: 5, y: 10.4 };
    let p2 = Point { x: "Hello", y: 'c' };

    let p3 = p1.mixup(p2);

    println!("p3.x = {}, p3.y = {}", p3.x, p3.y);
}
```

> Monomorphization: Rust compiler turns the generic
code into concrete type.

## Traits ##

* A trait defines functionality a particular type has
and can share with other types.

* We can use **trait bound** to specify that a generic
type can be any type that has certain behaviour.

### Defining a Trait ###

Example:
```rs
pub trait Summary {
    fn summarize(&self) -> String;
}
```

### Implementing a Trait on a Type ###

Example:
```rs
pub trait Summary {
    fn summarize(&self) -> String;
}

pub struct NewsArticle {
    pub headline: String,
    pub location: String,
    pub author: String,
    pub content: String,
}

impl Summary for NewsArticle {
    fn summarize(&self) -> String {
        format!("{}, by {} ({})", self.headline, self.author, self.location)
    }
}

pub struct Tweet {
    pub username: String,
    pub content: String,
    pub reply: bool,
    pub retweet: bool,
}

impl Summary for Tweet {
    fn summarize(&self) -> String {
        format!("{}: {}", self.username, self.content)
    }
}
```

> A trait can be implemented on a type
if at least one of the trait or the type
it local to the crate. For example,
we can implement standard library traits
like Display on a custom type like Tweet
as part of our aggregator crate functionality,
because the type Tweet is local to our aggregator crate.
We can also implement Summary on Vec<T> in our
aggregator crate, because the trait Summary is local
to our aggregator crate. But we can’t implement
the Display trait on Vec<T> within our aggregator crate,
as both are external to our aggregator crate.

### Default Implementations ###

* If implementation is provided for a
trait method, then it is not required
to implement that method for a type.
If a type doesn't implement it the
default implementation of the function
will be used.

```rs
pub trait Summary {
    fn summarize(&self) -> String {
        String::from("(Read more...)")
    }
}

pub struct NewsArticle {
    pub headline: String,
    pub location: String,
    pub author: String,
    pub content: String,
}

// An empty impl block is required
// to specify that this type has
// Summary trait
impl Summary for NewsArticle {}

pub struct Tweet {
    pub username: String,
    pub content: String,
    pub reply: bool,
    pub retweet: bool,
}

impl Summary for Tweet {
    fn summarize(&self) -> String {
        format!("{}: {}", self.username, self.content)
    }
}
```

* If a default implementation isn't provided,
for a method, then a implementation must be
provided by the types that are using the
trait.

```rs
pub trait Summary {
		// Default implementation isn't provided
    fn summarize_author(&self) -> String;

    fn summarize(&self) -> String {
        format!("(Read more from {}...)", self.summarize_author())
    }
}

pub struct Tweet {
    pub username: String,
    pub content: String,
    pub reply: bool,
    pub retweet: bool,
}

// Tweet only have to implement summarize_author method
impl Summary for Tweet {
    fn summarize_author(&self) -> String {
        format!("@{}", self.username)
    }
}
```

### Trait As Parameter ###

If a Trait is used a parameter to a function,
then that function will accept any type that
implements that Trait.

```rs
pub trait Summary {
    fn summarize(&self) -> String;
}

pub struct NewsArticle {
    pub headline: String,
    pub location: String,
    pub author: String,
    pub content: String,
}

impl Summary for NewsArticle {
    fn summarize(&self) -> String {
        format!("{}, by {} ({})", self.headline, self.author, self.location)
    }
}

pub struct Tweet {
    pub username: String,
    pub content: String,
    pub reply: bool,
    pub retweet: bool,
}

impl Summary for Tweet {
    fn summarize(&self) -> String {
        format!("{}: {}", self.username, self.content)
    }
}

pub fn notify(item: &impl Summary) {
    println!("Breaking news! {}", item.summarize());
}

fn main() {
    let tweet = Tweet {
        username: String::from("aagontuk"),
        content: String::from("Hello, world!"),
        retweet: 0,
        reaction: 0,
    };

    notify(tweet);
}
```

### Trait Bound Syntax ###

Function signatures can be written
more concisely with trait bound box.
For example notice following function:

```rs
pub fn notify(item: &impl Summary) {
    println!("Breaking news! {}", item.summarize());
}
```

With trait bounds this can be written:

```rs
pub fn notify<T: Summary>(item: &T) {
    println!("Breaking news! {}", item.summarize());
}
```

Benefit of this will be more clear with multiple
Trait parameter:

```rs
pub fn notify(item1: &impl Summary, item2: &impl Summary) {
```

With Trait bound syntax:

```rs
pub fn notify<T: Summary>(item1: &T, item2: &T) {
```

### Specifying Multiple Trait Bounds with the + Syntax ###

We can specify more than one Trait bound.
Following function will accept any type that
implements Summary and Display trait.

Without Trait bound syntax:
```rs
pub fn notify(item: &(impl Summary + Display)) {
```

With Trait bound syntax:
```rs
pub fn notify<T: Summary + Display>(item: &T) {
```

### Clearer Trait Bounds with where Clauses ###

Consider following function with Trait bounds:
```rs
fn some_function<T: Display + Clone, U: Clone + Debug>(t: &T, u: &U) -> i32 {
```

With `where` clause this can be written:
```rs
fn some_function<T, U>(t: &T, u: &U) -> i32
where
		T: Display + Clone,
		U: Clone + Debug,
{

}
```

### Returning Types that Implement Traits ###

* `impl Trait` syntax can be used in function
return to return a type that implements that
trait.

* `impl Trait` can only be used if the function
returns a single type.

Example:
```rs
pub trait Summary {
    fn summarize(&self) -> String;
}

pub struct NewsArticle {
    pub headline: String,
    pub location: String,
    pub author: String,
    pub content: String,
}

impl Summary for NewsArticle {
    fn summarize(&self) -> String {
        format!("{}, by {} ({})", self.headline, self.author, self.location)
    }
}

pub struct Tweet {
    pub username: String,
    pub content: String,
    pub reply: bool,
    pub retweet: bool,
}

impl Summary for Tweet {
    fn summarize(&self) -> String {
        format!("{}: {}", self.username, self.content)
    }
}

// Uses impl Summary as return type
fn returns_summarizable() -> impl Summary {
    Tweet {
        username: String::from("horse_ebooks"),
        content: String::from(
            "of course, as you probably already know, people",
        ),
        reply: false,
        retweet: false,
    }
}
```

Following code won't compile as it can return different
types:
```rs
pub trait Summary {
    fn summarize(&self) -> String;
}

pub struct NewsArticle {
    pub headline: String,
    pub location: String,
    pub author: String,
    pub content: String,
}

impl Summary for NewsArticle {
    fn summarize(&self) -> String {
        format!("{}, by {} ({})", self.headline, self.author, self.location)
    }
}

pub struct Tweet {
    pub username: String,
    pub content: String,
    pub reply: bool,
    pub retweet: bool,
}

impl Summary for Tweet {
    fn summarize(&self) -> String {
        format!("{}: {}", self.username, self.content)
    }
}

// This functions can return either NewsArticle or Tweet
fn returns_summarizable(switch: bool) -> impl Summary {
    if switch {
        NewsArticle {
            headline: String::from(
                "Penguins win the Stanley Cup Championship!",
            ),
            location: String::from("Pittsburgh, PA, USA"),
            author: String::from("Iceburgh"),
            content: String::from(
                "The Pittsburgh Penguins once again are the best \
                 hockey team in the NHL.",
            ),
        }
    } else {
        Tweet {
            username: String::from("horse_ebooks"),
            content: String::from(
                "of course, as you probably already know, people",
            ),
            reply: false,
            retweet: false,
        }
    }
}
```

### Using Trait Bounds to Conditionally Implement Methods ###

```rs
use std::fmt::Display;

struct Pair<T> {
    x: T,
    y: T,
}

// new() method is implemented for
// all inner type T
impl<T> Pair<T> {
    fn new(x: T, y: T) -> Self {
        Self { x, y }
    }
}

// cmp_display() method is only
// implemented for inner types
// that implements Display  and PartialOrd
impl<T: Display + PartialOrd> Pair<T> {
    fn cmp_display(&self) {
        if self.x >= self.y {
            println!("The largest member is x = {}", self.x);
        } else {
            println!("The largest member is y = {}", self.y);
        }
    }
}
```

We can also conditionally implement a trait for
any type that implements another trait.
Implementations of a trait on any type that
satisfies the trait bounds are called blanket implementations.

```rs
impl<T: Display> ToString for T {

}
```

## Lifetime ##

* Lifetimes ensure that references are valid
as long as we need them to be.

* Most of the cases lifetime is automatically inferred.

* we must annotate lifetimes when the
lifetimes of references could be related in a few different ways.
Rust requires us to annotate the relationships
using generic lifetime parameters to ensure
the actual references used at runtime will definitely be valid.

* The main aim of lifetimes is to prevent dangling references,
which cause a program to reference data other than
the data it’s intended to reference.

### The Borrow Checker ###

* The Rust compiler has a borrow checker that compares
scopes to determine whether all borrows are valid.

* Following program will be rejected because the
borrow checker will see that x's lifetime 'b is
shorter than r's lifetime 'a which is referencing
x.
```rs
fn main() {
    let r;                // ---------+-- 'a
                          //          |
    {                     //          |
        let x = 5;        // -+-- 'b  |
        r = &x;           //  |       |
    }                     // -+       |
                          //          |
    println!("r: {}", r); //          |
}                         // ---------+
```

* Following code will be accepted x's lifetime 'b
is longer than r's lifetime 'a. So the compiler
knows r will be always valid when x valid.
```rs
fn main() {
    let x = 5;            // ----------+-- 'b
                          //           |
    let r = &x;           // --+-- 'a  |
                          //   |       |
    println!("r: {}", r); //   |       |
                          // --+       |
}                         // ----------+
```

### Lifetime Annotation Syntax ###

```rs
&i32        // a reference
&'a i32     // a reference with an explicit lifetime
&'a mut i32 // a mutable reference with an explicit lifetime
```

### Lifetime Annotations in Function Signatures ###

Following function signature tells Rust that
for some lifetime 'a, the function takes two parameters,
both of which are string slices that live
at least as long as lifetime 'a.
The function signature also tells Rust
that the string slice returned from the function
will live at least as long as lifetime 'a.
```rs
fn main() {
    let string1 = String::from("abcd");
    let string2 = "xyz";

    let result = longest(string1.as_str(), string2);
    println!("The longest string is {}", result);
}

fn longest<'a>(x: &'a str, y: &'a str) -> &'a str {
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```

* When returning a reference from a function,
the lifetime parameter for the return type
needs to match the lifetime parameter for one of the parameters.

### Lifetime Annotations in Struct Definitions ###

* We can define structs to hold references,
but in that case we would need to add
a lifetime annotation on every reference
in the struct’s definition. 

```rs
struct ImportantExcerpt<'a> {
    part: &'a str,
}

fn main() {
    let novel = String::from("Call me Ishmael. Some years ago...");
    let first_sentence = novel.split('.').next().expect("Could not find a '.'");
    let i = ImportantExcerpt {
        part: first_sentence,
    };
}
```

* This annotation means an instance of ImportantExcerpt
can’t outlive the reference it holds in its part field.

### Lifetime Elision ###

The compiler uses three rules to figure out
the lifetimes of the references when there aren’t 
explicit annotations. The first rule applies to
input lifetimes, and the second and third rules
apply to output lifetimes. If the compiler 
gets to the end of the three rules and there are still
references for which it can’t figure out lifetimes,
the compiler will stop with an error.
These rules apply to fn definitions as well as impl blocks.

* The first rule is that the compiler assigns
a lifetime parameter to each parameter that’s a reference. 
In other words, a function with one parameter gets
one lifetime parameter: `fn foo<'a>(x: &'a i32);`
a function with two parameters gets two separate
lifetime parameters: `fn foo<'a, 'b>(x: &'a i32, y: &'b i32);` and so on.

* The second rule is that, if there is
exactly one input lifetime parameter,
that lifetime is assigned to all output
lifetime parameters: `fn foo<'a>(x: &'a i32) -> &'a i32.`

* The third rule is that, if there
are multiple input lifetime parameters,
but one of them is `&self` or `&mut` self because this is a method,
the lifetime of self is assigned to all output lifetime parameters. 

### Lifetime Annotations in Method Definitions ###

Example 1:
```rs
struct ImportantExcerpt<'a> {
    part: &'a str,
}

impl<'a> ImportantExcerpt<'a> {
    fn level(&self) -> i32 {
        3
    }
}

impl<'a> ImportantExcerpt<'a> {
    fn announce_and_return_part(&self, announcement: &str) -> &str {
        println!("Attention please: {}", announcement);
        self.part
    }
}

fn main() {
    let novel = String::from("Call me Ishmael. Some years ago...");
    let first_sentence = novel.split('.').next().expect("Could not find a '.'");
    let i = ImportantExcerpt {
        part: first_sentence,
    };
}
```

### The Static Lifetime ###

* `'static` lifetime denotes that the
affected reference can live for
the entire duration of the program.

* All string literals have the `'static` lifetime

### Generic Type Parameters, Trait Bounds, and Lifetimes Together ###

```rs
fn main() {
    let string1 = String::from("abcd");
    let string2 = "xyz";

    let result = longest_with_an_announcement(
        string1.as_str(),
        string2,
        "Today is someone's birthday!",
    );
    println!("The longest string is {}", result);
}

use std::fmt::Display;

fn longest_with_an_announcement<'a, T>(
    x: &'a str,
    y: &'a str,
    ann: T,
) -> &'a str
where
    T: Display,
{
    println!("Announcement! {}", ann);
    if x.len() > y.len() {
        x
    } else {
        y
    }
}
```

## Closures: Anonymous Functions that Capture Their Environment ##

### Capturing the Environment with Closures ###

* The `unwrap_or_else()` method on `Option<T>`
is defined by the standard library.
It takes one argument: a closure without any arguments
that returns a value T (the same type stored
in the Some variant of the `Option<T>`)

```rs
#[derive(Debug, PartialEq, Copy, Clone)]
enum ShirtColor {
    Red,
    Blue,
}

struct Inventory {
    shirts: Vec<ShirtColor>,
}

impl Inventory {
    fn giveaway(&self, user_preference: Option<ShirtColor>) -> ShirtColor {
        user_preference.unwrap_or_else(|| self.most_stocked())
    }

    fn most_stocked(&self) -> ShirtColor {
        let mut num_red = 0;
        let mut num_blue = 0;

        for color in &self.shirts {
            match color {
                ShirtColor::Red => num_red += 1,
                ShirtColor::Blue => num_blue += 1,
            }
        }
        if num_red > num_blue {
            ShirtColor::Red
        } else {
            ShirtColor::Blue
        }
    }
}

fn main() {
    let store = Inventory {
        shirts: vec![ShirtColor::Blue, ShirtColor::Red, ShirtColor::Blue],
    };

    let user_pref1 = Some(ShirtColor::Red);
    let giveaway1 = store.giveaway(user_pref1);
    println!(
        "The user with preference {:?} gets {:?}",
        user_pref1, giveaway1
    );

    let user_pref2 = None;
    let giveaway2 = store.giveaway(user_pref2);
    println!(
        "The user with preference {:?} gets {:?}",
        user_pref2, giveaway2
    );
}
```

### Closure Type Inference and Annotation ###

* Closures usually don't require to specify
types of the parameter or the return value
like functions.

* Closures are stored in variables and used
without naming them and expose them only
to the user of the specific library.

* Closures are short and relevant only
within a narrow context.

* Within these limited contexts,
the compiler can infer the types
of the parameters and the return type

* It's also possible to annotate type 
like variables.

Example:
```rs
use std::thread;
use std::time::Duration;

fn generate_workout(intensity: u32, random_number: u32) {
    let expensive_closure = |num: u32| -> u32 {
        println!("calculating slowly...");
        thread::sleep(Duration::from_secs(2));
        num
    };

    if intensity < 25 {
        println!("Today, do {} pushups!", expensive_closure(intensity));
        println!("Next, do {} situps!", expensive_closure(intensity));
    } else {
        if random_number == 3 {
            println!("Take a break today! Remember to stay hydrated!");
        } else {
            println!(
                "Today, run for {} minutes!",
                expensive_closure(intensity)
            );
        }
    }
}

fn main() {
    let simulated_user_specified_value = 10;
    let simulated_random_number = 7;

    generate_workout(simulated_user_specified_value, simulated_random_number);
}
```

* Comparison with functions syntax:
```rs
fn  add_one_v1   (x: u32) -> u32 { x + 1 }
let add_one_v2 = |x: u32| -> u32 { x + 1 };
let add_one_v3 = |x|             { x + 1 };
let add_one_v4 = |x|               x + 1  ;
```

* If type isn't annotated compiler infers
closure's type.
```rs
fn main() {
    let example_closure = |x| x;

		// Compiler infers x as String and return type as String
		// and locks this inference.
    let s = example_closure(String::from("hello"));

		// This will produce a compiler error
		// as the compiler expects the parameter to be
		// a string
    let n = example_closure(5);
}
```

### Capturing References or Moving Ownership ###

Closures can capture values from their environment in three ways,
which directly map to the three ways a function can take a parameter:
borrowing immutably, borrowing mutably, and taking ownership.
The closure will decide which of these to use based on
what the body of the function does with the captured values.

* Captures an immutable reference:
```rs
fn main() {
    let list = vec![1, 2, 3];
    println!("Before defining closure: {:?}", list);

    let only_borrows = || println!("From closure: {:?}", list);

    println!("Before calling closure: {:?}", list);
    only_borrows();
    println!("After calling closure: {:?}", list);
}
```

* Captures a mutable reference:
```rs
fn main() {
    let mut list = vec![1, 2, 3];
    println!("Before defining closure: {:?}", list);

    let mut borrows_mutably = || list.push(7);

    borrows_mutably();
    println!("After calling closure: {:?}", list);
}
```
> Between the closure definition and the closure call,
an immutable borrow to print isn’t allowed because no other
borrows are allowed when there’s a mutable borrow.

* To force the closure to take ownership of the values it uses in the environment
even though the body of the closure doesn’t strictly need ownership,
you can use the move keyword before the parameter list.
This technique is mostly useful when passing a closure to a new thread
to move the data so that it’s owned by the new thread.

```rs
use std::thread;

fn main() {
    let list = vec![1, 2, 3];
    println!("Before defining closure: {:?}", list);

    thread::spawn(move || println!("From thread: {:?}", list))
        .join()
        .unwrap();
}
```

### Moving Captured Values Out of Closures and the Fn Traits ###

Once a closure has captured a reference or captured ownership of a value
from the environment where the closure is defined (thus affecting what,
if anything, is moved into the closure), the code in the body of the closure
defines what happens to the references or values when the closure is evaluated later
(thus affecting what, if anything, is moved out of the closure).
A closure body can do any of the following: move a captured value out of the closure,
mutate the captured value, neither move nor mutate the value,
or capture nothing from the environment to begin with.

The way a closure captures and handles values from the environment affects
which traits the closure implements, and traits are how functions and structs
can specify what kinds of closures they can use. Closures will automatically
implement one, two, or all three of these Fn traits, in an additive fashion,
depending on how the closure’s body handles the values:

1. `FnOnce` applies to closures that can be called once.
All closures implement at least this trait, because all closures can be called.
A closure that moves captured values out of its body will only implement FnOnce
and none of the other Fn traits, because it can only be called once.

2. `FnMut` applies to closures that don’t move captured values out of their body,
but that might mutate the captured values. These closures can be called more than once. 

3. `Fn` applies to closures that don’t move captured values out of their body
and that don’t mutate captured values, as well as closures that capture nothing
from their environment. These closures can be called more than once without mutating
their environment, which is important in cases such as calling a closure multiple times concurrently.

* Definition of `unwrap_or_else()`: Implements `FnOnce`
```rs
impl<T> Option<T> {
    pub fn unwrap_or_else<F>(self, f: F) -> T
    where
        F: FnOnce() -> T
    {
        match self {
            Some(x) => x,
            None => f(),
        }
    }
}
```

* Usage of `sort_by_key()`: Implements `FnMut`
```rs
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

fn main() {
    let mut list = [
        Rectangle { width: 10, height: 1 },
        Rectangle { width: 3, height: 5 },
        Rectangle { width: 7, height: 12 },
    ];

		// this closure is called multiple times
    list.sort_by_key(|r| r.width);
    println!("{:#?}", list);
}
```

## Iterators ##

### Processing a Series of Items with Iterators ###

Example:
```rs
fn main() {
    let v1 = vec![1, 2, 3];

    let v1_iter = v1.iter();

    for val in v1_iter {
        println!("Got: {}", val);
    }
}
```

### The Iterator Trait and the next Method ###

All iterators implement a trait named Iterator that is defined in the standard library.
The definition of the trait looks like this:
```rs
pub trait Iterator {
    type Item;

    fn next(&mut self) -> Option<Self::Item>;

    // methods with default implementations elided
}
```

To use iterator for a custom type it has to implement
Iterator trait. To implement Iterator define an Item type,
and use this Item type in the return type of the next method.

> values we get from the calls to next are immutable references to the values in the vector.
The iter method produces an iterator over immutable references.
If we want to create an iterator that takes ownership of v1 and returns owned values,
we can call `into_iter` instead of iter.
Similarly, if we want to iterate over mutable references, we can call `iter_mut` instead of iter.

### Methods that Consume the Iterator ###

* Methods that call next are called consuming adaptors,
because calling them uses up the iterator. 

Example: sum method, which takes ownership of the iterator
and iterates through the items by repeatedly calling next, thus consuming the iterator.
```rs
#[cfg(test)]
mod tests {
    #[test]
    fn iterator_sum() {
        let v1 = vec![1, 2, 3];

        let v1_iter = v1.iter();

        let total: i32 = v1_iter.sum();

        assert_eq!(total, 6);
    }
}
```

### Methods that Produce Other Iterators ###

* Iterator adaptors are methods defined on the Iterator trait
that don’t consume the iterator. Instead, they produce
different iterators by changing some aspect of the original iterator.

```rs
fn main() {
    let v1: Vec<i32> = vec![1, 2, 3];

    let v2: Vec<_> = v1.iter().map(|x| x + 1).collect();

    assert_eq!(v2, vec![2, 3, 4]);
}
```

### Using Closures that Capture Their Environment ###

```rs
#[derive(PartialEq, Debug)]
struct Shoe {
    size: u32,
    style: String,
}

fn shoes_in_size(shoes: Vec<Shoe>, shoe_size: u32) -> Vec<Shoe> {
    shoes.into_iter().filter(|s| s.size == shoe_size).collect()
}

#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn filters_by_size() {
        let shoes = vec![
            Shoe {
                size: 10,
                style: String::from("sneaker"),
            },
            Shoe {
                size: 13,
                style: String::from("sandal"),
            },
            Shoe {
                size: 10,
                style: String::from("boot"),
            },
        ];

        let in_my_size = shoes_in_size(shoes, 10);

        assert_eq!(
            in_my_size,
            vec![
                Shoe {
                    size: 10,
                    style: String::from("sneaker")
                },
                Shoe {
                    size: 10,
                    style: String::from("boot")
                },
            ]
        );
    }
}
```

## Fearless Concurrency ##

### Using Threads to Run Code Simultaneously ###

* The Rust standard library uses a 1:1 model of thread implementation,
whereby a program uses one operating system thread per one language thread.

## Smart Pointers ##

### Box<T> to Point to Data on the Heap ###

Situations:

* To use a type whose size can't be known at compile time
and to use a value of that type in a context that requires
an exact size.

* To handle large amount of data and transfer ownership but
unsure data won't be copied while transfering ownership.

* To own a value and you care only that it’s a type that implements
a particular trait rather than being of a specific type

### Usage ###

```rs
fn main() {
    let b = Box::new(5);
    println!("b = {}", b);
}
```

### Enabling Recursive Types with Boxes ###

* Rust Doesn't allow recursive types as their size can't be
known in compile time.

```rs
// Infinite recursion here
// when measuring space
enum List {
    Cons(i32, List),
    Nil,
}

use crate::List::{Cons, Nil};

fn main() {
    let list = Cons(1, Cons(2, Cons(3, Nil)));
}
```

### Using Box<T> to Get a Recursive Type with a Known Size ###

```
enum List {
    Cons(i32, Box<List>),
    Nil,
}

use crate::List::{Cons, Nil};

fn main() {
    let list = Cons(1, Box::new(Cons(2, Box::new(Cons(3, Box::new(Nil))))));
}
```

### Treating Smart Pointers Like Regular References with the Deref Trait ###

#### Following the Pointer to the Value ####

```rs
fn main() {
    let x = 5;
    let y = &x;

    assert_eq!(5, x);
    assert_eq!(5, *y);
}
```

#### Using Box<T> Like a Reference ####

```rs
fn main() {
    let x = 5;
    let y = Box::new(x);

    assert_eq!(5, x);
    assert_eq!(5, *y);
}
```

#### Defining Your Own Smart Pointer ####

Create a new type `MyBox<T>`
```rs
struct MyBox<T>(T);

impl<T> MyBox<T> {
    fn new(x: T) -> MyBox<T> {
        MyBox(x)
    }
}

fn main() {}
```

But deferencing won't work on MyBox<T>. Following code won't compile:

```rs
fn main() {
	let b = MyBox::new(5);
	assert_eq!(5, *b);
}
```

#### Implementing the Deref Trait ###

```rs
use std::ops::Deref;

impl<T> Deref for MyBox<T> {
    type Target = T;

    fn deref(&self) -> &Self::Target {
        &self.0
    }
}

struct MyBox<T>(T);

impl<T> MyBox<T> {
    fn new(x: T) -> MyBox<T> {
        MyBox(x)
    }
}

fn main() {
    let x = 5;
    let y = MyBox::new(x);

    assert_eq!(5, x);
    assert_eq!(5, *y);
}
```

#### Implicit Deref Coercions with Functions and Methods ####

* Deref coercion converts a reference to a type that implements
the Deref trait into a reference to another type.

* Deref coercion is a convenience Rust performs on arguments to
functions and methods, and works only on types that implement the Deref trait.

* It happens automatically when we pass a reference to a particular type’s
value as an argument to a function or method that doesn’t match the parameter
type in the function or method definition

Example: Reference to MyBox converts into &str
```rs
use std::ops::Deref;

impl<T> Deref for MyBox<T> {
    type Target = T;

    fn deref(&self) -> &T {
        &self.0
    }
}

struct MyBox<T>(T);

impl<T> MyBox<T> {
    fn new(x: T) -> MyBox<T> {
        MyBox(x)
    }
}

fn hello(name: &str) {
    println!("Hello, {name}!");
}

fn main() {
    let m = MyBox::new(String::from("Rust"));

		// Deref coersion from &MyBox to &str
    hello(&m);
}
```

#### How Deref Coercion Interacts with Mutability ###

Rust does deref coercion when it finds types and trait
implementations in three cases:

1. From `&T` to `&U` when `T: Deref<Target=U>`
2. From `&mut T` to `&mut U` when `T: DerefMut<Target=U>`
3. From `&mut T` to `&U` when `T: Deref<Target=U>`

* In 1: Converts &T to &U
* In 2: Converts &mut T to &mut U
* In 3: Converts &mut T to &U. But &T to &mut U isn't allowed

### Cleanup with the Drop Trait ###

Example implementing Drop trait:
```rs
struct CustomSmartPointer {
    data: String,
}

impl Drop for CustomSmartPointer {
    fn drop(&mut self) {
        println!("Dropping CustomSmartPointer with data `{}`!", self.data);
    }
}

fn main() {
    let c = CustomSmartPointer {
        data: String::from("my stuff"),
    };
    let d = CustomSmartPointer {
        data: String::from("other stuff"),
    };
    println!("CustomSmartPointers created.");
}
```

#### Dropping a Value Early with std::mem::drop ###

It is not possible to disable drop functionality or
call drop method on a type directly but memory
can be freed earlier using the std::mem::drop function.
```rs
struct CustomSmartPointer {
    data: String,
}

impl Drop for CustomSmartPointer {
    fn drop(&mut self) {
        println!("Dropping CustomSmartPointer with data `{}`!", self.data);
    }
}

fn main() {
    let c = CustomSmartPointer {
        data: String::from("some data"),
    };
    println!("CustomSmartPointer created.");
    drop(c);
    println!("CustomSmartPointer dropped before the end of main.");
}
```

### `Rc<T>`, the Reference Counted Smart Pointer ###

* Share ownership among multiple owners.
* Only applicable for single threaded case. (Arc<T> for multi threade).

* `Rc<T>` is useful to allocate data from the heap for multiple
parts of a program to read and it is not possible to determine at
compile time which part will finish using the data last

* Keeps a reference count of the owners. Will free the object when
count goes to zero.

* Convention is to use `Rc::clone(&T)` instead of `T.clone()`.
As in most cases `T.clone()` does deep copy. Though in this case
it will do a referance count instead of deep copy. But by using
`Rc::clone(&T)` it possible to visually tell that it is doing
reference counting.

Example 1:
```rs
enum List {
    Cons(i32, Rc<List>),
    Nil,
}

use crate::List::{Cons, Nil};
use std::rc::Rc;

fn main() {
    let a = Rc::new(Cons(5, Rc::new(Cons(10, Rc::new(Nil)))));
    let b = Cons(3, Rc::clone(&a));
    let c = Cons(4, Rc::clone(&a));
}
```

Example 2:
```rs
enum List {
    Cons(i32, Rc<List>),
    Nil,
}

use crate::List::{Cons, Nil};
use std::rc::Rc;

fn main() {
    let a = Rc::new(Cons(5, Rc::new(Cons(10, Rc::new(Nil)))));
    println!("count after creating a = {}", Rc::strong_count(&a));
    let b = Cons(3, Rc::clone(&a));
    println!("count after creating b = {}", Rc::strong_count(&a));
    {
        let c = Cons(4, Rc::clone(&a));
        println!("count after creating c = {}", Rc::strong_count(&a));
    }
    println!("count after c goes out of scope = {}", Rc::strong_count(&a));
}
```

### `RefCell<T>` and the Interior Mutability Pattern ###

Interior mutability: Interior mutability is a design pattern
in Rust that allows you to mutate data even when there are
immutable references to that data. To mutate data,
the pattern uses unsafe code inside a data structure
to bend Rust’s usual rules that govern mutation and borrowing.

* With references and `Box<T>` borrowing rules are enforced
at compile time but with `RefCell<T>` borrowing rules are
enforced at runtime.

* Can only be used in single threaded scenario.

* Interior mutability is possible with `RefCell<T>`.

* To get interior mutability enclose the type
in `RefCell<T>`, then call `borrow_mut()` method
on the object to get mutable reference and `borrow()`
method to get immutable reference.

* `borrow()` method returns `Ref<T>` and `borrow_mut()`
returns `RefMut<T>`.

* Same borrowing rules applied for `RefCell<T>` but
enforced at runtime.

Example:
```rs
pub trait Messenger {
    fn send(&self, msg: &str);
}

pub struct LimitTracker<'a, T: Messenger> {
    messenger: &'a T,
    value: usize,
    max: usize,
}

impl<'a, T> LimitTracker<'a, T>
where
    T: Messenger,
{
    pub fn new(messenger: &'a T, max: usize) -> LimitTracker<'a, T> {
        LimitTracker {
            messenger,
            value: 0,
            max,
        }
    }

    pub fn set_value(&mut self, value: usize) {
        self.value = value;

        let percentage_of_max = self.value as f64 / self.max as f64;

        if percentage_of_max >= 1.0 {
            self.messenger.send("Error: You are over your quota!");
        } else if percentage_of_max >= 0.9 {
            self.messenger
                .send("Urgent warning: You've used up over 90% of your quota!");
        } else if percentage_of_max >= 0.75 {
            self.messenger
                .send("Warning: You've used up over 75% of your quota!");
        }
    }
}

#[cfg(test)]
mod tests {
    use super::*;
    use std::cell::RefCell;

    struct MockMessenger {
				// With RefCell<T> it isn't
				// possible to mutate this in
				// send() method of Messanger trait
        sent_messages: RefCell<Vec<String>>,
    }

    impl MockMessenger {
        fn new() -> MockMessenger {
            MockMessenger {
                sent_messages: RefCell::new(vec![]),
            }
        }
    }

    impl Messenger for MockMessenger {
        fn send(&self, message: &str) {
            self.sent_messages.borrow_mut().push(String::from(message));
        }
    }

    #[test]
    fn it_sends_an_over_75_percent_warning_message() {
        // --snip--
        let mock_messenger = MockMessenger::new();
        let mut limit_tracker = LimitTracker::new(&mock_messenger, 100);

        limit_tracker.set_value(80);

        assert_eq!(mock_messenger.sent_messages.borrow().len(), 1);
    }
}
```

### Having Multiple Owners of Mutable Data by Combining `Rc<T>` and `RefCell<T>` ###

`Rc<T>` provides multiple ownership to immutable data.
But with combination of `RefCell<T>` we can get multiple
ownership of immutable data.

Example:
```
#[derive(Debug)]
enum List {
    Cons(Rc<RefCell<i32>>, Rc<List>),
    Nil,
}

use crate::List::{Cons, Nil};
use std::cell::RefCell;
use std::rc::Rc;

fn main() {
    let value = Rc::new(RefCell::new(5));

    let a = Rc::new(Cons(Rc::clone(&value), Rc::new(Nil)));

    let b = Cons(Rc::new(RefCell::new(3)), Rc::clone(&a));
    let c = Cons(Rc::new(RefCell::new(4)), Rc::clone(&a));

    *value.borrow_mut() += 10;

    println!("a after = {:?}", a);
    println!("b after = {:?}", b);
    println!("c after = {:?}", c);
}
```
