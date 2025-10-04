**Tags:** [[Sysadmin]] [[Operating Systems]]

## Compilation
".o" files are called object files and contain the compiled source of the original ".c" file. In that object file there is a table containing the variables and functions to be exported, and a table containing the variable and functions to be imported (variables/functions that are used but not defined in the file). Multiple object files can be used to create one executable, and during the linking phase the references of variables and functions are replaced by their respective values and calls, creating the executable. The header files only contain "prototypes" of the functions (and also macros etc), which are basically declaring the functions, but the actual code of the function comes through the linking options (eg. `<math.h>` is the header and the option is `-lm`). The files containing these function bodies are stored under unix as *archives* with the extension ".a", so when using the option `-l[name]` the file's real name is `lib[name].a` and is generally found in /usr/lib. In order to not include header files multiple times and risk multiple definitions, you only need to include the .h file into its corresponding.c file and all other .c files where you use the library, and it will automatically import the function definitions from the library's c file.

## Tables
In the syntax `int x[i]`, x is a pointer (constant, meaning unchangeable) to the first element of the table, meaning it contains the address of the first element in the table. You need to be very careful with these because buffer overflows and segfaults can happen when there is an access to out of bound memory space.
There can also be matrices like this `char matrix[i][j]` which inside the memory, is a single table of *i* elements where each element is a table containing *j* sub-elements. To initialize a matrix, you need to specify at least *j* but not necessarily *i*, like so `int b[][4]={{1,2}, {5,6,5}};` and you don't need to specify all the elements of each column. In both a normal table and a matrix, if you don't specify a size for *i* while initializing, C will calculate it automatically.

## Pointers
When passing an address as an argument (meaning the parameter required by the function is a pointer), the address is copied into a local variable so you can't modify the pointer itself but you can modify the variable to which it points. 
`void *malloc(size_t size)` returns a pointer to the first byte of the allocated memory, and `size` is in bytes. The pointer it returns is a generic pointer (`void *`) and needs to be cast into whatever type we want it to be, usually done inside functions that are supposed to handle multiple possibilities.
Pointer arithmetic is possible, for example say *p* is a pointer and *n* is an integer, `p+1` corresponds to the first element after the elements to which *p* points, regardless of size in bytes. It is also possible to do the difference between 2 pointers (the values of the pointers, so the difference between 2 addresses), but not a difference between an address and an integer.
To pass a function as an argument to a function, we pass the pointer to the beginning of the function in memory. The arguments of the pointed to function need to be part of the poiner declaration. Example:
```
void someFunc(int (*otherFunc) (arg1,arg2,...), int someOtherArgument, ...) {
	return otherFunc(10,someOtherArgument)/2;
	/* or we could use dereferencing but we need to pay attention to the parenthesis:
	return (*otherFunc) (10,someOtherArgument)/2;
	*/
}
```

## Strings
`char str[256]` declares
## Segmentation fault
**Definition:** A memory access violation caused by a program attempting to access an illegal memory violation.
Types:
- Writing to a read-only portion of the memory
- Accessing an array out-of-bounds
- Using a variable's value as an address
- Dereferencing a null pointer
- Dereferencing or assigning to an uninitialized pointer
- Dereferencing or assigning to a freed pointer
- Buffer overflow
- Stack overflow
Use cgdb and valgrind to debug a segfault.
## Makefile
- Used to resolve dependency issues non-manually, not just in C but in a huge variety of other subjects
- The `make` program looks for a file named *Makefile* in the current directory and interprets the rules written in there
The first line indicates the name of the target file followed by a column and the list of files it depends upon. If one of the files it depends on is newer than the target file (`make` checks the last modified date) then it runs the line that is right underneath it to reconstruct the target file from the updated sources. Ex:
```
target : dep1 dep2 [...]
			(a command that does something with the deps to  produce the target)
```
This program can be used to automate just about any operations on files.
Variables are declared at the beginning of a file like so `NAME=something` and used in the rules like so `$(NAME)`. Comments start with a `#`. `%` means anything and is used similarly to a wildcard or in order to create generic rules.

## CGDB
Make sure you compiled with the `-g` option:
```
gcc -std=c99 -Wall -Wextra -g -o executable source.c
```
Start cgdb: `cgdb ./executable`
To run/stop the program: `run/kill`

| Command            | Description                                                                                                 |
| ------------------ | ----------------------------------------------------------------------------------------------------------- |
| `next`,`n`         | Go to the next instruction without entering the called functions                                            |
| `step`,`s`         | Go the next instruction and enter the called function                                                       |
| `finish`           | Exit the current function                                                                                   |
| `b n`              | Add a breakpoint at line `n`                                                                                |
| `clear n`          | Remove breakpoint at line `n`                                                                               |
| `d`                | Delete all breakpoints                                                                                      |
| `c`                | Continue execution                                                                                          |
| `print variable`   | Display the value contained in `variable`                                                                   |
| `display variable` | Just like the previous one but after the command it will display the contents of the variable at every step |
In order to deal with a `scanf` call:
1. `Run`
2. `Esc`
3. `Shift` + `T`
4. Enter the value then press `enter`

Closing the cgdb tty:
 1. `Esc`
 2. `Shift` + `T`

Leave cgdb with `quit`.

## Other remarks
- `#ifndef`, `#ifdef`,`#elif`,`#else`,`#endif`,`#define` are used for macros in C. They are also used inside header files to avoid redefining modules that are already defined. This works using a macro that is created and named after the header file right when it's loaded (eg. `my-module.h` becomes `MY_MODULE_H_`).
- Macro commands are used like copy-paste functions that can be called for frequently used commands and without wasting additional time, contrary to functions which take time to get loaded on the stack etc. Macros defined manually are done like so `#define CARRE(x) ((x) * (x))` then used just like any function, except their parameters aren't typed. 
- `extern` keyword is before the declaration of an external assembly function.
- Ternary operator in C : `(condition) ? statement1 : statement1` (meanin if condition true then do statement 1 else do statement 2).
- `__func__` is a variable that contains the name of the current function.
- Complex types:
-> Enum: `enum name {one, two, three, [...]} variable;`, you can declare a variable at the same time you define an enum, or not if you want.
-> Union: Defined the same way as a struct, it can contain multiple types of variables but only one can be used at a time. Basically, at any moment, it can contain a variable from the possible variables inside its definition, but only one of them. It forces the developer to remember the type he put in the union which is why it isn't used that much.
- Incrementing and decrementing variables when copied to another variable means that depending on the side on which are the operators, the variable being copied to takes a different value.
- Add in `static inline` before a function definition makes it an inline function, which has the same utility as a macro but more complex and advanced, it can be defined inside a header file (as well as contain a body of code, being the only thing that can do that in header files) and are used just like macros.
- `atof`,`atoi`,`atol`, are functions that convert an char variable to (respectively) a double, an int and a long.
- `char smth[];` is enough of a declaration for a string (array of chars) 