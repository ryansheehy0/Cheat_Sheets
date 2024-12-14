[Home](../README.md)

# x86 assembly

- Todo
	- Intel vs AT&T
	- Nasm
	- Explain above

- ;s are comments.

## Registers

| Sub-registers | Description                             |
|---------------|-----------------------------------------|
| AL            | Lowest 8 bits                           |
| AH            | Highest 8 bits                          |
| AX            | Lowest 16 bits                          |
| EAX           | Lowest 32 bits. Resets the top 32 bits. |
| RAX           | 64 bits                                 |

| Register name | Description         |
|---------------|---------------------|
| RAX           | Primary accumulator |
| RBX           | Base register       |
| RCX           | Count register      |
| RDX           | Data register       |
| R8-R15        | General purpose     |
| RBP           | Base pointer reg    |
| RSP           | Stack pointer reg   |

## Commands
Commands follow this syntax: CMD DES, SRC
- The source(SRC) goes into the destination(DES).
- The sources and destinations can either be a register, a memory address, or an immediate number/string.
	- All immediate values are limited to 32 bits.
	- If you have a negative immediate value, the sign is extended to the end of the 64 bits.

### Moving and conditional codes

| Commands        | Description                                                                 |
|-----------------|-----------------------------------------------------------------------------|
| MOV DES, SRC    | Copies the value form source to destination. Dereferences pointers.         |
| LEA DES, SRC    | Copies the value form source to destination. Doesn't dereferences pointers. |
| CMOVcc DES, SRC | Conditional move. cc is the conditional code.                               |

| Conditional code | Description            | Flags              | Description |
|------------------|------------------------|--------------------|-------------|
| E                | Equals                 | ZF = 1             |             |
| NE               | Not equal              | ZF = 0             |             |
| G                | Greater than           | SF = OF and ZF = 0 |             |
| GE               | Greater than or equals | SF = OF            |             |
| L                | Less than              | SF != OF           |             |
| LE               | Less than or equals    | ZF = 1 or SF != OF |             |
| B                | Below                  | CF = 1             | What?       |
| NB               | Not below              | CF = 0             | What?       |
| A                | Above                  | CF = 0 and ZF = 0  | What ?      |
| NA               | Not above              | CF = 1 or ZF = 1   | What?       |
| S                | Sign                   | SF = 1             |             |
| NS               | Not sign               | SF = 0             |             |
| P                | Parity                 | PF = 1             |             |
| NP               | Not parity             | PF = 0             |             |

### Flags and Comparisons

These commands are used to set the flags and don't store the result.

| Commands      | Description  |
|---------------|--------------|
| CMP DES, SRC  | Same as SUB. |
| TEST DES, SRC | Same as AND. |

| Flags | Names         | Description                                                 | Example              |
|-------|---------------|-------------------------------------------------------------|----------------------|
| CF    | Carry flag    | Unsigned overflow                                           | 1111 + 0001 = 1 0000 |
| ZF    | Zero flag     | If the result is 0                                          |                      |
| SF    | Signed flag   | If the result is signed                                     |                      |
| OF    | Overflow flag | Signed overflow                                             | 0111 + 0001 = 1000   |
| PF    | Parity flag   | Count the number of 1 bits in the last 8 bits of the result |                      |

### Arithmetic

| Commands                  | Description                                                                |
|---------------------------|----------------------------------------------------------------------------|
| ADD DES, SRC              |                                                                            |
| SUB DES, SRC              |                                                                            |
| INC DES                   | Increment. Doesn't effect carry flag.                                      |
| DEC DES                   | Decrement. Doesn't effect carry flag.                                      |
| DIV DES                   | Unsigned division. Answer in RAX and remainder in RDX.                     |
| IDIV DES                  | Signed division. Answer in RAX and remainder in RDX.                       |
| MUL DES or MUL DES, SRC   | Signed multiplication. Lower 128 bits(64 bits) in RAX and higher in RDX.   |
| IMUL DES or IMUL DES, SRC | Unsigned multiplication. Lower 128 bits(64 bits) in RAX and higher in RDX. |
| SHL DES, SRC              | Shift left. Multiplying by powers of 2.                                    |
| SHR DES, SRC              | Unsigned shift right. Dividing by powers of 2.                             |
| SAR DES, SRC              | Signed shift right. Dividing by powers of 2. If odd then round up.         |
| ROL DES, SRC              | Rotate left.                                                               |
| ROR DES, SRC              | Rotate right.                                                              |
| RCL DES, SRC              | Rotate left through the carry flag.                                        |
| RCR DES, SRC              | Rotate right through the carry flag.                                       |

- The SRC for shift commands can only be AL or IMM8.

### Logic gate

| Commands     | Description                                                 |
|--------------|-------------------------------------------------------------|
| AND DES, SRC | ANDing a reg with itself updates the flags with no changes. |
| OR DES, SRC  |                                                             |
| NOT DES      | Flips bits.                                                 |
| NEG DES      | Negates signed numbers(2s compliment).                       |
| XOR DES, SRC | XORing a reg with itself makes it 0.                         |

### Jump

| Commands   | Description                                                                                                 |
|------------|-------------------------------------------------------------------------------------------------------------|
| CALL label | Transfers control to a subroutine at the label. The return address is pushed on the stack.                  |
| RET        | Returns from a subroutine. Pops the stack and uses the return address.                                      |
| SYSCALL    | Makes a syscall to the operating system. The specific service is determined by values in certain registers. |
| JMP label  | Jumps to a label.                                                                                           |
| Jcc label  | Conditional jump based on the conditional code.                                                             |

### Stack

| Commands | Description |
|-|-|
| POP DES | |
| PUSH DES | |
| 

### Floats

## Data and pointers
- [var] ; gives address of var
- [reg/mem +/- # * #] for references off of reg/mem

## Hello World

```assembly

```