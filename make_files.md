[Home](./README.md)

# Make files
Make files are used to automate the building and compiling of a project.

This is most often used for C style languages.

- Make files allow you to compile just the changed files instead of re-compiling everything.

Example: * means a file has changed.

```
+--------------+      +---------------+
|  *file1.c    |      |    file2.c    |
+--------------+      +---------------+
       |                      |
       v                      v
+--------------+      +---------------+
|  *file1.o    |      |    file2.o    |
+--------------+      +---------------+
        \                     /
          \                 /
            \             /
              v         v
           +---------------+
           |  *executable  |
           +---------------+
```
- Because file2.c wasn't changed there is no reason to re-compile it to create file2.o again.

1. Create a file called `makefile` or `Makefile`
1. Add rules
1. Run `make` when ready to compile

## Table of Contents

<!-- TOC -->

- [Make files](#make-files)
  - [Table of Contents](#table-of-contents)
- [Comments](#comments)
- [Rules](#rules)
- [Clean](#clean)
- [Variables](#variables)
- [Conditional execution](#conditional-execution)
  - [List of ifs](#list-of-ifs)
- [Full Example](#full-example)

<!-- /TOC -->

# [Comments](#table-of-contents)
Comments start with #

# [Rules](#table-of-contents)
- If the dependency changes then the command is run to regenerate the target

```
target: dependencies
    command

# Example:
file1.o: file1.c
    gcc file1.c
```

# [Clean](#table-of-contents)
There is often a clean target that usually removes the .o files and the executable.
- To use clean just run `make clean`

```
clean:
    rm -f *.o executable
```

# [Variables](#table-of-contents)

|                  |              |
|------------------|--------------|
| VAR_NAME = value | Creating var |
| $(VAR_NAME)      | Using var    |

# [Conditional execution](#table-of-contents)

```
ifeq ($(VAR_NAME), value)
    # code
else ifeq ($(VAR_NAME), value2)
    # code
else
    # code
endif
```

## [List of ifs](#table-of-contents)

|        |                                     |
|--------|-------------------------------------|
| ifeq   | if equals                           |
| ifneq  | if not equals                       |
| ifdef  | if a variable is defined(non-empty) |
| ifndef | if a variable is not defined        |

# [Full Example](#table-of-contents)

```
CC = gcc
CFLAGS =
LIBS = 

executable: file1.o file2.o
    $(CC) $(CFLAGS) file1.o file2.o -o executable $(LIBS)

file1.o: file1.c
    $(CC) $(CFLAGS) -c file1.c $(LIBS)

file2.o: file2.c
    $(CC) $(CFLAGS) -c file2.c $(LIBS)

clean:
    rm -f *.o executable

```
