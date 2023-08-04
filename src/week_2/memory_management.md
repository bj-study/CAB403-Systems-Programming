# Dynamic Memory Management
Memory in a C program can be divided into four categories:
1. Code memory
2. Static data memory
3. Runtime stack memory
4. Heap memory

## Code Memory
Code memory is used to store machine instructions. As a program runs,
machine instructions are read from memory and executed.

## Static Data Memory
Static data memory is used to store static data. There are two categories of
static data: global and static variables.

Global variables are variables defined outside the scope of any function as 
can be seen in example 1. Static variables on the other hand are defined with
the `static` modifier as seen in example 2.

Both global and static variables have one value attached to them; they are
assigned memory once; and they are initialised before `main` begins execution
and will continue to exist until the end of execution.

**Example 1: Global variables.**
```c
int counter = 0;

int increment(void) {
    counter++;

    return counter;
}
```

**Example 2: Static variables.**
```c
int increment(void) {
    // will be initialised once
    static int counter = 0;

    // increments every time the function is called
    counter++;

    return counter;
}
```

## Runtime Stack Memory
Runtime stack memory is used by function calls and is FILO (First in, Last out).
When a function is invoked, a block of memory is allocated by the runtime 
stack to store the information about the function call. This block of memory 
is termed as an _Activation Record_.

The information about the function call includes:
- Return address.
- Internal registers and other machine-specific information.
- Parameters.
- Local variables.

## Heap Memory
Heap memory is memory that is allocated during the runtime of the program.
On many systems, the heap is allocated in an opposite direction to the stack
and grows towards the stack as more is allocated. On simple systems without 
memory protection, this can cause the heap and stack to collide if too much
memory is allocated to either one.

To deal with this, C provides two functions in the standard library to handle
dynamic memory allocation; `calloc()` (contiguous allocation) and `malloc()`
(memory allocation).

`void *calloc(size_t n, size_t s)` returns a pointer to enough space in memory
to store `n` objects, each of `s` bytes. The storage set aside is automatically
initialised to zero.

`void *malloc(size_t s)` returns a pointer to a space of size `s` and leaves the
memory uninitialised.

**Example 3: `malloc()` and `calloc()`**
```c
#include <stdio.h>
#include <stdlib.h>

int main() {
    int num_of_elements;
    int *ptr;
    int sum = 0;
  
    printf("Enter number of elements: ");
    scanf("%d", &num_of_elements);
  
    ptr = malloc(num_of_elements * sizeof(int));
    // or
    // ptr = calloc(num_of_elements, sizeof(int));
   
    if (ptr == NULL) {
        printf("[Error] - Memory was unable to be allocated.");

        exit(0);
    }
  
    printf("Enter elements: ");

    for (int i = 0; i < n; i++) {
        scanf("%d", ptr + i);

        sum += *(ptr + i);
    }
  
    printf("Sum = %d", sum);
    
    free(ptr);
  
    return 0;
}
```

## Relevant Links
- [cppreference - malloc](https://en.cppreference.com/w/c/memory/malloc)
- [cppreference - calloc](https://en.cppreference.com/w/c/memory/calloc)
- [cppreference - realloc](https://en.cppreference.com/w/c/memory/realloc)
- [cppreference - free](https://en.cppreference.com/w/c/memory/free)
