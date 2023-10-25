# Assembler
### Basic Assembler Functions
- **Convert mnemonic operation codes** to their machine language equivalents.
- Convert symbolic operands to their equivalent machine address.
- Build the machine instructions in the proper format.
- Convert the data constants specified in the source program into their internal machine representations.

## Two Pass Assembler
The two pass assembler during the initial pass scans for label definitions and  assigns memory addresses to all variables then the second pass to convert the intermediate code into machine code.

### Need for a two pass assembler
The main objective of the two pass assembler is to handle all the **forward reference errors**, the two passes also gives the assembler time to process assembler directives.

```
Forward Rerefence : reference to a label that is defined later in the program the assembler identifies this as an error because it maybe an invalid label that is being used here 
```

## Assembler Output Format
Object program format contains three types of records:
1. **Header Record** - Contains program name, starting address and length.

| Header Record |                                    |
| ------------- | ---------------------------------- |
| Column 1      | H                                  |
| Column 2-7    | Program Name                       |
| Column 8-13   | Starting Address of Object Program |
| Column 14-19  | Length of Object Program in bytes                                   |
   
2. **Text Record** - Contains the machine code and data of the program together with an indication of the address where these are to be loaded.

| Text Record |                                    |
| ------------- | ---------------------------------- |
| Column 1      | T                                 |
| Column 2-7    |Starting Address for Object Code in the record                       |
| Column 8-13   | Length of Object Code in bytes |
| Column 14-19  | Object code, represented in hexadecimal                                   |

3. **End Record** - Marks the end of the object program and specifies the address in the program where execution is to begin.

| End  Record |                                    |
| ------------- | ---------------------------------- |
| Column 1      | E                                  |
| Column 2-7    | Address of First Executable Instruction                        |

## Assembler Data Structures
### OPTAB
- The OPTAB contains the mnemonic operation code and its corresponding machine language equivalent. 
- It acts as a **dictionary/lookup** table for the assembler to convert the mnemonic codes to object code.
- In more complex assemblers the table also stores **instruction format information and length information**.
- Usually organized as a hash table.
- It is usually a static table which doesn't see much modification.
- The assembler checks through the OPTAB for the **validity** of the mnemonics used, and later translate them.
- For SIC/XE The OPTAB also lets the assembler know the instruction format and length to use.
### LOCCTR
- The LOCCTR is a counter variable used to keep track of addresses.
- The LOCCTR is **initialized when the START** assembler directive is used.
- After each statement is processed the length of the data instruction or data area is added to the LOCCTR.
- Whenever a label is encountered, the value in the **LOCCTR gives the address** that label is associated with.
### SYMTAB
- The SYMTAB is the **storage** area for the addresses assigned to labels.
- It includes the name and address for each label, along with the flags to indicate error conditions.
- During pass 1, labels are **entered into the SYMTAB**, and if there is an entry already found then an error is raised.
- During pass 2, the SYMTAB is used as a look up to obtain the addresses for labels, while assembly.

# The Two Pass Assembler
### **Pass One**
```
BEGIN
	read the first input line
	IF OPCODE = 'START' THEN {
		save #[OPERAND] as staring address
		intialize LOCCTR to starting address
		write line to intermediate file
		read next input line
	}
	ELSE
		initialise LOCCTR to 0
	WHILE OPCODE != 'END' {
		IF  not a comment{
			IF there is a symbol in the LABEL field{
				IF LABEL in SYMTAB
					ERROR                // because this would be a duplicate label.
				ELSE
					INSERT (Label, LOCCTR) to the SYMTAB
			}
			IF OPCODE == 'WORD' 
				ADD 3 to LOCCTR
			IF OPCODE == 'RESW' 
				ADD 3 * #[OPERAND] to LOCCTR
			IF OPCODE == 'RESB' 
				ADD #[OPERAND] to LOCCTR
			IF OPCODE == 'BYTE'{
				ADD Length of the constant (in bytes)  to LOCCTR
			} 
			ELSE 
					ERROR
		}
		write line to intermediate file
		read next input line
	}
	write the last line to the intermediate file
	save the program length = LOCCTR - Starting addr
END
```
### Pass Two
```
BEGIN
	read the first input line this time from intermediate file
	IF OPCODE = 'START' THEN {
		write listing line
		read next input line
	}
	Write header record to the object program
	Initialise the first text record
	WHILE OPCODE != 'END' {
		IF  not a comment{
			IF OPCODE in OPTAB{
				IF a symbol is present in the OPERAND field{
					IF OPERAND in SYMTAB{
						Store symbol value as operand address
					}
					ELSE{
						Store 0 as operrand address
						Set error flag         // This is an undefined sumbol
					}
				}
			}
		}
		write line to intermediate file
		read next input line
	}
	write the last line to the intermediate file
	save the program length = LOCCTR - Starting addr
```