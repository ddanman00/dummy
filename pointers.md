## Pointers

### Void Pointer

- Void pointer is a pointer which has no associated data type with it.
- It can point to any data of any data type and can be type casted to any type.

Example:
~~~C
int main() {
    int n = 10;
    void *ptr = &n;

    printf("%d", *(int*)ptr);
    return 0;
}
~~~
Output: 10
- We cannot dereference a void pointer.

Uses:
- malloc and calloc function returns a void function. Due to this they can allocate a memory for any data type.

### Null Pointer

- A NULL Pointer is a pointer that does not point to any memory location. It represents an invalid memory location.
- When a NULL value is assigned to a pointer, then the pointer is considered as a NULL pointer.

Example:
~~~C
int main() {
    int *ptr = NULL;
    return 0;
}
~~~

Uses:
- It is used to initialize a pointer when that pointer isn't assigned any valid memory address yet.
- Useful for handling errors when using the malloc function.  

Facts:
- The value of NULL is 0. We can either use NULL or 0, but this 0 is written in context of pointers and is not equivalent to the integer 0.
- Size of the NULL pointer depends upon the platform and is similar to the size of the normal pointers.

Best Practices:
- Initialize a pointer as NULL, and not 0.
- Perform NULL check before dereferencing any pointer to avoid surprises.

### Dangling Pointer

- A dangling pointer is a pointer which points to some non-existing memory location.

Example 1:
~~~C
int main() {
    int *ptr = (int *)malloc(sizeof(int));
    // statements
    // statements

    free(ptr);
    // here we are freeing the allocated memory, but it still points to that deacllocated memory, which currently does not exist.

    // to fix that, we just re-initialise it to NULL.
    ptr = NULL;
    return 0;
}
~~~

Example 2:
~~~C
#include <stdio.h>

int* fun() {
    int num = 10;
    return &num;
}

int main() {
    int *ptr = NULL;
    ptr = fun();
    printf("%d", *ptr);
    return 0;
}
~~~
Output: Segmentation fault
- When we are trying to return the address of the `num` variable from the `fun` function, the `num` variable is local to that function only, and upon execution of the function, the variable will not exist, and so it is basically like deallocated memory.
- Seg fault is basically trying to access illegal memory.

### Wild Pointer

- Also known as uninitialized pointers.
- These pointers usually point to some arbitrary memory location and may cause a program to crash or misbehave.

Example:
~~~C
int main() {
    int *p;     // wild pointer
    *p = 10;
    return 0;
}
~~~

How to avoid:
- Initialize them with the address of a known variable.
- Explicitly allocate the memory and put the values in the allocated memory.