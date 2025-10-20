**Tags:** [[Programming]]

`splice(@array,offset,length,list);` removes an element from an array. if length and list are not specified, it removes everything after the offset index. if length is specified, it removes from the offset and counts up to the specified length and returns the values that are removed.

print "something\n"; for printing to the console. Arguments can be surrounded by parentheses.

Comments start with `#` on each line, embedded documentation is surrounded by an = at the beginning of a line to start and a =cut to stop, and can be on multiple lines.

Quotations and interpolation are just like Ruby.

Every statement in Perl must end with a semicolon.

Scalars contain single string or numeric values and are preceded with a `$`.
Arrays contain a set of scalars and are preceded by a `@`.
Hashes contain a set of key-value pairs and are preceded by a `%`.
Perl has no boolean data type. Instead, anything that symbolizes null, is considered false in the context of condition evaluation, namely, 

`keys %hash_name` and `values %hash_name` return arrays of the keys and values of the hash respectively.

Conditional statements in perl can be:
- `if (condition) statement`
- `if (condition) {statement1; statement2; statement3;}`
- `if (condition) statement else statement` and can also be `(condition) ? statement1 : statement2`
- `if (condition) elsif (condition) statement else statement`
- `unless (condition) statement`
- `unless (condition) statement else statement`
- `unless (condition) elsif (condition) statement else statement`

`<=>` Compares the values of two numeric values and returns -1, 0, or 1 if the left argument is numerically less than, equal to, or greater than the right argument, respectively

String operations:
- `eq` true if the left argument is stringwise equal to the right argument
- `ne` true if the left argument is stringwise not equal to the right argument
- `gt` true if the left argument is stringwise greater than the right argument
- `lt` true if the left argument is stringwise less than the right argument
- `ge` true if the left argument is stringwise greater than or equal to the right argument
- `le` true if the left argument is stringwise less than or equal to the right argument
- `cmp` -1, 0, or 1 depending on whether the left argument is stringwise less than, equal to, or greater than the right argument, respectively

`[statement] if exists $hash{$key}` executes whatever statement is passed only if the specified element exists inside the hash.

Incrementing and decrementing is simple with `++` and `--`.

Loops are simple as well, and are usually like follows `while (condition) {block;}`.
There are also `do {block;} while (condition)` loops and `foreach $var (@array) {block;}`.
`next` skips the rest of the block and executes the next iteration. `last` exits the loop like a `break`.

`@array=(1,2,3,4,5)` defines an array. To refer to an array variable, it has to be referred to as a scalar, like so `$array[0]`.
`%hash=(key1 => value1, key2 => value2)`. To refer to a value, use `$hash{key}`. Note that when interpolating inside a string, if the key is a string then the quotations need escape sequences.

`$a=$x++` will assign to `$a` the value of `$x` and to `$x` the value of `$x+1`, while `$a=++$x` will assign `$a` the value of `$x+1` and to `$x` the value of `$x+1`. And similarly with auto-decrementing.

Hex values are preceded with `0x` and binaries with `0b`.

Bitwise operators:
`&` AND - bitwise AND of the operand values from either side of the operator 
`|` OR - bitwise OR of the operand values from either side of the operator
`^` XOR - bitwise XOR of the operand values from either side of the operator
`~` NOT - bitwise INVERT (unary operator) inverts each bit of the left operand
`<<` SHIFT LEFT - bitwise SHIFT LEFT the left operand, right operand times
`>>` SHIFT RIGHT - bitwise SHIFT RIGHT the left operand, right operand times

Logical operators:
`and` Logical AND operator - return TRUE if both the operands are true, otherwise FALSE
`&&` Logical AND operator - return TRUE if both the operands are true, otherwise FALSE
`or` Logical OR operator - return TRUE if either one of the operands is true, otherwise FALSE
`||` Logical OR operator - return TRUE if either one of the operands is true, otherwise FALSE
`xor` Logical XOR operator - return TRUE if one of the operands is true and the other is false, otherwise FALSE
`not` Logical NOT operator (unary operator)- return TRUE if the operand is false, otherwise FALSE
`!` Logical NOT operator (unary operator)- return TRUE if the operand is false, otherwise FALSE

@ARGV contains the command line arguments passed when calling the script (first argument is at `
`$ARGV[0]`).

Perls' `given` statement is similar to `switch case` statements in other languages. The syntax is:
```
given(expr){
     when(expr1){ statement;}
     when(expr1){ statement;}
     when(expr1){ statement;}
     default{ $code = '';}
}
```
Perl evaluates the argument iside the given statement with the arguments in the when statement, and if the evaluation gives out true then it executes the code block.
It can also be written elegantly, this way it prints out whatever is return by the `given` statement:
```
print do{
   given($color){
     "#FF0000\n" when 'RED';
     "#00FF00\n" when 'GREEN';
     "#0000FF\n" when 'BLUE';
     default { '';}
   }
}
```

$string for string substitution inside a "print" function call

The dot operator "." converts everything to a string and concatenates it

The plus sign converts a string to a number

qw(string1 string2) initializes an array containing the strings inside the parenthesis by surrounding them with diuble quotes, easier than writing "string1", "string2", ...

while ($=<>) {} reads input one line at a time. Here, perl checks if you passed any files as arguments in the command line when calling the scripts, it sequentially opens the files and runs their contents through <> to the loop. If you didn't, it reads from stantard input. $= can be omitted since <> automatically stores each line in $ of no variable is provided

($var1, $var2) = split ',' [string] splits the string passed as argument at the specified chacacter (in this case comma) and assigns the resulting strings to the variables in order. If the string is not provided as argument, the function is applied to whatever $ contains.

$var=split ':' would assign the number of fields to the scalar $var instead of the resulting string, which is why we write it in the form of a list if we want to assign the fields themselves

$ref= [split ':'] assigns to $ref a reference to an array, which can then be stored inside a hash (hashes in perl can only contain scalars). To access elements of the array, we use the notation $ref->[index]

`if ($text =~ /regex/)` checks if `$text` matches the specified regex pattern (`$text` can be omitted if we want to work on the default variable `$_`)

m/regex/ is used to specify that we should look for a match of what is between slashes

s/regex/sub specifies that we should substitue whatever matches what is between slashes with what comes after (sub in this case)

s/regex/sub/g does the same thing but replaces all instances not just the first one

[Something] or die "string"; prints string to the screen if the previous operation (Something) failed

To open a file in reading mode `open(DATA, "<file.txt");` and in writing mode `open(DATA, ">file.txt");`

<INFILE> does the same thing as <> except it stops the loop at the EOF and doesn't go through any more files
You can use shell redirection inside the open({INFILE/OUTFILE},"here") function when specifying files (eg. you could specify a pipe)

Something if condition; is a valid syntax for conditional statements, like in ruby (with no else statement)

foreach element (elements) {dosomething;}
is pearl's loop syntax (traditional for loop also works)

A way of using case statements:
 
readline(*STDIN) to ask for user input

Variables are global by default in perl, adding the "my" keyword before the variable make them local

Perl command line option -a splits the input and stores it in a default array @F, the delimiter is whitespace by default but can be changed with the -F option

Join(string, array) puts the string between every 2 elements in the array

-i command line argument for perl modifies the input file directly, adding a suffix (eg. -i.backup~) creates a backup for the file with the provided suffix