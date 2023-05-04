# Null Programming Language

- A very simple programming language. Any ease of use features should be handled by the IDE and not the language.

- Anything that can be done in recursion can be done in a while loop. Never use recursion.
- Macro like functions and function are 2 sides of the same coil. Macro like functions are faster, but if used more than once take up more memory. Functions 
	- Macro like function and functions should be used to abstract code and be treated like comments. You should be able to read a high level function just from the function calls.
- all names should use _ to separate words, be very descriptive, and there should be no acronyms.
- All data is dynamic and binary and to extract information from data you run it through a function that uses a protocol.
- Use enums when working with states. Use match whin checking for cases(See rust)
- Everything should be organized into folders and files with function in those files.
	- ./, ../, folder/.../file
		- ./ searches in the current folder
		- ../ searches in the folder one layer up
		- folder/.../file searches for a file named file recursively in the folder. It has to be ensured that no 2 files are named the same recursively in the folder. This is the responsibility of the programmer.
			- This allows for code within the folder to be moved around without having to change all the file paths

- There needs to be 2 programming languages for each computer.
	- One that runs on the direct hardware. This would be something similar to assembly.
	- The other runs for websites and through a library can run on the hardware. The library will be written in the first programming language.



- Variable names have to be written in camelCase. Names can only have lower case letters and uppercase letters.
- Use const for constants and var for variables.
- You cannot use recursion.
- Anything that can be syntacticly allowed in your language it's going to show up eventually in a large enough code base. There needs to be a programming language tha tdouble checks your work.
- Every list of things where each element is separated with a , should allow for a trailing ,
- Strings should only be allowed to use 's for starting and stopping.
- No semi-colons and tab delimited


- Static typing aka types are checked before the code runs. Strongly typed language aka enforces strick rules for variables types.
- Dynamic typing aka types are check when run.