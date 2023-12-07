# C

- [Usage](#usage)
- [References](#references)
- [Overview](#overview)
  - [Input/Output](#inputoutput)
  - [Pointers](#pointers)
  - [Arrays](#arrays)
  - [Strings](#strings)
  - [Structures](#structures)
  - [Union](#union)
- [Memory Management](#memory-management)
- [Files](#files)
- [Exceptions](#exceptions)
- [Preprocessor](#preprocessor)
  - [Directives](#directives)
  - [Always Available Macros](#always-available-macros)
  - [Operators](#operators)

## Usage

- scripting
- low-level programming
- drivers, micro controllers (e.g. Arduino)

## References

## Overview

Main function:

```c
#include <stdio.h>

int main() {
  //code
  return 0;
}
```

- operators: (variables get assigned to the needed type if two different types are processed in an operation)
  - arithmetic: `+`, `-`, `*`, `/`, `%`, `++`, `--`, `+=`, `-=`, `/=`, `*=`, `%=`
  - comparision: <, >, >=, <=, ==, !=
  - boolean: ||, &&, !
- comments: `// ...`, `/* ... */`
- control structures:
  - if, else
  - switch, case, default break
  - for(init, condition, step)
    - step can include several statements like `x++, y++`
  - while(condition)
  - do, white(condition)
  - break, continue
  - ternary operator
  ```c
  if (<condition>) { <code> } else { <code> }
  <variable> = (<condition>)?<value if true>:<value if false>;
  while (<condition>) { <code> }
  do { <code> } while (<condition>);
  for (<init>; <condition>; <step>) { <code> }
  switch (<var>) {
      case <value1>: <code> [break;]
      case <value2>: <code> [break;]
      ...
      [default: <code> [break;]]
  }
  ```
- functions:
  - need to be declared before usage (can be declared before main program and defined later on)
  - variables in functions are only visible in the function itself whilst variables outside any function are visible in the whole code
  - variables in functions:
    - can be declared const in parameter list if they do not need to be changed
    - get destroyed after escaping the function
    - only static variables will be kept! → they cannot be accessed outside the function, but if the function gets reused the value will be the same as it was at the end of the last call
  ```c
  //declaration
  <return type> <function name>(<parameters>);
  //definition
  <return type> <function name>(<parameters>) { <code> }
  ```

Variables:

- data types: int, float, double, char
- required size of storage: `sizeof(type)`
- each data type needs a specific format modifier in string output
- can be declared constant with const-keyword or #define
- can be declared static (in functions)

```c
// ways of declaration
datatype name; name = value;
datatype name = value;
datatype name1, name2, ...; // declares several variables at the same time
```

### Input/Output

Input:

- `getchar()` → one char
- `gets()` → sequence of chars = string
- `scanf(string with specifier[s], variable address [, next variable address, ...])` → scans input for a specifier to store in a variable, splits input at space symbols

Output:

- `putchar(char)`
- `puts(string)`
- `printf(string with specifier[s], value for specifier[, next value, ...])`

Formatted Input:

- format specifiers:`%[*][max_field]<conversion character>`
  - `*` = would skip the input field if not found in input
  - `max_field` = maximal length of this input field
  - `conversion character` = converts input into needed type
    - d - decimal
    - c - character
    - s - string
    - f - float
    - x - hexadecimal

Formatting Output:

- Escape sequences add special characters
- `\n` = new line
- `\t` = horizontal tab
- `\\` = \
- `\b` = backspace
- `\'` = '
- `\"` = "
- Format specifiers: `%[-][width].[precision]<conversion character>`
  - `-` = left alignment of data in the string
  - `width` = minimum number of characters for the data
  - `precision` = number of decimal places for numeric data/number of characters to print
  - `conversion character` = converts argument to needed type
    - d - decimal
    - c - character
    - s - string
    - f - float
    - e - scientific notation
    - x - hexadecimal

### Pointers

- 8 char hexadecimal storage address = 32bit
- to access the value the pointer point to use `*pointer`
- can be overhanded to functions → these can directly access a variable to change it

```c
//when not directly used
<datatype> * <name> = NULL;
//for direct usage
<datatype> * <name> = & <variable>;
```

Function Pointers:

- point to the beginning of the executable code
- could also be used as a parameter for another function
- e.g. can be used in an array to store a set of actions to choose from

```c
<return type> (*<pointer name>)(<parameters>);

//e.g.
int square(int x) { return x * x; }
int main() {
  int (*ptr)(int);
  ptr = square;
  int y = ptr(3); //function call → y = 9
}
/*
Also possible:
ptr = &square; int y = (*ptr)(3);
*/
```

Void Pointer:

- can point to value of any type → can be changed dynamically
- need to be casted for specific usage later on
- often used to return a value of a variable type from a function or to receive parameters of a variable type

```c
void * <name>;

//in a function
void * <function name>([const] void * <variable name>) { <code> }
```

### Arrays

```c
//declaration
<datatype> <name>[<count>];
//initialization → can be initialized partially → missing values become 0
<datatype> <name>[<count>] = { <values ...> }
```

- access: `<array>[<index>]`
- can have multiple dimensions, e.g.: `<array>[<x>][<y>] ...`
- IMPORTANT: array names act like pointers! (the name of the array is a pointer to its first element)
  ```c
  //e.g. to print all values of an array
  int a[5] = { <values> }
  int *ptr = NULL;
  ptr = a; //the same like ptr = &a[0]
  for (int i = 0; i < 5; i++) { printf("%d", *(ptr + i)); }
  ```
  - ptr++ = the pointer jumps to the next array element
  - arrays must be overhanded to a function as a pointer
  ```c
  //passing an array to a function
  void arrfunc(* variable) { <code> }
  arrfunc(<arrayname>);
  //getting an array from a function
  <datatype of the array> * getarr() { <code> return <arrayname>; }
  <datatype of the array> * ptr = getarr();
  //ptr can access the array via *(ptr + i) or with ptr[i]
  ```

### Strings

- is kind of array ending with NULL character `\0`
- sting uses " → char array!
- char uses ' → no array!
- strings in arrays:

  - two-dimensional char array → all strings would have the same length
  - array of pointers → pointed strings can have different lengths

  ```c
  char <name>[<length>] = "<char sequence>"; //is the same like an array of chars!
  //e.g.
  char str1[6] = "hello";
  //is the same like { 'h', 'e', 'l', 'l', 'o', '\0' }
  char str2[] = "world"; //length 6 = world + \0
  ```

- String Input:
  - does not need &-sign in scanf, because a string is an array and an array variable is a pointer!
  - to read string with spaces use `gets(<variable>)` → reads until new line
  - `fgets(<variable>, <length>, <input>)` reads a specific number of characters → prevents buffer overflow, use stdin (= standard input keyboard) for input, also stores newline character, has space for length-1 characters (`\0` needs one)
- String Output:
  - `fputs(<string>, <output>)` prints string to output, use stdout for standard output
  - `puts(<string>)` outputs string + newline character
  - `printf(<string>)` outputs string without newline character
- String Functions:
  - `sprintf(<target string> , <string sequence with formatter[s]>, <value[s]>)` inserts values into a string and stores it into target string
  - `sscanf(<source string> <formatter[s]>, <target variable[s]>)`
  - string methods in: `#include <string.h>`
    - `strlen(<str>)` → length
    - `strcat(<str1>, <str2>)` → merge two strings, returns pointer to str1
    - `strncat(<str2>, <str2>, <int>)` → append first n characters of str2 to str1
    - `strcpy(<str1>, <str2>)` → copy str2 into str1
    - `strncpy(<str1>, <str2>, <int>)` → copy first n characters of str2 to str1
    - `strcmp(<str1>, <str2>)` → compare two strings:
      - → 0 = equal, `< 0` = str1 < str2, `> 0` = str1 > str2
    - `strncmp(<str1>, <str2>, n)` → compare first n characters of two strings:
      - → 0 = equal, `< 0` = str1 < str2, `> 0` = str1 > str2
    - `strchr(<str>, <c>)` → returns pointer to first occurrence of char c in str, NULL if not found
    - `strrchr(<str>, <c>)` → strchr with reversed str
    - `strstr(<str1>, <str2>)` → returns pointer to first occurrence of str2 in str1, NULL if not found
    - `strlwr()` → to lower case
    - `strupr()` → to upper case
    - `strrev()` → reverse
  - converting methods in: stdio.h
    - `int atoi(<str>)` → ASCII to integer, 0 if not possible
    - `double atof(<str>)` → ASCII to float, 0.0 if not possible
    - `long int atol(<str>)` → ASCII to long int, 0 if not possible

### Structures

- user defined data type → groups related variables of different data types
- to initialize a struct with {} → write down values for members in correct order or type `.<membername> = <value>` to initialize a specific member
- to access a member of a struct out of a pointer, declared with struct-keyword:
  - `<ptr> -> <member>`
  - is the same as `(*<ptr>).<member>`

```c
struct <struct name> { <member declarations> };

//usage for variable declaration
struct <struct name> <variable name>;
<variable name> = (struct <struct name>) { <values for members> };
//or
struct <struct name> <variable name> = { <values for members> };
//or
<struct name>.<member name> = <value>;

//using typedef → does not require the word struct to initialize a struct in code!
typedef struct { <member declaration> } <struct name>;
```

### Union

- stores different data types at same memory location
- has some members but only one can occupy the location at a time
- can be declared inside a struct to be a member of it
- pointer can be declared using union-keyword

```c
union <union name> { <member declarations> };
//initialization
union <union name> <variable name>;
//member access <union variable>.<member> → last assignment overrides all previous assignments → old assignments become meaningless

typedef struct {
		int id_type; /*0 for int, 1 for char*/
		union {
			int num;
			char c[20];
		} id;
} <struct name>;
```

## Memory Management

- basic data types (int, arrays, …) → stored at stack
- dynamic memory allocation → stored at heap

Functions in: `#include <stdlib.h>`

- `malloc(<bytes>)` → returns pointer to storage of size bytes
- `calloc(<num items>, <item size>)` → returns pointer to storage with amount of items each of a specific size, often used for arrays and structures and other derived data types, memory gets initialized to 0
- `realloc(<ptr>, <bytes>)` → resizes pointed memory, does not get initialized
- `free(<ptr>)` → releases block of memory pointed by pointer
- if allocation is not successful → returns NULL → need to check if there is a NULL-pointer!
- to refer the size of the data type of the pointer use `sizeof(*<ptr>)`
- e.g. could be used to create a dynamic array that grows and shrinks depending on count of elements

## Files

Functions in `#include <stdio.h>`: → file pointer declaration: `FILE * <name>`;

- open/close:
  - `fopen(<filename>, <mode>)` → returns file pointer, if file cannot be opened NULL is returned
  - Modes:
    - r = reading, file must exist
    - w = writing, file need not exist
    - a = append, file need not exist
    - r+ = reading + writing from beginning
    - w+ = reading + writing, overwrites file
    - a+ = reading + writing appending to file
  - `fclose(<fptr>)` → closes file pointed to by fptr, returns 0 if close was successful, returns EOF (end of file) if error occurs
- writing:
  - `fputc(<char>, <fp>)` → writes character to fp
  - `fputs(<string>, <fp>)` → writes string to fp
  - `fprintf(<fp>, <string>[, <variables>])` → prints string to fp, string can contain format specifiers to insert variables
- reading:
  - `fgetc(<fp>)` → returns next character from file, EOF if end reached
  - `fgets(<buff>, <n>, <fp>)` → reads n-1 characters from fp and stores string (with \0) to buff, if line or file ends before n-1 characters, the string ends at this point
  - `fscanf(<fp>, <conversion specifier[s]>, <variable[s]>)` → reads characters from fp and stores values in variable[s] using conversion specifier[s], stops reading a string if space or newline reached

```c
#include <stdio.h>
int main() {
  //opening
  FILE *fptr;
  fptr = fopen("FILENAME", "r");

  //reading all characters
  while ((int c = getc(fptr)) != EOF) printf("%c", c);

  //closing
  fclose(fptr);
}
```

- binary file I/O:
  - Additional fopen()-modes: rb, wb, ab, rb+, wb+, ab+
  - `fwrite(<ptr>, <item_size>, <num_items>, <fp>)` → writes num_items of item_size from pointer ptr to file fp
  - `fread(<ptr>, <item_size>, <num_items>, <fp>)` → reads num_items of item_size from file fp to pointer ptr
  - `fclose(<fp>)` → closes file fp, 0 if successful, EOF if error
  - `feof(<fp>)` → returns 0 if end of file reached
- file pointer:
  - `ftell(<fp>)` → returns long int value = pointer position in number of bytes from beginning of file
  - `fseek(<fp>, <num_bytes>, <from_pos>)` → moves fp to position by num_bytes relative to position from_pos
    - from_pos can be:
      - SEEK_SET = start of file
      - SEEK_CUR = current position
      - SEEK_END = end of file

## Exceptions

- `exit(<EXIT_FAILURE=-1|EXIT_SUCCESS=1|any value>);` → stops program execution, sends exit code back to calling process, also closes all file connections and processes → ends file controlled
- error code = global variable named errno → defined in errno.h
  - need to declare errno before main as: extern int errno;
  - when using errno → set errno = 0 before calling library functions
  - output: `fprintf(stderr, <str>, errno|strerror(errno));`
- `perror(<string>)`
- `strerror(errno)` → converts errno number to string
- errno = EDOM if domain out of range
- errno = ERANGE if range error

## Preprocessor

- uses # directives to make substitutions in program source code before compilation
- to extend a directive over more lines use \ at end of a line
- code without semicolon (;)

### Directives

- `#include` = include header files
  - header file = collection of functions and macros for a library
  - header file ends with `.h` → `#include<name.h>` → searches in compiler include paths
  - for user-defined header files: `#include "name.h"` → searches in source code directory
  - stdio: input/output functions, printf and file operations
    - stdlib: memory management and other utilities
    - string: functions for handling strings
    - errno: errno global variable and error code macros
    - math: common mathematical functions
    - time: time/date utilities
- `#define`, `#undef` = define/undefine macros
  - used to create object-like macros for constants → based on values or expressions
  - can be used to define function-like macros → will be replaced by preprocessor
  - preprocessor does a direct replacement! → be aware of calculations in arguments! e.g.:
    - `#define AREA(PI*r*r)` will replace `AREA(var+1)` as `PI*var+1*var+1`
    - `#define AREA(PI*(r)*(r))` will replace `AREA(var+1)` as `PI*(var+1)*(var+1)`
- `#ifdef`, `#ifndef`, `#if`, `#else`, `#elif`, `#endif` = conditional compilation
  - e.g. use #ifdef to check if a macro is already defined to prevent double definitions
  - could also use `defined(<macro>)`
- `#pragma` = implementation and compiler specific
- `#error`, `#warning` = output and error or warning message, an error halts compilation

### Always Available Macros

- `__DATE__` = current date as string → MM DD YYYY
- `__TIME__` = current time as string → HH:MM:SS
- `__FILE__` = current filename as string
- `__LINE__` = current line number as int
- `__STDC__` = 1

### Operators

- `#define <function name>(x) #x`
  - → will convert x to a string (#-sign tells that) → spaces around argument are ignored, escape sequences get recognized → e.g. `<function name>( 12\\3 ) will be "12\3"`
- `#define <function name>(x, y) x##y`
  - → will paste x and y together
