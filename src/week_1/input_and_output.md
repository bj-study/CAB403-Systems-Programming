# Input and Output

## `printf()`
`printf()` is an output function included in `stdio.h`. It outputs a character
stream to the standard output file, also known as `stdout`, which is normally
connected to the screen.

It takes 1 or more arguments with the first being called the control string.

Format specifications can be used to interpolate values within the string. A
format specification is a string that begins with `%` and ends with a conversion
character. In the above example, the format specifications `%s` and `%d` were used. 
Characters in the control string that are not part of a format specification are 
placed directly in the output stream; characters in the control string that are 
format specifications are replaced with the value of the corresponding argument.

**Example 1: Output with `printf()`**
```c
printf("name: %s, age: %d\n", "John", 24); // "name: John, age: 24"
```

## `scanf()`
`scanf()` is an input function included in `stdio.h`. It reads a series of characters
from the standard input file, also known as `stdin`, which is normally connected
to the keyboard.

It takes 1 or more arguments with the first being called the control string.

**Example 2: Reading input with `scanf()`**
```c
char a, b, c, s[100];
int n;
double x;

scanf("%c%c%c%d%s%lf", &a, &b, &c, &n, n, &x);
```

## Relevant Links
- [cppreference - printf](https://en.cppreference.com/w/c/io/fprintf)
- [cppreference - scanf](https://en.cppreference.com/w/c/io/fscanf)
