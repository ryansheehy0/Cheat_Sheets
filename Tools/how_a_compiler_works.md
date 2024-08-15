<!--
 * This file is part of RS Cheat Sheets.
 *
 * RS Cheat Sheets is free software: you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation, either version 3 of the License, or
 * (at your option) any later version.
 *
 * RS Cheat Sheets is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with RS Cheat Sheets. If not, see <https://www.gnu.org/licenses/>.
 */
-->

[Home](../README.md)

# How A Compiler Works
A **compiler** translates code from one programming language to another, usually machine code.

An **interpreter** directly translates and executes code line by line. It is usually slower than a compiler, but can give better feedback to the programer because they can directly see their code changes.

Steps for a compiler:

- Analysis(Front end) - Creates syntax tree, symbol table, and checks them for errors.
	- **Lexical Analyzer/Tokenizer**               - Outputs a sequences of tokens in order
	- **Syntax Analyzer/Parser**                   - Creates a syntax tree and symbol table from the tokens
	- **Semantic Analyzer**                        - Checks the syntax tree and symbol table for any semantic errors
- Synthesis(Back end) - Constructs target program from syntax tree and symbol table.
	- Intermediate Code Generator                  - Create machine independent code from the syntax tree and symbol table
	- Machine-Independent Code Optimizer           - Optimizes this machine independent code
	- Code Generator                               - Generates machine code for the particular platform
	- Machine-Dependent Code Optimizer             - Optimizes the machine code

<!-- TOC -->

- [Lexical Analyzer/Tokenizer](#lexical-analyzertokenizer)
- [Syntax Analyzer/Parser](#syntax-analyzerparser)
	- [Shunting yard algorithm](#shunting-yard-algorithm)
- [Semantic Analyzer](#semantic-analyzer)
- [Code Generator](#code-generator)

<!-- /TOC -->


position = init + rate * 60
            |
	     Lexical Analyzer
			      v
(id, 1) (=) (id, 2) (+) (id, 3) (*) (60)
            |
				Syntax Analyzer
				    v

## [Lexical Analyzer/Tokenizer](#how-a-compiler-works)
The lexical analyzer reads the source code and groups characters together called tokens.

- A token is composed of two parts, the **token type** and the **attribute value**.
	- The **attribute value** points to an entry in the symbol table.
- Spaces separate the tokens/lexemes

## [Syntax Analyzer/Parser](#how-a-compiler-works)

### [Shunting yard algorithm](#how-a-compiler-works)
- Input expression
- Holding stack
- Output
- Solve stack

- If literal put to output
- If operator put onto holding stack if they are higher president then what's on the stack
- If operator not higher or equal president, then put holding stack onto output until operator is of higher precedence.
- If nothing then empty holding stack to output
- Once input and holding stack are empty
	- If literal put on solve stack
	- If operator, computer the two past operators in the solve stack and put output on the solve stack.

## [Semantic Analyzer](#how-a-compiler-works)
## [Code Generator](#how-a-compiler-works)

Problems:
- How to tokenize?
	- Handle spaces? How do I enforce spaces?
	- How to handle all the different types f tokenization in C++?
- How to parse more complicated code?
- How to organize the code?