[Home](./README.md)

# Bash Scripting

Bash scripting is creating a file with a sequence of bash commands which allow for automating tasks on linux.

Add `#!/bin/bash` to the start of bash script files. Bash script files what the .sh extension.

`#`s are comments in bash

## Table of Contents

<!-- TOC -->

- [Bash Scripting](#bash-scripting)
  - [Table of Contents](#table-of-contents)
  - [Variables](#variables)
  - [Special parameters](#special-parameters)
  - [Math](#math)
  - [If statements](#if-statements)
    - [Conditionals](#conditionals)
    - [Extended test command](#extended-test-command)
  - [Exit](#exit)

<!-- /TOC -->

## [Variables](#table-of-contents)
Variables in bash are case sensitive.

```bash
var="Ryan"

echo "hello $var"
echo "all uppercase " ${var^^}
echo "all lowercase " ${var,,}
echo "length of var: " ${#var}

# variable:offset:length
nums=0123456789
echo ${nums:2:3} # 234
echo ${nums: -4:4} # 6789

# To run commands and get the output ou can use $()
currentDir=$(pwd)
```

## [Special parameters](#table-of-contents)
Special parameters are parameters set by the shell itself.

| Parameter   | Description                                                                     |
|-------------|---------------------------------------------------------------------------------|
| $#          | Number of arguments passed to the script                                        |
| $0, $1, ... | Represents each argument passed to the script. $0 is the name of the script ran |
| $$          | Process id of the current script                                                |

## [Math](#table-of-contents)

```bash
x=4
y=8
echo $((x+y)) #12

# No negative numbers or decimals
```

- List a sequence of numbers

```bash
echo month{1...3} # month1 month2 month3
```

## [If statements](#table-of-contents)

```bash
if [ condition ]; then
    # Commands to be executed if the condition is true
else
    # Commands to be executed if the condition is false
fi
```

### [Conditionals](#table-of-contents)

| Conditional | Description              |
|-------------|--------------------------|
| -eq         | Equal                    |
| -ne         | Not equal                |
| -lt         | Less than                |
| -le         | Less than or equal to    |
| -gt         | Greater than             |
| -ge         | Greater than or equal to |
| !           | Logical not              |
| -z          | True if string is empty  |
| -a          | Logical and              |
| -o          | Logical or               |

### [Extended test command](#table-of-contents)



## [Exit](#table-of-contents)
Use `exit #` to exit the script.

A non-zero status indicates an error, and 0 indicates a success.
