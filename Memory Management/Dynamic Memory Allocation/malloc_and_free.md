# Allocating Dynamic Memory
- To allocate dynamic memory on the heap means to make a contiguous memory area accessible to the program at runtime and to mark this memory as occupied so that no one else can write there by mistake.

- To reserve memory on the heap, one of the two functions malloc (stands for Memory Allocation) or calloc (stands for Cleared Memory Allocation) is used. The header file stdlib.h or malloc.h must be included to use the functions.

- Here is the syntax of malloc and calloc in C/C++:

```cpp
pointer_name = (cast-type*) malloc(size);
pointer_name = (cast-type*) calloc(num_elems, size_elem);
```

- **malloc** is used to dynamically allocate a single large block of memory with the specified size. It returns a pointer of type void which can be cast into a pointer of any form.

- **calloc** is used to dynamically allocate the specified number of blocks of memory of the specified type. It initializes each block with a default value '0'.

Both functions return a pointer of type void which can be cast into a pointer of any form. If the space for the allocation is insufficient, a NULL pointer is returned.

```cpp
int *p = (int*)malloc(sizeof(int));
```

- At compile time, only the space for the pointer is reserved (on the stack). When the pointer is initialized, a block of memory of sizeof(int) bytes is allocated (on the heap) at program runtime. The pointer on the stack then points to this memory location on the heap.

```cpp
struct MyStruct {
    int i; 
    double d; 
    char a[5];
};

MyStruct *p = (MyStruct*)calloc(4,sizeof(MyStruct));
p[0].i = 1; p[0].d = 3.14159; p[0].a[0] = 'a';
```

## Realloc:

- The size of the memory area reserved with malloc or calloc can be increased or decreased with the realloc function.

```cpp
pointer_name = (cast-type*) realloc( (cast-type*)old_memblock, new_size );
```

To do this, the function must be given a pointer to the previous memory area and the new size in bytes. Depending on the compiler, the reserved memory area is either 
(a) expanded or reduced internally (if there is still enough free heap after the previously reserved memory area) or 
(b) a new memory area is reserved in the desired size and the old memory area is released afterwards.

> The data from the old memory area is retained, i.e. if the new memory area is larger, the data will be available within new memory area as well. If the new memory area is smaller, the data from the old area will be available only up until the site of the new area - the rest is lost.

## Freeing up Memory
- If memory has been reserved, it should also be released as soon as it is no longer needed. If memory is reserved regularly without releasing it again, the memory capacity may be exhausted at some point. If the RAM memory is completely used up, the data is swapped out to the hard disk, which slows down the computer significantly.

```cpp
free(p);
```

- The free function releases the reserved memory area so that it can be used again or made available to other programs. To do this, the pointer pointing to the memory area to be freed is specified as a parameter for the function. 

## Important

**Some things should be considered with dynamic memory management, whose neglect in some cases might result in unpredictable program behavior or a system crash - in some cases unfortunately without error messages from the compiler or the operating system:**

1. free can only free memory that was reserved with malloc or calloc.

2. free can only release memory that has not been released before. Releasing the same block of memory twice will result in an error.

3. Memory allocated with malloc or calloc is not subject to the familiar rules of variables in their respective scopes. This means that they exist independently of block limits until they are released again or the program is terminated. However, the pointers which refer to such heap-allocated memory are created on the stack and thus only exist within a limited scope. As soon as the scope is left, the pointer variable will be lost - but not the heap memory it refers to.
