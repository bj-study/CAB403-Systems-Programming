# Strings
A string is a one-dimensional array of type `char`. All strings must end with a
null character `\0` which is a byte used to represent the end of a string.

A character in a string can
be accessed either by an element in an array of by making use of a pointer.

**Example 1: Strings in practice**
```c
char *first = "john";
char last[6];

last[0] = 's';
last[1] = 'm';
last[2] = 'i';
last[3] = 't';
last[4] = 'h';
last[5] = '\0';

printf("Name: %s, len: %lu", first, strlen(first));
```

## Relevant Links
- [Wikipedia - Null-terminated string](https://en.wikipedia.org/wiki/Null-terminated_string)
