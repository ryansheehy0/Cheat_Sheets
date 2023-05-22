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

Programming is like a game where the goal is to implement a feature as fast as possible while having a minimum level of quality.
    - All tools should be there to better achieve this goal.
    The minimum level of quality should be decided by how well other people can read the code.
        - No acronyms or abbreviations
        - If you have abbreviations it would make everything much much faster. Comments can be put in to explain what that variable does.
    - Everything in the programming language should be designed with the speed of writing in mind
        - f for function, w for while, f for for that only work within functions, v for var

- Indexes start at 0
- All data is dynamic
    - How can you do this while still being performant?

- for loops
    - f index name, starting value, how many times to run, increment index by _ at the end of each code execution
        Example:
    f i, 0, 10, 1
        - i starts at 0, the code will run 10 times, i increments by 1
    - functions are f. You cannot create a function inside another function
        - for loops are f and only work inside functions
