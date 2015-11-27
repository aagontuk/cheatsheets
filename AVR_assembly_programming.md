## Data Memory Space ##

Data memory space in AVR is devided into 3 parts. General Purpose Registers(GPRs), Input/Output Registers, Internal SRAM.

```
					  Data Memory Space

				------------------------------
				|			R0				 |	Address In Hex: $0000
				------------------------------
	GPRs		|			...				 | .....
				------------------------------
				|			R31				 | $001F
				------------------------------
				|			I/O				 | $0020
				------------------------------
I/O	Registers	|			...				 | .....
				------------------------------
				|			I/O				 | $005F
				------------------------------
				|		SRAM	Location	 | .....
				------------------------------
				|		SRAM	Location	 | .....
				------------------------------
	SRAM		|		SRAM 	Location	 | $0300
				------------------------------
				|		SRAM	Location	 | $0301
				------------------------------
				|		SRAM	Location	 | .....
				------------------------------

```

#### Registers: ####

CPU uses registers to store data temporairly. Most AVRs have 8 bit registers. Two kinds of registers. The General Purpose Registers(GPRs) & I/O registers.

#### GPRs: ####

ARVs have 32 general purpose registers. They are R0 to R31. And located in the lowers location of memory address($0000 to $001F). They can be used by all arithmatic and logical instructions.

#### I/O Registers: ####

I/O registers are dedicated to special functions such as status register, timers, serial comunications, I/O port, ADC etc. For this reason they are called special functions registers(SFRs). The function of each I/O register is fixed by the CPU designer as they are used to controll the microcontroller or peripheral functions supported by the microcontroller.

#### Internal SRAM: ####

Internal SRAM is used for storing data. Each loacation of the SRAM can be accessed directly by its address. Each location is 8 bit wide.

#### Difference between SRAM and EEPROM ####

EEPROM stores data permanently. data stays if power is off. SRAM loses data if poweris off.				

## Some Instructions ##

`;` is used for comment in assembly programming.

`LDI` instruction is used to Load a data into a GPR
```
LDI Rd, k
```
Load Imidiate value. Load value `k` into GPR `Rd` where 16 <= d <= 32. `k` can be any binary, hexadecimal or decimal number.

---------------------------------------------------------

`LDS` instruction is used to load data into GPRs from a memory address
```
LDS Rd, K
```
Load from data space. Load `Rd` with data from a memory address `K` where 0 <= d <= 32. `K` is a memory address between $0000 to $FFFF

---------------------------------------------------------

`STS` instruction is used to store data to a memory address from GPRs
```
STS K, Rd
```

Store directly into memory address `K` from GPR `Rd`. Here `K` is an address of a memory location

---------------------------------------------------------

`ADD` instruction is used to add the data of two GPRs
```
ADD Rd, Rr	       ; Rd = Rd + Rr`
```

Add register `Rd` and `Rr`. And store result in `Rd`

---------------------------------------------------------

`IN` instruction is used to store data into GPRs from I/O registers
```
IN Rd, A
```
Retrieve data from I/O register location `A` and store into the GPR `Rd`. `A` is the memory location of the I/O register. 0<= d <= 32, 0<= A <= 63

---------------------------------------------------------

`OUT` instruction is used to store value in I/O registers from GPRs
```
OUT A, Rr
```
Store GPR `Rr`'s value to an I/O register who's location is `A`

---------------------------------------------------------

`MOV` instruction is used to copy data among GPRs
```
MOV Rd,Rr		; Rd = Rr
```

copy data from `Rr` to `Rd`.

---------------------------------------------------------

`INC` instruction is used to increment data of a register by 1
```
INC Rd			; Rd = Rd + 1
```

Increment the value of `Rd` by 1.

---------------------------------------------------------

`SUB` instruction is used to substract one GPR's value from another GPR's value
```
SUB Rd, Rr		; Rd = Rd - Rr
```
substarct the value of `Rr` from the value of `Rd` and store the result into `Rd`.

---------------------------------------------------------

`DEC` instruction is used to decrement the value of a GPR by 1
```
DEC Rd			; Rd = Rd - 1
```

---------------------------------------------------------

`COM` instruction is used to make 1's complement of a GPR
```
COM Rd
```
invert the bits of `Rd` and then store the value into `Rd`

---------------------------------------------------------

`TST`(Test) instruction can be used to examine a register & set the status regtesr's flag according to the content of the register without performing an arithmetic instruction.

Example:
```
OVER:	IN R20, PINB		; Load R20 with the content of I/O register PINB
		TST R20				; Test R20
		BREQ OVER			; Loop if R20 = 0
```

---------------------------------------------------------

`NOP`(No Operation) instruction wastes time by spending one CPU cycle without executing any operation.
```
NOP			; Spend 1 CPU cycle doing nothing
```

---------------------------------------------------------

`CLR`(Clear) instruction is used to clear a register's value or set to zero.
```
CLR R20		; R20 = 0
```

---------------------------------------------------------

`PUSH` instruction is used to push data to memory stack
```
PUSH Rr 			; PUSH data into memory stack from GPR(0 <= r <= 31)
```

---------------------------------------------------------

`POP` instruction is used to retrieve data back from memory stack
```
POP Rr 				; Pop data from the top of the stack and store into Rr
```
Memory stack works in LIFO method

## DIRECTIVES ##

`.EQU` directive is used to define a constant value / Label for some value of address.
```
.EQU HEXNUM = 0xFF
```
define `HEXNUM` as a constant hex value `0xFF`

---------------------------------------------------------

`.SET` directive is same as `.EQU` but value assigned by set can be re-assigned leter
```
.SET HEXNUM = 0xFF
```
define `HEXNUM` as a hex value `0xFF`

---------------------------------------------------------

`.ORG` directive is used to specify start of a ROM location. Where codes will be burnt.
```
.ORG $0		; Burn From ROM location 0x0
```

## STATUS REGISTER's FLAGS ##
```
Bits 		 D7							 D0
			---------------------------------
SREG		| I | T | H | S | V | N | Z | C |
			---------------------------------
```
`C` = Carry Flag, This flag is set whenever there is a carry out from the D7 bit after an arithmetic operation(Addition, subtraction, increment, decrement etc). This flag bit is affected after an 8 bit addition or substruction.

`Z` = Zero Flag, This flag is affected after an arithmetic or logic operation. If the result is zero than `Z = 1`, else `Z = 0`.

`N` = Negative Flag, It reflects the result of an arithmetic operation. If the D7 bit of the result is zero then `N = 0` and the result is positive. Else `N = 1` and the result is negative.

`V` = Overflow Flag,

`S` = Sign Flag,

`H` = Half Carry Flag, This bit is set if there is a carry from D3 to D4 bit after ADD or SUB instruction.

`T` = Bit Copy Storage. Used as a temporary storage for bit. It can be used to copy a bit from a GPR to another GPR.

`I` = Global Inturrupt Enable

`CLC`(CLear Carry) instruction is used to clear carry bit, `C = 0`

`SEC`(SEt Carry) instruction is used to set carry bit, `C = 1`

## BRANCHING INSTRUCTINS ##

`BRNE` (Branch If Not Equal) instruction is used for looping. `BRNE` instruction uses the zero or Z flag in the status register. CPU jumps to target address if zero flag is low. Z = 0.
```
LABEL:	............	; loop body
		............	; loop body
		DEC Rn			; Z flag = 1 if Rn = 0. Decrement Rn untill it becomes zero 
		BRNE LABEL		; Goto LABEL if Rn != 0 that means zero flag = 0
```
Example: Add 10 times
```
LDI R16, 10
LDI R20, 0
LDI R21, 20
AGAIN:	ADD R20, R21
		DEC R16
		BRNE AGAIN
```

---------------------------------------------------------

`BREQ` (BRanch If EQual). CPU jumps to target address if zero flag is High.
```
AGAIN:	IN R20, PORTB	; Load R20 from PORTB
		TST R20			; Examine R20 and set Z & N flag accordingly
		BREQ AGAIN		; if Z = 1, goto AGAIN
```

---------------------------------------------------------

`BRCC` (BRanch if Carry Cleared). Branch if `C = 0`

---------------------------------------------------------

`BRSH` (BRanch if Same or Higher) Branch if `C = 0`

---------------------------------------------------------

`BRLO` (BRanch if LOwer) Branch if `C = 1`

## JUMP INSTRUCTIONS ##
**TO DO**

## PROGRAM COUNTER ##
**TO DO**

## CALL & STACK ##

`CALL` instruction is used to call a subroutine. Its like C, C++ founctions. Its a 4 Byte instruction. 10 bits are used for the opcode and 22 bits are used for the address of the subroutine. So call can be used to call subroutine any where within the 4 Megabytes of the RAM address space.

When a subroutine is called CPU transfers the control to subroutine & the Program Counter(PC) of the next instruction is saved on the stack. **Stack** is a section of memory used by the CPU to store information temporarily. To access the stack CPU uses Stack Pointer(SP) register.

The **SP** is implemented as two registers. In I/O memory space there are two register named **SPL**(Lower byte of SP) & **SPH**(Higher byte of SP).

When data is pushed into the stack SP decrements. When data is retrieved SP increments. Poping data from stack works in LIFO(Last In First Out) process. `RET` instruction is used to return back to caller.

Example: Toggle all the bits of PORTB by sending 0x55 & 0xAA continuously. Put a time delay between each issuing data to PORTB.
```
.INCLUDE "M32DEF.INC"		; Include file
.ORG 0						; Burn code into ROM memory starting at $0

	LDI R16, HIGH(RAMEND)	; RAMEND is the address of the last location of the RAM.
    						; Load R16 with the higher byet of RAMEND
	
    OUT SPH, R16			; Load SPH with higher byte of RAMEND
	LDI R16, LOW(RAMEND)	; Load R16 with the lower byte of RAMEND
	OUT SPL, R16			; LOad SPL with the lower byte of RAMEND

BACK:	LDI R16, 0x55		; Load R16 with 0x55
		OUT PORTB, R16		; Send 0x55 to PORTB
		CALL DELAY			; Call delay subroutine
		LDI R16, 0xAA		; Load R16 with 0xAA
		OUT PORTB, R16		; Send 0xAA to PORTB
		CALL DELAY			; Call delay subroutine
		RJMP BACK			; Keep doing it forever

;-----------	Delay Subroutine	-------------

DELAY:
		LDI R20, 0xFF	; R20 = 255, Counter for loop
AGAIN:
		NOP				; No operation wastes clock cycles
		NOP
		DEC R20			; Decrement R20
		BRNE AGAIN		; Repeat until R20 = 0
		RET				; Return to caller
```

## AVR I/O PORT PROGRAMMING ##

Number of I/O pins differ among different microcontrollers. There are **32 I/O pins in ARV ATMEGA32**. They are devided into four groups. **PORT A, PORT B, PORT C & PORT D**. There are also some special functions of these I/O pins.

There are also 32 I/O registers. Their memory address is from 0x20 to 0x3F and I/O address is from 0x00 to 0x1F. For example PORTB register which is located at memory address 0x38. This register is used to set PORT B pins as OUTPUT. If the d7 bit of PORTB register is 1, then 8th pin of PORT B will be high.

Pin Confiuration of AVR ATMEGA32
```
							 ___________________
							|					|
			  (XCK/) PB0   --1				  40--  PA0 (ADC0)
							|					|
				(T1) PB1   --2				  39--  PA1 (ADC1)
						  	|					|
		 (INT2/AIN0) PB2   --3				  38--  PA2 (ADC2)
							|					|
		  (OC0/AIN1) PB3   --4				  37--  PA3 (ADC3)
				 __			|					|
				(SS) PB4   --5				  36--  PA4 (ADC4)
							|					|
			  (MOSI) PB5   --6				  35--  PA5 (ADC5)
							|					|
			  (MISO) PB6   --7				  34--  PA6 (ADC6)
							|					|
			   (SCK) PB7   --8				  33--  PA7 (ADC7)
				   _____	|					|
				   RESET   --9				  32--  AREF
							|					|
					 VCC   --10				  31--  AGND
							|					|
					 GND   --11				  30--  AVCC
							|					|
				   XTAL2   --12				  29--  PC7 (TOSC2)
							|					|
				   XTAL1   --13				  28--  PC6 (TOSC1)
							|					|
			    (RXD) PD0  --14				  27--  PC5 (TDI)
							|					|
			    (TXD) PD1  --15				  26--  PC4 (TDO)
							|					|
			   (INT0) PD2  --16				  25--  PC3 (TMS)
							|					|
			   (INT1) PD3  --17				  24--  PC2 (TCK)
							|					|
			   (OC1B) PD4  --18				  23--  PC1 (SDA)
							|					|
			   (OC1A) PD5  --19				  22--  PC0 (SCL)
							|					|
				(ICP) PD6  --20				  21--  PD7 (OC2)
							|___________________|

```
Here PA0 - PA7 = PORT A(8 pins so 8 bits), PB0 - PB7 = PORT B, PC0 - PC7 = PORT C, PD0 - PD7 = PORT D

Each port has three registers assosiated with it. PORTx, DDRx, PINx. DDR stands for Data Direction Rgister. For example PORT B is assosiated with PORTB, DDRB and PINB registers. Each port can be used as input / output. DDRx is used to define the port's direction Whether it is input or output. 1 is set to define as output. PORTx is used to set output. 1 is set to output HIGH. PINx is used to get input of the ports.

Each PORTx, DDRX or PINx is 8 bits register. So the 8 bits are assosiated with consecutive port's 8 pins. For example if d7 bit of DDRC is register is 1, it will indicate that 8th pin of PORT C, PC7 is defined as output. If d5 bit of PORTA is 1 then 6th pin of PORT A, PA5 is high.

-------------------------------------------------------------------------------

**Example of DDRx & PORTx registers role in outputting data:**

Following code will toggle all 8 bits of Port B forever with some delay between on & off state:
```
LDI R16, 0xFF	; R16 = 0xFF = 0b11111111

OUT DDRB, R16	; Make Port B an output port. As each bit of DDRB is 1,
				;  So each pin of Port B is defined as output pin.

L1:		LDI R16, 0x55	; R16 = 0x55 = 0b01010101

		OUT PORTB, R16	; Put 0x55 in port B pins. Port B's 8 pins are now
						; 0 1 0 1 0 1 0 1. 1 means high, 0 means low.

		CALL DELAY		; call subroutine for some delay

		LDI R16, 0xAA	; R16 = 0xAA = 0b10101010

		OUT PORTB, R16	; Put 0xAA in Port B pins. Port B's 8 pins are now
						; 1 0 1 0 1 0 1 0.

		CALL DELAY		

		RJMP L1		; Do this forever
```

-------------------------------------------------------------------------------

**Example of DDRx & PINx registers role in inputting data:**

PORTx effect pull up registors.

Following code gets the data from the pins of port C and send it to port B after adding value 5 with it
```
LDI R16, 0x00	; R16 = 0x00 = 0b00000000

OUT DDRC, R16	; Make port C an input port. As DDRC = 0b00000000, so each pin
				; of port C will set for input.

LDI R16, 0xFF	; R16 = 0xFF = 0b11111111

OUT DDRB, R16	; Make Port B as an output port.As DDRB = 0b11111111, so
				; each pin of Port B will set for output.

L1:		IN R16, PINC	; Take input from Port C pins. And store bits in R16

		LDI R17, 5		; R17 = 5

		ADD R16, R17	; Add R16 with R17 and store to R16

		OUT PORTB, R16	; Send R16 data to Port B

		RJMP L1		; Do it forever
```

-------------------------------------------------------------------------------

**Synchronizer delay:** The Input Circuit of the AVR has a delay of 1 Clock Cycle. That means the PIN registers represents the data that was present at the pin one clock cycle ago. So one cycle delay is used to get realtime data.

Example:
```
.INCLUDE "M32DEF.INC"

.EQU TEMPMEM 0x100	; Memory location

LDI R16, 0x00		; R16 = 0x00 = 0b00000000

OUT DDRB, R16		; Make Port B as input port

NOP					; No operation cycle. Synchronizer Delay.

IN R16, PINB		; Take bits of PINB and store to R16

STS TEMPMEM, R16	; Store R16 to memoty location
```
In the above code when the instruction "IN R16, PINB" is executed, the PINB registers contains the data, which was present at the pins on clock before. That is why NOP is used before this instruction. If NOP is omitted, the read data is the data of the pins when they were output pins.

```
		#######################################################
		##			I/O BIT MANIPULATION PROGRAMMING		 ##
		##							OR						 ##
		##		MANIPULATING SINGLE BIT OF I/O REGISTERS	 ##
		##							OR						 ##
		##	 	  MANIPULATING SINGLE PIN OF I/O PORTS		 ##
		#######################################################
```

A powerful feature of AVR I/O ports is their capability of access individual bits of the port without altering the rest of the bits.

**32 I/O register's name and their address:** $ sign indicates hexadecimal value.
```
Mem Add		I/O Add		Name	|	Mem Add		I/O Add		Name
$20			$00			TWBR	|	$30			$10			PIND
$21			$01			TWSR	|	$31			$11			DDRD
$22			$02			TWAR	|	$32			$12			PORTD
$23			$03			TWDR	|	$33			$13			PINC
$24			$04			ADCL	|	$34			$14			DDRC
$25			$05			ADCH	|	$35			$15			PORTC
$26			$06			ADCSRA	|	$36			$16			PINB
$27			$07			ADMUX	|	$37			$17			DDRB
$28			$08			ACSR	|	$38			$18			PORTB
$29			$09			UBRRL	|	$39			$19			PINA
$2A			$0A			UCSRB	|	$3A			$1A			DDRA
$2B			$0B			UCSRA	|	$3B			$1B			PORTA
$2C			$0C			UDR		|	$3C			$1C			EECR
$2D			$0D			SPCR	|	$3D			$1D			EEDR
$2E			$0E			SPSR	|	$3E			$1E			EEARL
$2F			$0F			SPDR	|	$3F			$1F			EEARH
```

-------------------------------------------------------------------------------

**Following instructions are used to manipulate single bit:**

`SBI`(Set Bit in I/O register) instruction is used to set a bit in I/O register. To make a bit 1.
```
SBI ioReg, bitNumber	; ioReg is the name of I/O register, which is any
						; lower 32 I/O register. bitNumber(0 - 7) is the 
						; position of the bit of the register to manipulate
```
Example:
```
SBI PORTB, 5			; This will set the D5(6th) bit of the PORTB register
						; to 1. As a result the PB4(5th) pin of Port B will
						; output high
```

-------------------------------------------------------------------------------

`CBI`(Clear Bit in I/O register) instruction is used to clear a bit in I/O register. To make a bit 0.
```
CBI ioReg, bitNumber	; ioReg is the name of I/O register, which is any
						; lower32 I/O register. bitNumber is the
						; number of the bit of the register to manipulate
```

-------------------------------------------------------------------------------

Following code will toggle `PB0`(1st) pin of Port B continuously
```
SBI DDRB, 0				; Make PB0 an output pin. D0 = 1. So PB0 is configured
						; as output pin.

LOOP:	 SBI PORTB, 0	; Make PB0 HIGH. As bit is set in D0 of PORTB.
						; So D0 of PORTB == 1

		 CALL DELAY		; call delay subroutine

		 CBI PORTB, 0	; Make PB0 LOW. As bit is cleared from D0 of PORTB.
						; So D0 0f PORTB == 0

		 CALL DELAY

		 RJMP LOOP		; Do this forever
```

-------------------------------------------------------------------------------

Following instructions are used for checking an input pin & make decisions based on the input pin's status.

`SIBS`(Skip if Bit in I/O register is Set) instruction tests a bit and skip next instruction if it is HIGH.
```
SIBS ioReg, bitNumber	; Skip next instruction if bitNumber bit of ioReg
						; register is HIGH
```
The following program will keep monitoring the PB2 pin untill it becomes HIGH. When PB2 becomes HIGH it will write value $45 to Port C, and also send a HIGH-to-LOW pulse to PD3.
```
.INCLUDE M32DEF.INC

	CBI DDRB, 2			; Configure PB2 as input

	LDI R16, 0xFF		; R16 = 0xFF = 0b11111111

	OUT DDRC, R16		; Configure Port C as output port

	SBI DDRD, 3			; Configure PD3 as output

AGAIN:	SIBS PINB, 2	; Check PB2 input. If HIGH skip next instruction

		RJMP AGAIN		; Keep monitoring if PB2 is LOW. If HIGH skip this
						; instruction

		LDI R16, 0x45	; R16 = 0x45

		OUT PORTC, R16	; Write 0x45 to PORTC

		SBI PORTD, 3	; Send HIGH to PD3 by setting D3 of PORTD == 1

		CBI PORTD, 3	; Send LOW to PD3 by setting D3 of PORTD == 0

HERE:	RJUPM HERE		; Stay here forever
```

-------------------------------------------------------------------------------

`SIBC`(Skip if Bit in I/O register is cleared) instruction tests a bit and skip next instruction if it is LOW.
```
SIBC ioReg, bitNumber	; Skip next instruction if bitNumber bit of ioReg
						; register is LOW
```
A switch is connected to PB2. Following program will check the status of switch and send the letter 'N' if SW = 0 or send the letter 'Y' if SW = 1 to PORTD
```
.INCLUDE "M32DEF.INC"

	CBI DDRB, 2				; Set PB2 as input

	LDI R16, 0xFF			; R16 = 0xFF = 0b11111111

	OUT DDRD, R16			; Set Port D as output port

WRITE_N:	SIBC DDRB, 2	; Check PB2 input. Skip next instruction it it is LOW

			RJMP WRITEY	; execute this if PB2 is HIGH. Else skip.

			LDI R16, 'N'	; R16 = 'N'

			OUT PORTD, R16	; Write 'N' to Port D

			RJMP WRITEN	; Check Again.

WRITE_Y:	LDI R16, 'Y'	; R16 = 'Y'

			OUT PORTD, R16	; Write R16 to Port D

			RJMP WRITEN	; Check Again.
```

## ARITHMETIC & LOGICAL OPERATIONS

**Unsigned Number Operations:** In this case the sign bit(8th bit) is not taken into account. So numbers can be from 0 to 255.

`ADD Rd, Rr`

This instruction adds register Rd with Rr and store the number into Rd. Z(Zero), C(Carry), N(Negative), V(Overflow), H(Half Carry), S(Sign) bits of the status register can be affected after this operation.

Example:
```
LDI	R21, 0xF5		; Load 0xF5 into R21

LDI R22, 0x0B		; LOad 0x0B into R22

ADD R21, R22		; R21 = R21 + R22
					; 0xF5 + 0x0B = 11110101 + 00001011 = 100000000(9 bit)
					; So 1 carry out. R21 = 0x00
					; After this operation C = 1 as there is a carry out from D7
					; Z = 1 because the result in the destination(R21) is zero
					; H = 1 as there is a carry out from D3 to D4

LDS R22, 0x400		; Load from RAM location address 0x400 to R22
					; As no adding instruction can add directly with memory

ADD R21, R22		; R21 = R21 + R22

STS 0x400, R21		; Store result into RAM memory space 0x400
```

`ADC`(Add with carry) instruction is used to add with carry bit. As it add with carry bit, 16 bit addition is possible with ADC instruction. As when adding two 16 bit data operands we need to concerned about the carry out from lower byte to upper byte. Its is called multi byte addition.

Example: Add 0x3CE7 with 0x3B8D
```
LDI R16, 0x8D		; R16 = 8D
LDI R17, 0x3B		; R17 = 3B
LDI R18, 0xE7		; R18 = E7
LDI R19, 0x3C		; R19 = 3C

ADD R18, R16		; R18 = R18 + R16 = E7 + 8D = 74 with C = 1(Carry Out)
					; ADD instruction is used for lower byte as carry is
					; not a concern here

ADC R19, R17		; R19 = R19 + R17 + C(Carry out from previous operation)
					; 	  = 3C + 3B + 1
					;	  = 78
					; ADC instruction is used as carry is a concern for upper
					; byte
					; Result: 7874. R19 = 78, R18 = 74
```

--------------------------------------------------------------------------------

There are **five** instrtuctions for substraction in AVR. `SUB`(Subtract), `SBC`(Subtruct with borrow), `SBI`(Subtract immediate), `SBCI`(Subtract immediate with borrow), `SBIW`(Subtract a immediate value from register pair). C flag is used for borrow.

**Subtraction Instruction Summary:**
```
SUB Rd, Rr		; Rd = Rd - Rr.	Borrow is not a concern for this instruction

SBC	Rd, Rr		; Subtract with Borrow. Rd = Rd - Rr - C . In this case
				; C flag is checked for Borrow. This instruction is useful
				; for 16 bit subtraction.

SUBI Rd, K		; Subtract a value K from Rd without borrow. Rd = Rd - K.

SBCI Rd, K		; Subtract a value K from Rd with borrow. Rd = Rd - K - C
				; In this case C flag is checked for borrow.

SBIW Rd:Rd+1, K ; Subtract a value K from Rd+1:Rd register pair.
```
In AVR(And most other CPUs) subtraction is done using 2's complement. Separate circuitry isn't used for subtraction as it takes too many transistors. Assuming that the AVR is executing a simple subtractions and C = 0 prior to this execution. The steps of SUB instruction for unsigned numbers are following:

1. Take 2's complement of the righthand operator
2. Add it with the lefthand operator.
3. Invert the carry. Notice that carry is inverted after above operations.

Example: Subtract 0x23 from 0x3F
```assembly
LDI R20, 0x23		; R20 = 0x23
LDI R21, 0x3F		; R21 = 0x3F
SUB R21, R20		; R21 = R21 - R20
```
**Steps involved in executing this instruction in the CPU:**
```
1. Right hand operator is 0x23 = 0b00100011. Take 2's complement of this. Which is 1's complement(Invert bits) of 0b00100011 + 1. So 2's complement of 0b00100011 is 11011100 + 1 = 11011101

2. Now add this with the left hand operator which is 0x3F = 0b00111111
		R21		=	0x3F	=	00111111	=	00111111
	  - R20		= - 0x23	= - 00100011	= + 11011101 (2's complement)
				  -------					  -----------
				    0x1C					   100011100

So the result after the addition is 100011100 which is 1C with a carry. So the result of the subtraction is 1C and R21 = 1C

3. After this execution C = 0 (Though there is a carry CPU invert it because of the 2's complement method. Carry is found for positive result in 2's complement subtraction method). And N = 0 (As the result is positive)

After execution of the subtraction instructions if N = 0 or C = 0 the result is posative. Else if N = 1 or C = 1 the result is negative.
```
**`SBC`, Subtracting 16 bit number example:** 0x2762 - 0x1296
```
LDI R16, 0x96		; Lower byte of the right hand operator
LDI R17, 0x12		; Higher byte of the right hand operator
LDI R18, 0x62		; Lower byte of the left hand operator
LDI R19, 0x27		; Higher byte of the left hand operator

SUB R18, R16		; Subtract lower byte without carry. As carry is not
					; a concern for lower byet. R18 = R18 - R16 = 0x62 - 0x96
					; = 0xCC. After this execution C = 1 & N = 1 (Negative)

SBC R19, R17		; Subtract higher byte with carry. As lower byte
					; subtraction was negative there is a borrow(C=1) from
					; lower byte subtraction. R19 = R19 - R17 - C
					; = 0x27 - 0x12 - 1 = 0x14
					; So the result is 0x14CC after 16 bit subtraction
					; R19 = 0x14, R17 = 0xCC
```

--------------------------------------------------------------------------------

There are 3 Multiplication instruction in AVR.
```
MUL Rd, Rr		; Multiply two unsigned numbers
MULS Rd, Rr		; Multiply two signed numbers
MULSU Rd, Rr	; Multiply signed number with unsigned number
```
Result is **stored in R1(Higher byte) and R2(Lower byte) registers**.
```
LDI R23, 0x25	; R23 = 0x25
LDI R24, 0x65	; R24 = 0x65

MUL R24, R23	; R24 * R23 = 0x65 * 0x25 = 0xE99
				; R1 = 0x0E, R2 = 0x99
```

--------------------------------------------------------------------------------

There is no division instruction. But division can be done by repeated subtraction. To devide 95 with 10. Subtract 10 from 95, 9 times. The result is 05. So the quotient is 9 and remainder is 5.

So to devide in this method numerator is kept in a register. And the denuminator is subtracted repeatedly. So the quotient is the number of times subtracted. And the remainder is in the register.

Example: devide 95 by 10
```
.DEF NUM = R20			; Define R20 as NUM
.DEF DENUM = R21		; Define R21 as DENUM
.DEF QUOTIENT = R22		; Define R22 as QUOTIENT

LDI NUM, 90
LDI DENUM, 10
CLR QUOTIENT

L1:		INC QUOTIENT	; Increment QUOTIENT
		SUB NUM, DENUM	; Subtact DENUM from NUM
		BRCC L1			; Branch if Carry is Cleared. C = 0. After repeated
						; subtraction if the result is negative C = 1. And the
						; branching / looping will be stopped.

		DEC QUOTIENT			; As once too many
		ADD NUM, DENUM	; add back to it
```

--------------------------------------------------------------------------------

**Signed Numbers:** For signed numbers the most significant bit(D7 bit for 8 bit number) is reserved for sign. And number is represented by other bits. 0 in the D7 bit indicates positive number & 1 indicates negative number.

**Positive Number:** for positive number D7 = 0. So the range of positive number is from +1 to +127.

**Negative Number:** For negative number D7 = 1. Negative numbers are represented using 2's complement. To find the binary representation of a negative number first write the magnitude of the number in the 8 bit format. Now take 2's complete of that. It will be the binary of the negative number of that magnitude.
; For example binary of -5 is 11111011. Binary of 5 in 8 bit format is 00000101. Take 2's complement. Its 11111011. So its the binary of -5. Notice that the D7 bit is 1. its indicating that the number is negative.

--------------------------------------------------------------------------------

**Overflow & V flag:** TO DO

--------------------------------------------------------------------------------

**Difference between N & S flag:** TO DO

--------------------------------------------------------------------------------

**Logic `AND` operator:**
```
AND Rd, Rr		; Rd = Rd & Rr
ANDI Rd, K		; Rd = Rd & K
```
`AND` effects N, Z, S flags. N is the D7 bit of the result. Z = 1 if the result is zero.

`AND` is often use to mask(Set to zero) bit. For example say I want to mask the D5 & D6 bits of 01100011. I can AND it with 10011111.
```
LDI R16, 0x63	; R16 = 0x63 = 0b01100011
ANDI R16, 0x9F	; 0x63 & 0x9F = 01100011 & 10011111 = 00000011 = 0x03
				; R16 = 0x03
```

--------------------------------------------------------------------------------

**Logic `OR` operator:**
```
OR Rd, Rr		; Rd = Rd | Rr
ORI Rd, K		; Rd = Rd | K
```
`OR` effects N, Z, S flags. N is the D7 bit of the result. Z = 1 if the result
is zero.

OR is often used to set certain bits to 1. For example say I want to set the D3 & D4 bit of the 01100101 to 1. I can OR it with 00011000.
```
LDI R16, 0x65	; R16 = 0x65 = 0b01100101
ORI R16, 0x18	; 0x65 | 0x18 = 01100101 | 00011000 = 01111101 = 0x7D
				; R16 = 0x7D
```

--------------------------------------------------------------------------------

**Logic exclusive or `XOR`:**
```
XOR Rd, Rr		; Rd = Rd XOR Rr
```
XOR effects N, Z, S flags. N is the D7 bit of the result. Z = 1 if the result
is zero.

XOR can be used to check equality of two registers. If two registers are equal then the result of XOR of them will be zero. So Z will be set to 1. And we can take decision based on that.

another application of XOR can be toggling the bits. 10101010 XOR 11111111 = 01010101

--------------------------------------------------------------------------------

**Logic Inverter / Complement `COM`:**
```
LDI R20, 0xAA	; R20 = 0xAA = 10101010
COM R20			; R20 = 0x55 = 01010101
```

--------------------------------------------------------------------------------

**Negation / 2's complement `NEG`:**
```
LDI R20, 0x56	; R20 = 0x56 = 01010110 = 86 in decimal
NEG R20			; R20 = 2's complement of 0x56 = 10101001 + 1 = 10101010
					  = 0xAA = -86 in decimal
```

--------------------------------------------------------------------------------

**Compare Instruction CP:**
```
CP Rd, Rr		; Compare Rd with Rr
CPI Rd, K		; Compare Rd with imediate value K
```
compare instruction is really a subtraction except it doesn't change the left hand operator.

Compare instruction affects Z, C & S flags. Different branching instruction can be used based on this.

After CP instruction Z = 0 means operands are not equal. Z = 1 means operands are equal.

After CP instruction for unsigned numbers C = 0 means left hand operand is same or higher than the right hand operator. C = 1 means left hand operator is lower

After CP instruction for signed numbers S = 0 means left hand operand is greater than or equal. S = 1 means left hand operand is less than the right hand operand.

--------------------------------------------------------------------------------

**Branching Instructions:** There are several branching instructions in AVR. Here is most frequently used instructions
```
BREQ LABEL		; BRanch if EQual zero. Branch to LABEL if the result
				; of the previous
				; instruction is zero( Z = 1 ). For example if the two
				; operands are equal in CP instruction.

BRNE LABEL		; BRanch if Not Equal zero. Branch to LABEL if the result
				; of the previous
				; instruction is not zero( Z = 0 ). For example if the two
				; operands are not equal in CP instruction.

BRSH LABEL		; BRanch if Same or Higher. Branch to LABEL if C = 0
				; after previous instruction. For example if the left hand
				; operand is same or higher in CP instruction. Can be used for
				; unsigned numbers

BRLO LABEL		; BRanch if LOwer. Branch to LABEL if C = 1
				; after previous instruction. For example if the left hand
				; operand is lower in CP instruction. Can be used for
				; unsigned numbers

BRGE LABEL		; BRanch if Greater than or Equal. Branch to LABEL if S = 0
				; after previous instruction. For example if the left hand
				; operand is greater than or equal in CP instruction. Used
				; for signed numbers

BRLT LABEL		; BRanch if Less Than. Branch to LABEL if S = 1
				; after previous instruction. For example if the left hand
				; operand is less than right hand operand in CP instruction.
				; Used for signed numbers.

BRCS LABEL		; BRanch to LABEL if Carry is Set. C = 1

BRCC LABEL		; BRanch to LABEL if Carry is Cleared. C = 0

BRVS LABEL		; BRanch if V flag is Set. Branch to LABEL if overflow
				; happens(V = 1)

BRVC LABEL		; BRanch if V flag is Cleared. Branch to LABEL if overflow
				; does not happen(V = 0)
```
**Some example of branch instructions:** TO DO

--------------------------------------------------------------------------------

**Rotational & Shift Instruction:**

`ROR`(Rotate right) instruction rotate 1 bit from left to right through carry. As rotate from left to right after rotate command the carry flag enters to MSB and LSB exits to carry.
```
ROR Rd			; Rotate Rd right through carry
```
Example
```
CLC				; Clear carry C = 0
LDI R20, 0x26	; R20 = 0x26 = 0b00100110
ROR R20			; R20 = 00010011	C = 0
ROR R20			; R20 = 00001001	C = 1
ROR	R20			; R20 = 10000100	C = 1
```

--------------------------------------------------------------------------------

`ROL`(Rotate Left) instruction rotate 1 bit from right to left through carry. As rotate from right to left after rotate command the carry flag enters to LSB and MSB exits to carry.
```
ROL	Rd			; Rotate Rd left through carry
```
; Example
```
SEC				; Set carry C = 1
LDI R20, 0x15	; R20 = 0x15 = 00010101
ROL R20			; R20 = 00101011	C = 0
ROL R20			; R20 = 01010110	C = 0
ROL R20			; R20 = 10101100	C = 0
ROL R20			; R20 = 01011000	C = 1
```

--------------------------------------------------------------------------------

**Data serialization** is to send a byte of data one bit at a time. It can be done through 1 pin of the I/O pins or using serial ports. Rotate instruction can be used for data serialization.

Example: Send 0x45 serially(One bit at a time) through PB1
```
LDI R16, 0x02			; R16 = 0x02 = 0b00000010
OUT DDRB, R16			; PB1 is output pin

LDI R17, 0x45			; Data to send
LDI R18, 8				; 8 bit to send

AGAIN:	ROR R17			; Rotate to right. Keep LSB to C. C = 0
		BRCS ONE		; Branc to ONE if C = 1
		CBI PORTB, 1	; Else if C = 0 send 0 to PB1
		JMP NEXT		; Jump to NEXT

ONE:	SBI PORTB, 1	; Send 1 to PB1

NEXT:	DEC 8			; Decrement after data send
		BRNE AGAIN

HERE:	JMP HERE		; After completing stay here forever
```

--------------------------------------------------------------------------------

**There are three logical shift operator in AVR:**

`LSL`(Logical Shift Left) instruction shifts bits from right to left. After shift instruction 0 is entered into LSB and MSB exits to carry. Notice shift instruction multiply the content of the register by 2.
```
CLC					; Clear carry C = 0
LDI R20, 0x26		; R20 = 0x26 = 00100110 = 38
LSL R20				; R20 = 01001100 = 76	C = 0
LSL R20				; R20 = 10011000 = 152	C = 0
LSL R20				; R20 = 00110000 = 48	C = 1
					; Notice not multiplied as C = 1, overflow
```

--------------------------------------------------------------------------------

`LSR`(Logical Shift Right) instruction shifts bits from left to right. After shift instruction 0 is entered into MSB and LSB exits to carry. Notice shift instruction devides the content of the register by 2.
```
CLC					; Clear carry C = 0
LDI R20, 0x26		; R20 = 0x26 = 00100110 = 38
LSR R20				; R20 = 00010011 = 19	C = 0
LSR R20				; R20 = 00001001 = 9	C = 1
LSR R20				; R20 = 00000100 = 4	C = 1
```

--------------------------------------------------------------------------------

`ASR`(Arithmetic shift right) istruction can devide signed numbers by two. As ASR can shift bits to right without altering MSB. LSB exits to carry.
```
CLC					; C = 0
LDI R20, 0xD0		; R20 = 11010000 = -48
ASR R20				; R20 = 11101000 = -24	C = 0
ASR R20				; R20 = 11110100 = -12	C = 0
ASR R20				; R20 = 11111010 = -6	C = 0
ASR	R20				; R20 = 11111101 = -3	C = 0
ASR	R20				; R20 = 11111110 = -1	C = 1
```

--------------------------------------------------------------------------------

`SWAP` instruction swaps the nibble of a byte.
```
SWAP Rd				; Swaps nibble of Rd register where 0 <= d <= 31
```
```
Before: |D7|D6|D5|D4|D3|D2|D1|D0|
After	|D3|D2|D1|D0|D7|D6|D5|D4|
```

--------------------------------------------------------------------------------

## ADVANCED AVR ASSEMBLY PROGRAMMING ##

Arithmetic & Logical expression can be used with constants

**Arithmetic & Logical operators:**

**Arithmetic operator:** +, -, *, /, %

**Logical operator:** &, |, ^ (exclusive or), ~ (not), << (shift left), >> (shift right)

Example:
```
.EQU ALFA = 60						; .EQU directive is used to define constants
.EQU BETA = 50
.EQU C1 = 0x50
.EQU C2 = 0x10
.EQU C3 = 0x04

LDI R16, (((ALFA - BETA) * 2) + 9)	; R16 = ((ALFA - BETA) * 2) + 9 = 29

LDI R16, (C1 & C2) | C3				; R16 = (0x50 & 0x10) | 0x04
									; = (01010000 & 00010000) | 00000100
									; = 00010000 | 00000100 = 00010100 = 0x14

LDI R16, 0b00001100 << 2			; R16 = 00001100 << 2 = 00110000
```

---------------------------------------------------------

**Manipulating status register's bits:**

To manipulate status register's bits we need to remember the structure of the status register. For example if we want to set the Zero & Carry flag we have to set the d0 & d1 bit of the status register as we know that the d0 & d1 bits are the carry flag & zero flag.

Example: Set carry & zero bit of status register.
```
LDI R20, 0b00000011
OUT SREG, R20			; SREG = 00000011, so carry & zero flag is on
```
To make this task easy & to remove the need of remembering sreg's structure name of each register  bits are defined in the avr microcontroller header files. For example in M32DEF.INC header file
```
.EQU SREG_C = 0		; Carry flag bit
.EQU SREG_Z = 1		; Zero flag bit
.EQU SREG_N = 2		; Negative flag bit
.EQU SREG_V = 3		; Overflow flag bit
.EQU SREG_S = 4		; Sign flag bit
.EQU SREG_H = 5		; Half carry flag bit
.EQU SREG_T = 6		; Bit copy storage flag bit
.EQU SRGE_I = 7		; Global interrept flag bit
```
This names can be used to easily manipulate flags. For example to set the zero flag and clear others:
```
LDI R16, 1<<SREG_Z	; R16 = 00000001 << 1 = 00000010
OUT SREG, R16		; SREG = 00000010, So zero flag is on
```
Set both V & S flag:
```
LDI R16, (1 << SREG_V) | (1 << SREG_S)	; R16 = 00001000 | 00000100 = 00001100
OUT SREG, R16							; SREG = 00001100, So S & V flag is on
```
Pin numbers are also define in the .INCLUDE file of avr. Example: To set PB4 & PB2 as output we can write.
```
.INCLUDE "M32DEF.INC"
	LDI	R20, (1 << PB4 | 1 << PB2)	; R20 = (1 << 4 | 1 << 2)
    								; = 00010000 | 00000100 = 00010100
	OUT DDRB, R20
```

--------------------------------------------------------------------------------------

; HIGH() & LOW() and low function give the higher and lower byte of a 16 bit value
; Example:
```
LDI R16, HIGH(0x4455)	; R16 = 0x44
LDI R17, LOW(0x4455)	; R17 = 0x55
```

--------------------------------------------------------------------------------------

## ADDRESS MODE ##

CPU can access data in various ways. The data could be in registers, in memory or provided as a direct value. These various ways of accessing data is called addressing modes. AVR supports 13 distinct address modes. They can be catagorized into following groups:

1. Single Register or Immediate address mode(Only single register is involved)
2. Two Register addressing mode
3. Direct address mode(Memory is accessed by their direct addresses)
4. Indirect address mode(Memory is accessed by using registers as pointers pointing to memory)
5. Flash Direct address mode(Direct access to flash rom by flash memory addresses)
6. Flash Indirect address mode (Accessed using pointers)

-------------------------------------------------------------------------------------

**Single register address mode:** In this address mode operand is single register. imediate values can be used in this address mode. So its called immediate address mode too. Registers from R16 to R31 can be used in this address mode.

Example:
```
NEG R16				; Negate R16 contents
COM R16				; Take complement
DEC R16				; Decrement R16's content by 1
INC R16				; Increment R16's content by 1

LDI R16, 0xFF		; Load R16 with immediate value
ADI R16, 0x05		; Add R16 with an immediate value
ANDI R16, 0b00100101; AND R16 with 0x25
```
* These are 16 bit instructions.
* In instructions involving only register: 12 bit for opcode & 4 bit for register's address.
* In insstructions with immediate values: 4 bits for opcode, 8 bits for immediate value & 4 bits for register's address.

-------------------------------------------------------------------------------------

**Two register address mode:** Instructions involving two registers.

Example:
```
ADD R16, R17		; R16 = R16 + R17
MOV R16, R17		; Move content of R17 to R16
```
* 16 bits instructions.
* 6 bits for opcode, 5 bits for left hand register & 5 bits for right hand register.

-------------------------------------------------------------------------------------

**Direct address mode:** In this address mode content of RAM memory or I/O registers are accessed by their direct addresses.

Example:
```
LDS R16, 0x200		; Load R16 with the contents of location $200
STS 0x305, R20		; Save R20's contents is RAM location $305
```
I/O registers can be accessed by their direct memory address or their direct I/O address. Direct memory address is used in direct memory instructions & I/O addressing is used in I/O instructions. For example following two instructions are same:
```
OUT 0x18, R16		; 0x18 is the I/O address of port B. 
					; This instruction is sending content of R16 to port B.
STS 0x38, R16		; 0x38 is the memory address of port B.
					; This instruction also sending content of R16 to port B.
```
I/O instructions are faster than memory instructions. also I/O registers name can be used instead of address. These names are defined in .INCLUDE file. Its safer and portable. As I/O addresses can be different in different AVR.
```
OUT PORTB, R16		; Send contents of R16 to port B
```
In memory instructions 16 bit is reserved for memory location. So from $0000 to $FFFF locations of memory can be addressed. So 65536 bytes of data from RAM can be accessed. In I/O instructions address field is 6 bits. So from $00 to $3F addresses can be accessed. So total 64(0 to 63) I/O registers can be accessed. These are standard I/O register memory space.

In some AVRs there is more than 64 I/O registers. These extra I/O registers are called extended I/O registers. As in I/O direct addressing mode address space is 6 bits, extended I/O registers can't be accessed via I/O direct addressing mode. For these direct memory addressing mode have to be used.
```
STS 0x62, R20		; Save content of R20 in PORT F, which is an extended I/O
					; register in ATmega128
```

--------------------------------------------------------------------------------------

**Indirect memory addressing:** In this address mode rather than direct memory addresses, a pair of registers as a pointer to data memory is used. There are three pointers X, Y & Z. X consists of R26(Lower byte, XL) & R27(Higher byte, XH) register. Y consists of R28(Lower byte YL) & R29(Higher byte YH). Z consists of R30(Lower byte, ZL) & R31(Higher byte, ZH). So "LDI R26, 0x02" can be written as "LDI XL, 0x02".
```
			 15		XH					XL		 0
			 -------------------------------------
  X register |7		R27		 0|7		R26		0|
			 -------------------------------------

			 15		YH					YL		 0
			 -------------------------------------
  Y register |7		R29		 0|7		R28		0|
			 -------------------------------------

			 15		ZH					ZL		 0
			 -------------------------------------
  Z register |7		R31		 0|7		R30		0|
			 -------------------------------------
```
`LD` instruction is used to read from the location pointed to by pointer. For example to read from location pointed by X:
```
LD R16, X		; Load R16 with the content of data memory location
				; pointed to by X
```
Load the content of data memory location 0x302 into R20:
```
LDI XL, 0x02		; Load R26(Lower byte of X) with 0x02
LDI XH, 0x03		; Load R27(Higher byte of X) with 0x03.
					; So, Now X is pointing to 0x302
                    
LD R20, X			; Load R20 with content of location 0x302
					; which is pointed to by X
```
`ST` instruction is used to store a value into a location pointed to by a pointer.

Example: Store the content of R20 into location 0x139F
```
LDI XL, 0x9F		; Load XL with lower byte of the address
LDI XH, 0x13		; Load XH with higher byte of the address
ST X, R20			; Store the content of R20 into location
					; pointed to by X, 0x139F
```
Indirect addressing mode makes accessing data dynamic rather than static. Like subsequent data can be accessed using loop. For example for copying $55 in memory location from $140 to $144 with direct addressing we can write:
```
LDI R20, 0x55		; data to save
STS 0x140, R20		; Save 0x55 to location 0x140
STS 0x141, R20		; Save 0x55 to location 0x141
STS 0x142, R20		; Save 0x55 to location 0x142
STS 0x143, R20		; Save 0x55 to location 0x143
STS 0x144, R20		; Save 0x55 to location 0x144
```
But with indirect addressing with pointer we can write:
```
LDI R20, 0x55		; Data to save
LDI R21, 5			; Loop counter

LDI XL, 0x40		; Lower byte of the address
LDI XH, 0x01		; Higher byte of the address. X is now pointing to 0x140

LOOP:	ST X, R20	; Store R20 into data memory location pointed to by X
		INC XL		; Increment XL to point to next memory location
		DEC R21		; Decrement loop counter R21
		BRNE R21	; contineue loop if R21 is not equal to zero
```
**Auto increment:** Incrementing pointer's lower byte with INC instruction has a problem. If the address is 0x1FF, if we increment  XL, carry will not propagate into XH. In this case we can use auto increment feature:
```
LD Rn, X+			; Load Rn with the content of memory location pointed to
					; by X and then increment X to point to the next location.
					; In this case if there is a carry from lower byte of
					; the address, carry will be propagate to higher byte.
```
Using auto increment we can write above program:
```
LDI R20, 0x55		; Value to be stored
LDI R21, 5			; Loop counter

LDI XL, 0x40		; Lower byte of the address
LDI XH, 0x01		; Higher byte of the address

LOOP:	ST X+, R20	; Store R20's content into memory pointed to by X.
					; And then increment X to point to next location.

		DEC R21		; Decrement loop counter
		BRNE LOOP	; Contineue loop if R21 is not equal to zero
```
Example: RAM location $90 to $94 has ASCII character data. $90 = 'H', $91 = 'E', $92 = 'L', $93 = 'L', $94 = 'O'. Send them to port B, on byte at a time.
```
LDI R16, 0xFF
OUT DDRB, R16			; Define port B as output
LDI R17, 5				; Loop counter

LDI XL, 0x90			; point X to $90
LDI XH, 0x00

LOOP:	LD R16, X+		; Load R16 with the content of X then increment
		OUT PORTB, R16	; Send R16 to port B
		DEC R17			; Decrement loop counter
		BRNE LOOP		; contineue loop if R17 not equal to zero
```
Example: Data memory location $240 to $243 have following hex data. $240 = $7D, $241 = $EB, $242 = $C5, $243 = $5B. Add them together and store in locations $220 & $221
```
.EQU L_BYTE = 0x220		; Lower byte of the result to store
.EQU H_BYTE = 0x221		; Higher byte of the result to store

LDI R20, 0x00			; Add the results to
LDI R21, 0x00			; Keep carry here
LDI R16, 4				; Loop counter

LDI XL, 0x40
LDI XH, 0x02

L1:	LD R19, X+			; Load R19 with X, then increment X
	ADD R20, R19
	BRCC L2
	INC R21

L2:	DEC R16
	BRNE L1

STS L_BYTE, R20			; Store lower byte of the result into $220
STS H_BYTE, R21			; Store higher byte of the result into $221
HERE: RJMP HERE		; Stay here forever
```

-------------------------------------------------------------------------------------

**Indirect addressing with displacement:** Suppose we want to read / write from a few bytes higher than where Z is pointing. In that case we can use indirect addressing with displacement. `LDD` & `STD` instruction is used for indirect addresing with displacement.
```
LDD Rn, Z+q			; Load Rn with the contents of memory location pointed to by Z+q
STD Z+q, Rn			; Store content of Rn into location pointed to by Z+q
```
Example: Store 0x55 into location 0x401 & 0x405
```
LDI R20, 0x55
LDI ZL, 0x01
LDI ZH, 0x04

ST Z, R20
STD Z+4, R20
```

-------------------------------------------------------------------------------------

## ACCESSING FLASH ROM ##

AVRs have maximum of 8 megabytes of flash ROM & 64 kilobytes of SRAM. Flash ROM is also called code space or progarm space. SRAM is also called data memory space. **Each location in the flash ROM is 2 byte sized**.

`.DB`(Define byte) directive can be used to allocate byte sized chunks from flash ROM. We can store byte sized data to ROM memory using .DB directive. Each memory location of flash ROM is 2 byte sized, but .DB allocates byte-sized chunks. So if we store few bytes of data using .DB, first byte will go to the lower byte of the location. Next byte will goto the higher byte of the location. Next byte will goto the lower byte of the next location and so on.

If we allocate a fraction of a flash ROM memory, the assembler will allocate whole memory and load the un-used part of it with zero. For example if we allocate only a single byte data using .DB into a memory location, the data will be stored in the lower byte of the location. Higher byte will be loaded with zero.

Example: Store some data into ROM memory location $500
```
.ORG 0x500					; Burn into ROM starting at $500

DATA1: .DB 2,3,5,7			; 4 byte of data has been allocated. So first
							; decimal 2 will be stored into the lower byte
							; of $500, 3 will be into higher byte of $500,
							; 5 will be stored lower byte of $501,
							; 7 will be stored into higher byte of $501

DATA2: .DB 0x1F				; will be stored into lower byte of $502
DATA3: .DB 0b00110011		; will be stored into higher byte of $502

DATA4: .DB 'S'				; ASCII character.
							; will be stored into lower byte of $503
							; as higher byte is un-used,
                            ; it will be loaded with zero.

.ORG 0x510					; Store data from ROM location $510.

DATA5: .DB "Hello, World"	; ASCII string. 'H' will be stored in
							; lower byte of $510. 'e' will be stored in
                            ; the higher byte of $510, 'l' will
							; be stored in the lower byte of $511 and so on.
```
`.DW`(Define Word) can be used to allocated 2 byte from flash ROM location. So entire location can be allocated using `.DW` directive.
```
.ORG $600					; Burn into ROM starting at $600
DATA: .DW 0x1234, 0xABCD	; First 2 byte hex data will be stored in $600
							; Second 2 byte hex data will be stored in $601
```

-------------------------------------------------------------------------------------

To fetch data from flash ROM a register poiter to the memory is neede. Z register can be used as a pointer. So fetching data from flash ROM is called register **indirect flash addressing mode**.

`LPM`(Load Program Memory) instruction is used to load from ROM memory.
```
LPM Rn, Z					; Load Rn with data from ROM memory
							; pointed to by Z


LPM Rn, Z+					; Load Rn with data from ROM memory pointed
							; to by Z.
							; then increment Z to point to next location
```
`LPM` instruction loads 1 byte from flash memory pointed to by Z. But each location in flash memory is 2 byte sized. So we have to mention if we want to read the lower byte or higher byte. The least significant bit(LSB) of Z indicates whether higher or lower byte should be read. If LSB = 0, lower byte of the location pointed to by Z will be read, else higher byte will be read. So LSB of Z is used for indication & rest of the bits are used for addressing.

For example if we want to read lower byte from location $0000, we have to load ZH with 0x00 & ZL with 0x00 (0b00000000). As LSB of ZL is zero lower byte will be read. if we want to read higher byte we have to load ZL with 0x01 (0b00000001). As LSB is 1 higher byte will be read. Similarly to read lower byte from $0001 we have to load ZH with 0x00 & ZL with 0x02 which is 00000010 in binary. LSB is indicating lower byte & rest of the bits are indicating address $00001. To read higher byte we have to load ZL with 0x03 which is 00000011 in binary. LSB is indicating higher byte & rest bits indicating location $0001.

Notice to read lower byte from a location we can left shift location 1 bit then load ZH with higher byte & ZL with lower byte of the location. For example to read lower byte of `$0002 (0000000000000010)`. Left shift 1 bit `0000000000000100`. Now load ZH with higher byte `ZH = 00000000(0x00)` & ZL with lower byte `ZL = 00000100(0x04)`. `LSB = 0`, so lower byte & rest of the bit of `ZL = 0000010(0x02)` indicating location `$0002`.

Notice to read higher byte from a location we can left shift location 1 bit then logical or it with 1. Then load ZH with higher byte & ZL with lower byte. For example to read higher byte from `$0002(0000000000000010).` Left shift `0000000000000010` & or with 1, so `0000000000000010 << 1 | 1` **=** `0000000000000100 | 0000000000000001` **=** `0000000000000101`. Now load ZH with higher byte `ZH = 00000000(0x00)` & ZL with lower byte `ZL = 00000101(0x05)`. `LSB = 1`, so indicating higher byte rest of the bits `0000010(0x02)` indicating location $0002.

Example: Read lower byte of $100 & store into R20
```
LDI ZH, HIGH(0x100 << 1)		; Load ZH with higher byte
LDI ZL, LOW(0x100 << 1)			; Load ZL with lower byte
LPM R20, Z						; Read lower byte of $100 pointed to by Z
```
Example: Read higher byte of $100 & store into R20
```
LDI ZH, HIGH((0x100 << 1) | 1)	; Load ZH with higher byte
LDI ZL, LOW((0x100 << 1) | 1)	; Load ZL with lower byte
LPM R20, Z						; Read higher byte of $100 pointed to by Z
```
Example: "HELLO WORLD", 0 is burnt into ROM starting at $500. Fetch & send to PORTB one byte at a time.
```
.ORG $0							; Burn into ROM starting at $0

LDI R16, 0xFF
OUT DDRB, R16					; Define port B as output

LDI ZH, HIGH(ROMDATA << 1)
LDI ZL, LOW(ROMDATA << 1)

LOOP:	LPM R16, Z+				; Load R16 with data pointed to by Z
								; then increment
                                
		CPI R16, 0				; Compare R16's value with zero
		BREQ END				; Branch if R16 is 0
		OUT PORTB, R16			; Send to PORT B
		RJMP LOOP

END:	RJMP END

.ORG $500						; Burn into ROM starting at $500

ROMDATA: .DB "HELLO WORLD", 0
```

-------------------------------------------------------------------------------------

**Look up table:** TO DO

-------------------------------------------------------------------------------------
