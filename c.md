[Home](./README.md)

# C
This cheat sheet is not for explaining all the concepts in C, but to explain some of the concepts that are hard to remember.

## Table of Contents

## Standard Libraries

`#include <library.h>`

| Library name | Description                                                                                |
|--------------|--------------------------------------------------------------------------------------------|
| stdio        | Input and output functions                                                                 |
| stdlib       | Converting strings, pseudo-random numbers, memory allocation, or process control functions |
| math         | Math related functions                                                                     |
| string       | String related functions                                                                   |
| ctype        | Classify characters by their types or to convert between types.                            |
| time         | Date and time manipulation.                                                                |
| stdbool      | bool type and values such as true and false.                                               |
| threads      | Managing thread functions.                                                                 |
| stdarg       | Allows functions to accept an indefinite number of arguments.                              |

## Command Line Arguments

```
int main(int argc, char* argv[]){
    // argc is the number of arguments
    // argv is an array of strings with each element being the argument. There arguments are separated with spaces.
    // By default the argc is 1 and the argv[0] is the name of the executable
}
```

## Interacting with files
```
#include <stdio.h>

FILE *fopen(const char *filename, const char *mode);
    // Modes: "r"(read), "w"(write), "a"(append)
    // If failed to open file then it returns NULL
    // "w" will clear the contents of the file or create an empty file if the file doesn't exist.

int fclose(FILE *stream);
    // Returns 0 for success or EOF(usually is a -1) on failure

size_t fread(void *ptr, size_t size, size_t count, FILE *stream);
    // Reads data from file stream into memory in ptr.
    // Size. Specifies the size of each element to be read in. For chars it would be 1 byte.
    // Count. Number of elements to be read in.
    // Do I have the understanding of size right?

size_t fwrite(const void *ptr, size_t size, size_t count, FILE *stream);
    // Writes data in the ptr to the file stream.

int fscanf(FILE *stream, const char *format, ...);
int fprintf(FILE *stream, const char *format, ...);

int fseek(FILE *stream, long offset, int whence);
    // Changes the internal cursor of the file.
    // offset is the number of bytes to offset
    // whence is where to offset from. 
        // SEEK_SET offsets from the start of the file. 
        // SEEK_CUR offsets from the current position of the file.
        // SEEK_END offsets from the end of the file.
    // fseeko, fseeko64 for longer files.

char fgetc(FILE *stream);
    // Gets the next character from the file stream.
```

## Unions
Unions allow a single variable to hold different types with only one member active at a time. All members in a union share the same memory space and assigning a value to one member overwrites the values of the other members. The size of the union is the size of the largest member.

## Printf format specifiers

| Specifier | Print a                                                                       |
|-----------|-------------------------------------------------------------------------------|
| %c        | character                                                                     |
| %s        | string                                                                        |
| %p        | memory address of a pointer in hexadecimal                                    |
| %d or %i  | singed decimal int                                                            |
| %u        | unsigned decimal int                                                          |
| %o        | unsigned int in octal                                                         |
| %x or %X  | unsigned int in hexadecimal with lowercase or uppercase letters               |
| %e or %E  | float in exponential notation with lowercase or uppercase letters(3.1415e+00) |
| %f        | floating point number in decimal notation                                     |
| %g or %G  | float in either decimal or exponential notation depending on the value        |
| %lu       | unsigned long                                                                 |
| %%        | % character                                                                   |

### Format specifiers flags
- %.1 decimal precision with floats

```
double x = 10.1234;
printf("%.2f", x); // 10.12
```

- %1 minimum field width right aligned.
    - This doesn't decrease the amount of characters outputted.

```
double x = 10.1234;
printf("X is:%8.2f", x); // X is:   10.12
```

- %- left aligned.

## Pointers

```
// An array of pointers
    int *array_of_pointers[] // init
    *array_of_pointers[] // de-ref
// A pointer to an array
    int (*pointer_to_an_array)[] // init
    (*pointer_to_an_array)[] // de-ref 
```

## Arrays
- Get size of arrays:`sizeof(array) / sizeof(type)`
    - Doesn't work with pass by reference.

## Header Guards

```
#pragma once

// Contents of the header file
```

```
#ifndef HEADER_NAME_H
#define HEADER_NAME_H

// The HEADER_NAME_H needs to be unique
// Contents of the header file

#enif HEADER_NAME_H
```
## stdlib functions

|       |                              |
|-------|------------------------------|
| strol | Converts a string to an int. |