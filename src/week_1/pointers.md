# Pointers
A pointer is a variable used to store a memory address. They can be used to access
memory and manipulate an address.

**Example 1: Various ways of declaring a pointer**
```c
// type *variable;

int *a;
int *b = 0;
int *c = NULL;
int *d = (int *) 1307;

int e = 3;
int *f = &e; // `f` is a pointer to the memory address of `e`
```

**Example 2: Dereferencing pointers**
```c
int a = 3;
int *b = &a;

printf("Values: %d == %d\nAddresses: %p == %p\n", *b, a, b, &a);
```

