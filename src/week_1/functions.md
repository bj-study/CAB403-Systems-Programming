# Functions
A function construct in C is used to write code that solves a (small) problem.
A procedural C program is made up of one or more functions, one of them being
`main()`. A C program will always begin execution with `main()`.

Function parameters can be passed into a function in one of two ways; pass by value
and pass by reference. When a parameter is passed in via value, the data for the
parameters are copied. This means any changes to said variables within the function
will not affect the original values passed in. Pass by reference on the other hand
passes in the memory address of each variable into the function. This means that
changes to the variables within the function will affect the original variables.

**Example 1: Function control**
```c
#include <stdio.h>

void prn_message(const int k);

int main(void) {
    int n;

    printf("There is a message for you.\n");
    printf("How many times do you want to see it?\n");

    scanf("%d", &n);

    prn_message(n);

    return 0;
}

void prn_message(const int k) {
    printf("Here is the message:\n");

    for (size_t i = 0; i < k; i++) {
        printf("Have a nice day!\n");
    }
}
```

**Example 2: Pass by values**
```c
#include <stdio.h>

void swapx(int a, int b);

int main(void) {
    int a = 10;
    int b = 20;

    // Pass by value
    swapx(a, b);

    printf("within caller - a: %d, b: %b\n", a, b); // "within caller - a: 10, b: 20"

    return 0;
}

void swapx(int a, int b) {
    int temp;

    temp = a;
    a = b;
    b = temp;

    printf("within function - a: %d, b: %b\n", a, b); // "within function - a: 20, b: 10"
}
```

**Example 3: Pass by value**
```c
#include <stdio.h>

void swapx(int *a, int *b);

int main(void) {
    int a = 10;
    int b = 20;

    // Pass by reference
    swapx(&a, &b);

    printf("within caller - a: %d, b: %b\n", a, b); // "within caller - a: 20, b: 10"

    return 0;
}

void swapx(int *a, int *b) {
    int temp;

    temp = *a;
    *a = *b;
    *b = temp;

    printf("within function - a: %d, b: %b\n", *a, *b); // "within function - a: 20, b: 10"
}
```

