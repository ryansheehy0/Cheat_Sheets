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
- [Semantic Analyzer](#semantic-analyzer)
- [Code Generator](#code-generator)

<!-- /TOC -->

## [Lexical Analyzer/Tokenizer](#how-a-compiler-works)
The lexical analyzer reads the source code and groups characters together called tokens.

- A token is composed of two parts, the **token type** and the **attribute value**.
	- The **attribute value** points to an entry in the symbol table.

## [Syntax Analyzer/Parser](#how-a-compiler-works)
## [Semantic Analyzer](#how-a-compiler-works)
## [Code Generator](#how-a-compiler-works)