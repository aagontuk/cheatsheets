## Variable and fundamental data types ##

### Initializing a variable ###

* Copy initialization:
```c++
int numRings = 20;
```

* Direct initialization:
```c++
int numRings(20);
```

* Uniform initialization:
```c++
int numRings{20}
```

If uniform initialization is used with no value. Default is 0.
```c++
int numRings{}
```

### Integers ###

#### Fixed width integers ####
Will give fixed sized integer in all architecture.

```c++
#include <cstdint> // for fixed width integers

/* 
 * 8 bit singed integer. Many systems consider them as chars. So it is better
 * to not use them if using integers is the purpose
 */
int8_t var;

uint8_t var;	// 8 bit unsigned integer

intN_t var;	// N = 16, 32, 64 bits signed integer
uintN_t var;	// N = 16, 32, 64 bits unsigned integer
```

Fixed width integers performance is machine dependent. To get the fastest
integer type on a specific machine use `int_fastN_t`. It will give the fastest
integer which is at least N bits long. N = 8, 16, 32, 64.
```c++
int_fast32_t var;
```

To get the smallest integer which is at least N bits long use `int_leastN_t`
where N = 8, 16, 32, 64.
```c++
int_least64_t var;
```

### Floating point numbers ###

Setting precision of a floating point number:
```c++
#include <iostream>
#include <iomanip> // for std::setprecision()

int main(){
	double d{12.34567890};

	std::cout << "Without precision: " << d << std::endl;
	std::cout << std::setprecision(4);
	std::cout << "With precision: " << d << std::endl;

	return 0;
}
```

Special floating numbers: positive infinity, negative infinity, not a number.
```c++
#include <iostream>

int main(){
	float zero(0.0);
	float posinf = 5.0 / zero;
	float neginf = -5.0 / zero;
	float nan = zero / zero;

	std::cout << posinf << std::endl;
	std::cout << neginf << std::endl;
	std::cout << nan << std::endl;

	return 0;
}
```

### Boolean Numbers ###

```c++
#include <iostream>

int main(){
	bool universeCameFromNothing(true);

	std::cout << "Universe came from nothing: " << universeCameFromNothing
		<< std::endl;

	std::cout << std::boolalpha;
	
	std::cout << "Universe came from nothing: " << universeCameFromNothing
		<< std::endl;

	return 0;
}
```

### Type Casting ###

```c++
#include <iostream>

int main(){
	char ch(65);

	std::cout << ch << std::endl;
	std::cout << static_cast<int>(ch) << std::endl;

	return 0;
}
```

To get the variable or expression type.
```c++
#include <typeinfo>

int main(){
	int numerator(50);
	double denominator(5.0);

	std::cout << typeid(numerator).name() << std::endl;
	std::cout << typeid(numerator / denominator).name() << std::endl;
}
```

### Literal ###

```c++
int integer(50);	// integer
float f(0.05f); 	// used f suffix as default literal is double type
double d(0.31416);	// double floating literal
int hex(0xa0);		// hexadecimal literal
int oct(012);		// Octal literal
int bin(0b1010);	// Binary literal

int longNumber(1'23'570) // c++14 only
```

### Constants ###

```c++
const double avg(6.023e23);
const double massEarth; 	// This is not allowed

int x(50);
const int y(x)			// This is allowed

constexpr double adg(9.8);	// Compile time constant. Value of the constant
				// must be resolved in compile time otherwise
				// will generate an error. This is c++11 feature
```

### Variable Scopes and duration ###

#### shadowing: ####
```c++
int number(5);

if(number == 5){
	int number; 	// local variable

	number = 10;	// will effect only local variable
			// this is shadowing

	std::cout << number << std::endl;	// will print local
}

std::cout << number << std::endl;	// will print outer block number
```

#### Global scope operator ####

`::` is the global scope operator.
```c++
int x(50);	// global variable

int main(){
	int x(40);

	std::cout << x << std::endl;	// will print local x
	std::cout << ::x << std::endl;	// will print global x
}
```

**Internal Variable:** Can be used anywhere in the file they are defined but not
out of the file.

**External Variable:** Cab be used across multiple files. Global variables are
by default external. static keyword can be used to make them internal.

## Console Input/Output ##

* `std::cin` is used for console input. `std::cin` takes inputs untill first
whitespace.
```c++
#include <iostream>

int main(){
	int selection;

	std::cin >> selection;
	std::cout << "You have selected: " << selection << std::endl;

	return 0;
}
```

* `std::getline()` is used to take whole line as input.
```c++
#include <iostream>
#include <string>

int main(){
	std::string name;

	std::cout << "Enter Name: ";
	std::getline(std::cin, name);
	std::cout << "Your name is: " << name;

	return 0;
}
```

* `std::cin` takes upto newline from the input stream. So it will be a problem if any other input function is used after taking numeric input from std::cin.
```c++
#include <iostream>
#include <string>

int main(){
	std::string name;
	int select;

	std::cout << "Select: ";
	std::cin >> select;

	std::cout << "Enter name: ";
	std::getline(std::cin, name);		// will not work
 
	std::cout << "Your name is: " << name << "! You have selected: "
		  << select;

	return 0;
}
```

To solve this problem `std::cin.ignore(n, ch)` can be used where **n** is the
number of character to ignore from the input stream before **ch** character is
found.

```c++
#include <iostream>
#include <string>

int main(){
	int select;
	std::string name;
	
	std::cout << "Select: ";
	std::cin >> select;

	std::cin.ignore(32767, '\n');

	std::cout << "Enter name: ";
	std::getline(std::cin, name);

	std::cout << "Hi " << name << "! You have selected " << select << std::endl;

	return 0;
}
```
### Generating Random Numbers ###

```c++
#include <iostream>
#include <ctime>
#include <cstdlib>

int main(){
	/* For generating different seed each time the program runs */
	srand(static_cast<unsigned int>(time(0)));
	std::cout << rand();

	return 0;
}
```
