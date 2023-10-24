---
author: '"Edgar"'
tags: []
---


## System Software vs Application Software
#compare

|System Software                        | Application Software                    |
| -------------------------------------- | --------------------------------------- |
| Runs Independantly                     | Dependant on System Software            |
| Complex codebase                       | Simple codebase                         |
| Usually written in Low level languages | Usually written in high level languages |
| Relatively low in number               | Abundantly available                    |
| e.g. gcc, systemctl,                   | e.g. Firefox, Obsidian                  |

## Types of System Software

- **Assembler**
	- Program that converts assembly language to machine readable machine language
	- Makes machine code for the itself, **Self Assembler**
	- Makes machine code for other computers, **Cross Assembler**
	- Difference based on passes
		- **One pass** - Assigns memory addresses to all variables as well as convert the source code to machine code in a single pass.
		- **Two pass** - Takes two passes to initially assign memory addresses to all variables then the other pass to convert the intermediate code into machine code.
- **Compiler**
	- Program that converts code written in one language to other languages without changing its functionality, 
		e.g. High Level or Low Level Languages to Assembly.
	- Compiler performs a lot of operations such as preprocessing, lexical analysis, parsing, semantic analysis, conversion of input programs to an intermediate representation, code optimization and code generation.
	- The **compiler is smarter** than the assembler and checks for syntactical errors in code, or a few logical errors which may occur during runtime.
	- Two types of compilers - Self and Cross (same as assembler)
- **Interpreter**
	- Programs that execute code without compiling them beforehand, they get directly executed.
	- The interpreter stops only if it encounters an error.
	- Examples of Interpreted languages: Python, Ruby, PHP

## Compiler Vs Interpreter 
#compare 

| Compiler                        | Interpreter                                |
| ------------------------------- | ------------------------------------------ |
| Takes the whole program at once | Executes line by line                      |
| Generates executable files      | No files generated                         |
| Compilation then execution      | Compilation and execution at the same time |
| Relatively faster               | Relatively Slower                          |
| Shows all errors at once        | Shows error only on encounter              |

- **Linker**
	- Connects the required library files in a program and makes it available for the compiler, if the files are not found then informs the compiler to generate an error.
	- Gets automatically invoked as the last step of the compiler.
- **Loader**
	- The program responsible for the execution of a compiled program, all operating systems that support loading of programs contain a loader.
	- The loader loads machine code into the memory and prepares them for execution, it reads the program from the disk and proceeds to send it to the CPU for it to load and execute.
- **Macro Preprocessor**
	- Macros are directives that enable code reuse and text replacement in programming, improving code readability and maintainability. 
	  (very similar to functions)
	- A macro preprocessor is a tool that scans and processes source code, expanding macros, and performing text replacement 
	- It also does conditional compilation before the actual compilation or assembly of a program, enhancing code readability and maintainability.
- **Text Editor**
	- A simple computer program that allows to create, review and modify documents in a computer.
- **Debugger**
	- The program that tracks and keeps track of the flow of a program and informs the user of any bugs with the most amount of detail possible to help fix the issue.
	- Debugger also allows for code to be executed in parts and relives the pain of executing the whole program again to find the bug.
- **Device Driver**
	- Software component that enable the communication of application software and device hardware. 
	- Allows the computer to recognize and take I/O request from hardware components in the computer.
- **Operating System**
	- The OS is the resource manager for a computer, it orchestrates the system software to work in harmony and manages the actions performed by the application software as well.
	- The OS is responsible for
		- Memory management
		- Security
		- Job Scheduling 
		- Process Scheduling
		- Resource Allocation...
- **Database Management System**
	- It is a collection of programs that enable users to create & maintain a database.
	- It is a general purpose software system that facilitates the process of defining, constructing, manipulating & sharing of database among various users & applications.
	- Allows multiple users & programs to access the database simultaneously.


## Simplified Instructional Computer ( SIC )

### Registers
There are **5 register**, which have the special uses, Each register is **24 bits** in length

| Mnemonic | Number | Special Use                                                      |
| -------- | ------ | ---------------------------------------------------------------- |
| **A**    | 0      | Accumulator; Used for arithmetic operations                      |
| **X**    | 1      | Index Register; Used for addressing                              |
| **L**    | 2      | Linkage Register; Used to store return address from a Subroutine |
| PC       | 8      | Program Counter; Contain the address for the next instruction    |
| SW       | 9      | Status Word; Contains a variety of information                                                                 |

### Memory 
Memory consist of **8 bit** bytes (one location stores only 8 bits). And three of these bytes form a **word** (24 bits). There are a total of 32768 (2^15) bytes in the computer. Words are addressed by the location of their lowest numbered byte.

### Data format
- Integers - 24 Bit Binary numbers
- Negative Numbers are represented by 2's Compliment
- Character take 8 bits
- No support for Floating point numbers.

### Instruction Format
#important
There is only one instruction format in SIC which has **24 bits**

| opcode | x   | address |                    
| ------ | --- | ------- |
| 8      | 1   | 15      |

### Addressing Modes
There are two addressing modes in SIC
- Direct addressing mode
- Indexed addressing mode

| Mode    | Indication | Target addressing caluculation |
| ------- | ---------- | ------------------------------ |
| Direct  | x = 0      | TA = address                   | 
| Indexed | x = 1      | TA = address + x               |
### Instruction Set
1. **Data Transfer Instructions**
	- LDA, LDX LDL, STA, STX, STL
	- LDA {value} - The data in the value is stored to the accumulator.
	- STA {value} - The data from the accumulator is stored to the value.
2. **Arithmetic Instructions**
	- ADD, SUB, MUL, DIV
	- ADD {value} - Adds the data in value to the accumulator 
3. **Comparison Instructions**
	- COMP {value} - The data in the accumulator is compared to the data in the value register and the condition flag in the status word register is set accordingly.
4. **Conditional Jump Instructions**
	- JLT, JEQ, JGT
	- JLT {value} - Jump to {value} if condition code  is set to < 
	  JEQ {value} - Jump to {value} if condition code  is set to = 
	  JGT {value} - Jump to {value} if condition code  is set to >
5. **Unconditional Jump Instructions**
	- J {value} - Jumps to {value} regardless of condition code
6. **Subroutine Linkage Instruction**
	- JSUB {value} - Jump to the subroutine at {value}
	- RSUB - Return from the subroutine
7. **I/O Instructions**
	- TD, RD, WD
	- TD - Test I/O Device
	  RD - Read from I/O Device
	  WD - Write to I/O Device

## SIC/XE (Simple Instruction Computer Extended)

### Registers
There are **9 register**, which have the special uses, Each register is **24 bits** in length, except **F** which is 48 bits.

| Mnemonic | Number | Special Use                                                      |
| -------- | ------ | ---------------------------------------------------------------- |
| **A**    | 0      | Accumulator; Used for arithmetic operations                      |
| **X**    | 1      | Index Register; Used for addressing                              |
| **L**    | 2      | Linkage Register; Used to store return address from a Subroutine |
| PC       | 8      | Program Counter; Contain the address for the next instruction    |
| SW       | 9      | Status Word; Contains a variety of information                   |
| B        | 3      | Base Register; Used for addressing                               |
| S        | 4      | General Register                                                 |
| T        | 5      | General register                                                 |
| F        | 6      | Floating point accumulator (48 bits)                                                                 |
### Memory 
Memory consist of **8 bit** bytes (one location stores only 8 bits). And three of these bytes form a **word** (24 bits). There are a total of 1 Megabyte (2^20) bytes in the computer. Words are addressed by the location of their lowest numbered byte.
### Data format
- Integers - 24 Bit binary numbers.
- Negative Numbers are represented by 2's Compliment.
- Character take 8 bits.
- Floating point numbers supported 
	- The fraction is represented as value between 0 & 1 .
	- The exponent is represented as an unsigned number between 0 & 2047 .
	- s is the sign bit, 0 for positive, 1 for negative.

| s | exponent   |                  fraction                |                    
| ------ | --- | ------- |
| 1 | 11   | 36     |
### Instruction Format
#important
There are 4 different instruction format in SIC/XE ranging from 1 byte to 4 bytes.
#### Format 1 (1 bytes)
| opcode |
| ------ |
| 8      |       
#### Format 2 (2 bytes)
| opcode | r1   | r2 |
| ------ | --- | ------- |
| 8      | 4   | 4     |
#### Format 3 (3 bytes)
| opcode | n   | i   | x   | b   | p   | e   | displacement |
| ------ | --- | --- | --- | --- | --- | --- | ------------ |
| 6      | 1   | 1   | 1   | 1   | 1   | 1   | 12           | 

Value of e is 0
#### Format 4 (4 bytes)
| opcode | n   | i   | x   | b   | p   | e   | displacement |
| ------ | --- | --- | --- | --- | --- | --- | ------------ |
| 6      | 1   | 1   | 1   | 1   | 1   | 1   | 20           | 

Value of e is 1
### Addressing Modes
#important 
There are two addressing modes in SIC
- Direct addressing mode
- Indexed addressing mode
- Base Relative addressing mode
- Program Counter Relative addressing mode
- Immediate addressing mode
- Indirect addressing mode
- Simple addressing mode

| Mode                     | Indication  | Target addressing caluculation      |
| ------------------------ | ----------- | ----------------------------------- |
| Direct                   | x = 0       | {TA} = address                        |
| Indexed                  | x = 1       | TA = address + x                    |
| Base Relative            | b=1, p=0    | TA = {B} + disp, 0<= disp<=4095     |
| Program Counter Relative | b=0, p=1    | TA = {B} + disp, -2048<= disp<=2047 |
| Immediate                | n=0, i=1    | TA = Operand value                  |
| Indirect                 | n=1, i=0    | {{TA}} = Operand value              |
| Simple                   | n=i=0/n=i=1 | {TA} = Operand value                |

```
{} refferns to [] in this table
```
### Instruction Set
#important 
1. **Data Transfer Instructions**
	- LDA, LDX LDL, STA, STX, STL
	- LDA {value} - The data in the value is stored to the accumulator.
	- STA {value} - The data from the accumulator is stored to the value.
2. **Arithmetic Instructions**
	- ADD, SUB, MUL, DIV
	- ADD {value} - Adds the data in value to the accumulator.
3. **Comparison Instructions**
	- COMP {value} - The data in the accumulator is compared to the data in the value register and the condition flag in the status word register is set accordingly.
4. **Conditional Jump Instructions**
	- JLT, JEQ, JGT
	- JLT {value} - Jump to {value} if condition code  is set to < .
	  JEQ {value} - Jump to {value} if condition code  is set to =. 
	  JGT {value} - Jump to {value} if condition code  is set to >.
5. **Unconditional Jump Instructions**
	- J {value} - Jumps to {value} regardless of condition code.
6. **Subroutine Linkage Instruction**
	- JSUB {value} - Jump to the subroutine at {value}.
	- RSUB - Return from the subroutine.
7. **I/O Instructions**
	- TD, RD, WD
	- TD - Test I/O Device.
	   RD - Read from I/O Device.
	   WD - Write to I/O Device.
8. **Load & Store to Registers**
	- LDB, STB
	- LDB {value} - Load data in {value} to B register.
	- SDB {value} - Load data in B register to {value}.
9. **Floating Point Arithmetic**
	- ADDF, SUBF, MULF, DIVF
	- MULF {value} - Multiplication done with {value} and Floating point accumulator.
10. **Register to Register Arithmetic**
	- ADDR, SUBR, MULR, DIVR, RMO
	- DIVR r1,r2 - The output of **r2/r1**  is stored in r2.


## Assembler Directives
Assembler Directives are keywords for the assembler to keep track and perform certain tasks during assembly of the program. They are not translated into machine instructions.

- **START** - Specify the starting address of the program.
- **END** - Specify the end of the source program & optionally specifies the first executable instruction in the program.
- **WORD** - Generate one word integer constant.
- **BYTE** - Generate character/hexadecimal constant.
- **RESW** - Reserve the indicated number of words for data access.
- **RESB** - Reserve the indicated number of bytes for data access.

## SIC vs SIC/XE
#compare #important 

| Aspect                 | SIC                           | SIC/XE                                                                                |
| ---------------------- | ----------------------------- | ------------------------------------------------------------------------------------- |
| Full Form              | Simple Instructional Computer | Simple Instructional Computer eXtended                                                |
| Instruction Formats    | 3-byte instructions           | 1-byte, 2-byte 3-byte and 4-byte instructions                                         |
| Registers              | 5 registers (A, X, L, PC, SW) | 9  registers (A, X, L, PC, SW B, S, T,F)                                              |
| Addressing Modes       | Direct, Indexed               | Direct, Indexed, Base Relative, Program Counter Relative, Immediate, Indirect, Simple |
| Floating point support | No                            | Yes         (48 Bit)                                                                  |
| Memory Size            | 32K words (maximum)           | 1 MB (maximum)                                                                         |
| Instruction Set        | Limited                       | Plenty                                                                                |


