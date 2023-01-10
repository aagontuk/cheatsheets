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
