# Memory Management Problems:

1. **Memory Leaks:** Memory leaks occur when data is allocated on the heap at runtime, but not properly deallocated. A program that forgets to clear a memory block is said to have a memory leak.

2. Buffer Overruns Buffer overruns occur when memory outside the allocated limits is overwritten and thus corrupted.

3. Uninitialized Memory Depending on the C++ compiler, data structures are sometimes initialized (most often to zero) and sometimes not. So when allocating memory on the heap without proper initialization, it might sometimes contain garbage that can cause problems.

4. Incorrect pairing of allocation and deallocation Freeing a block of memory more than once will cause a program to crash.

5. Invalid memory access This error occurs then trying to access a block of heap memory that has not yet or has already been deallocated.
