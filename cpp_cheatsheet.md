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

### Console I/O Methods ###

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

### Error Handling in Console Input ###

`std::cin` takes upto newline from the input stream. So it will be a problem if any other input function is used after taking numeric input from std::cin.
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

### A Program Handling All the Error Case in Input ###

```c++
#include <iostream>

double getDouble(){
	double d;

	while(true){
		std::cout << "Enter: ";
		std::cin >> d;
		std::cin.ignore(32767, '\n');	/* clear '\n' from input stream */

		/*
		 * Input will fail if a valid number isn't typed. 
		 * if input fails, cin will set fail flag and stop extracting
		 * characters from input stream.
		 */
		if(std::cin.fail()){
			std::cout << "Please enter a floating number" << std::endl;
			std::cin.clear();				/* Clear fail flag */
			std::cin.ignore(32767, '\n');	/* Clear input stream */
		}
		else{
			return d;
		}
	}
}

char getOperator(){
	char op;

	while(true){
		std::cout << "Enter (+, -, * or /): ";
		std::cin >> op;
		std::cin.ignore(32767, '\n');
		
		if(op == '+' || op == '-' || op == '*' || op == '/'){
			return op;
		}
		else{
			std::cout << "Bad operator. Input again." << std::endl;
		}
	}
}

void printResult(double d1, char op, double d2){
	if(op == '+'){
		std::cout << d1 << " + " << d2 << " = " <<  d1 + d2 << std::endl;
	}
	else if(op == '-'){
		std::cout << d1 << " - " << d2 << " = " <<  d1 - d2 << std::endl;
	}
	else if(op == '*'){
		std::cout << d1 << " * " << d2 << " = " <<  d1 * d2 << std::endl;
	}
	else{
		if(d2 != 0){
			std::cout << d1 << " / " << d2 << " = " <<  d1 / d2 << std::endl;
		}
		else{
			std::cout << "Can't devide by zero!";
		}
	}
}

int main(){
	double d1 = getDouble();
	char op = getOperator();
	double d2 = getDouble();

	printResult(d1, op, d2);

	return 0;
}
```
## Generating Random Numbers ##

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

### Function for generating Random Numbers Between A Range ###

**Using modulus:**

```c++
#include <iostream>
#include <ctime>
#include <cstdlib>

int getRandom(int min, int max){
	return min + (rand() % (max - min + 1));
}

int main(){
	/* For generating different seed each time the program runs */
	srand(static_cast<unsigned int>(time(0)));
	std::cout << getRandom(1, 6);

	return 0;
}
```

But this method is biased to low numbers. Following method has less bias to
low numbers.

```c++
#include <iostream>
#include <ctime>
#include <cstdlib>

int getRandom(int min, int max){
	static const double fraction = 1.0 / RAND_MAX;

	return min + ((max - min + 1) * (rand() * fraction));
}

int main(){
	/* For generating different seed each time the program runs */
	srand(static_cast<unsigned int>(time(0)));
	std::cout << getRandom(1, 6);

	return 0;
}
```

For details: http://www.learncpp.com/cpp-tutorial/59-random-number-generation/

## Advanced Data Types ##

### Array ###

#### Array Indexes ####

Array index must be a compile time constant.

```c++
#include <iostream>

int main(){
	int array[5]; // ok

	#define ARR_SIZE 5
	int array[ARR_SIZE];	// ok

	int const arr_size = 5;
	int array[arr_size];	// ok

	int arr_size = 5;
}
```

#### Representing Array Indexes with Enumerators ####

Array index can be represented with enumerators. In this way it makes
arrays well documented:

```
#include <iostream>

namespace Store{
	enum Store{
		LM7805,
		MAX485,
		LM311,
		ATMEGA64,
		LED,
		MAX_ELEMENT
	};
}

int main(){
	int inStore[Store::MAX_ELEMENT];

	inStore[Store::LM7805] = 50;

	std::cout << "There are " << inStore[Store::LM7805] \
			  << " LM7805 in store" << std::endl;

	return 0;
}
```

#### Relation Between Array and Pointer ####

Arrays are actually pointers. It points to the first element of the array.

```c++
#include <iostream>

int main(){
	int arr[2] = {1, 2};

	/* Following two address will be same*/
	std::cout << arr << std::endl;
	std::cout << &arr[0] << std::endl;

	return 0;	
}
```

#### Difference Between Array and Pointer to Array ####

The type of the array is `int (*)[n]` if it is an integer array 
but the type of the pointer to that array is `int *`. Array type contains
the size information of the array. When array is dereferenced or assigned
to a pointer it implicitly converts itself into `type *` from
`type (*)[n]` so size information is lost. Here is an example of this
behaviour:

```c++
#include <iostream>

int main(){
	int arr[5] = {1, 2, 3, 4, 5};
	int *arrPtr = arr;	// arr is converted from int (*)[2] to int *

	/* Will print the size of the array which is 5 * 8 bytes */
	std::cout << sizeof(arr) << std::endl;

	/* Will print the size of the pointer which is 8 bytes */
	std::cout << sizeof(arrPtr) << std::endl;

	return 0;	
}
```

#### String Constants Using Fixed Sized Array and Pointer ####

```c++
#include <iostream>

int main(){
	/*
	 * keep the string constant in memory with r/w access
	 * and return the pointer to it.
	 * So string constant can be changed any time later
	 */
	char arr[] = "hello, world";

	/*
	 * Keep the string constant in read-only section of memory
	 * so it can't be changed
	 */
	char *text = "GNU is not Unix";

	/* As it is a constant so its better to initialize following way */
	const char *text = "GNU is not Unix";

	arr[0] = 'g';			// This OK

	/* 
	 * In this case as string constant is kept in read-only
	 * memory, doing this will generate segmentation
	 * fault
	 */
	*(text + 2) = 'O'; 

	std::cout << arr << std::endl;
	std::cout << text << std::endl;

	return 0;	
}
```

### Pointers ###

#### Definig NULL Pointer C++ Way ####

From C++11 `nullptr` keyword can be used to define a NULL pointer.

```c++
#include <iostream>

int main(){
	int *ptr = nullptr;

	if(ptr){
		std::cout << "Not null" << std::endl;
	}
	else{
		std::cout << "Null" << std::endl;
	}
		
	return 0;	
}
```

#### Void Pointers ####

* Can point to any data type
* Have to cast manually to a data type before dereferencing.
* Pointer arithmetic can't be done using void pointers as size of the
obect isn't known

```c++
#include <iostream>

int main(){
	int x(5);
	void *ptr = &x;	// pointing to an integer

	std::cout << *static_cast<int*>(ptr) << std::endl;

	char ch = 'P';	// pointing to a char
	ptr = &ch;
	
	std::cout << static_cast<char*>(ptr) << std::endl;

	return 0;
}

```

#### Converting A Pointer Address to Integer ####

Using `reinterpret_cast<>`:

```c++
#include <iostream>

int main(){
	int x = 17;
	unsigned int addressX = reinterpret_cast<int>(&x);

	std::cout << addressX << std::endl;

	return 0;
}
```

## Dynamic Memory Allocation ##

There are three basic type of memory allocation:

* **Static memory allocation**: Static and global variables. Allocated
when program runs. Persist throught the program life. Memory is taken from the stack.

* **Atomatic memory allocation**: Function parameter and local variables. Allocated when enter into relevent block and deallocated when exited the block. Memory is taken from the stack.

* **Dynamic memory allocation**: Memory allocated and deallocated dynamically. Memory is taken from the heap.

### Allocating Memory dynamically ###

Dynamically memory is allocated using the `new` keyword.

```c++
#include <iostream>

int main(){
	int *ptr = new int;	// dynamically an integer is allocated.

	*ptr = 5;

	return 0;
}
```

### Deallocating memory ###

Memory is deallocated using the `delete` keyword.

```c++
#include <iostream>

int main(){
	int *ptr = new int(5); // memory is allocated to the pointer

	/* memory is deallocated.
	 * memory is realesed by os.
	 */

	delete ptr; 

	/* still the pointer is holding the memory address
	 * so its better to make it null
	 */
	ptr = 0;
	ptr = nullptr;	// c++11

	return 0;
}
```

### Memory leak ###

memory leak happens when allocated memory can't be deallocated.

```c++
#include <iostream>

void doSomthing(){

	/* Memory is allocated but not deallocated
	 * so memory leak happens when the variable
	 * goes out of scope as there is no way
	 * to deallocate in that case
	 */

	int *ptr = new int;
}

int main(){
	doSomthing();
	return 0;	
}
```

```c++
#include <iostream>

int main(){
	int *ptr = int new;

	int val;

	// assigning to a address with out deallocating
	ptr = &val;	// memory leak

	return 0;
}
```

```c++
#include <iostream>

int main(){
	int *ptr = new int(5);

	// allocating new memory without deallocating previous one
	int *ptr = new int(10);

	return 0;
}
```

## Reference Variables ##

Create alias for a variable. Basically share same memory address. Must be
initialized with an addressable object. Can be used in function to pass
parameter by reference.

```c++
#include <iostream>

int main(){
	int x(10);
	int &y = x; // reference variable

	/*
	 * will output:
	 * 10
	 * 10
	 */
	std::cout << x << std::endl
	std::cout << y << std::endl

	return 0;
}
```

## For Each Loop ##

* Only works from c++11 above
* Can't be used in case of decayed arrays and dynamically allocated arrays.

```c++
#include <iostream>

int main(){
	int fibseq[] = {1, 1, 2, 3, 5, 8, 13, 21};

	std::cout << "Fibonacci Sequence: ";
	for(const auto &elem: fibseq){
		std::cout << elem << " ";
	}
	std::cout << std::endl;

	return 0;
}
```

## Functions ##

### Function Pointers ###

```c++
#include <iostream>

int foo(int x){
	return x*x;
}

int main(){
	int (*square)(int) = foo;

	std::cout << square(10) << std::endl;

	return 0;
}
```

* Can't be used for function's with default arguments

### Function Ellipsis ###

Ellipsis can be used to pass variable length argument in a function.

```c++
#include <iostream>
#include <cstdarg>	// to use ellipsis

void printNum(int count, ...){
	va_list list;
	va_start(list, count);

	for(int arg = 0; arg < count; arg++){
		std::cout << va_arg(list, int) << std::endl;
	}

	va_end(list);
}

int main(){
	printNum(5, 1, 2, 3, 4, 5);

	return 0;
}
```

* Ellipsis are dangerous. Try to avoid them. For more - http://www.learncpp.com/cpp-tutorial/714-ellipsis-and-why-to-avoid-them/

## Object Oriented Programming ##

### Basic Class Example ###

```c++
#include <iostream>

class Point{

	private:
		double m_x;
		double m_y;

	public:
		double getX(){
			return m_x;
		}

		void setX(double x){
			m_x = x;
		}

		double getY(){
			return m_y;
		}

		void setY(double y){
			m_y = y;
		}
};

int main(){
	Point p;
	
	p.setX(-2.5);
	p.setY(2.5);

	std::cout << "(" << p.getX() << ", " << p.getY() << ")" << std::endl;

	return 0;
}
```

### Constructors ###

```c++
#include <iostream>

class Point{

	private:
		double m_x;
		double m_y;

	public:
		Point(double x = 0, double y = 0): m_x(x), m_y(y){
				// empty
		}

		double getX(){
			return m_x;
		}

		void setX(double x){
			m_x = x;
		}

		double getY(){
			return m_y;
		}

		void setY(double y){
			m_y = y;
		}

		void printPoint(){
			std::cout << "(" << m_x << ", " << m_y << ")" << std::endl;
		}
};

int main(){
	Point p(0.5, 0.5);
	
	p.printPoint();

	return 0;
}
```
