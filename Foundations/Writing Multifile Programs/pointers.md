# Pointers:

> A C++ pointer is just a variable that stores the memory address of an object in your program.

a C++ program can be written without using pointers extensively (or at all). However, pointers give us better control over how our program uses memory.

## Accessing a Memory Address

Each variable in a program stores its contents in the computer's memory, and each chunk of the memory has an address number. For a given variable, the memory address can be accessed using an ampersand in front of the variable. To see an example of this, execute the following code which displays the [hexadecimal](https://en.wikipedia.org/wiki/Hexadecimal) memory addresses of the variables `i` and `j`:

```cpp
#include <iostream>
using std::cout;

int main() {
    int i = 5;
    int j = 6;
    
    // Print the memory addresses of i and j
    cout << "The address of i is: " << &i << "\n";
    cout << "The address of j is: " << &j << "\n";
}
```

> **The symbols `&` and `*` have a different meaning, depending on which side of an equation they appear.**

_This is extremely important to remember._ For the `&` symbol, if it appears on the left side of an equation (e.g. when declaring a variable), it means that the variable is declared as a reference. If the `&` appears on the right side of an equation, or before a previously defined variable, it is used to return a memory address

## Storing a Memory Address (int type)

Once a memory address is accessed, you can store it using a pointer. A pointer can be declared by using the `*` operator in the declaration. See the following code for an example:

```cpp
#include <iostream>
using std::cout;

int main() 
{
    int i = 5;
    // A pointer pointer_to_i is declared and initialized to the address of i.
    int* pointer_to_i = &i;
    
    // Print the memory addresses of i and j
    cout << "The address of i is:          " << &i << "\n";
    cout << "The variable pointer_to_i is: " << pointer_to_i << "\n";
}
```

## Getting an Object Back from a Pointer Address

Once you have a pointer, we may want to retrieve the object it is pointing to. In this case, the `*` symbol can be used again. This time, however, it will appear on the right hand side of an equation or in front of an already-defined variable, so the meaning is different. In this case, it is called the "dereferencing operator", and it returns the object being pointed to. You can see how this works with the code below:

```cpp
#include <iostream>
using std::cout;

int main() 
{
    int i = 5;
    // A pointer pointer_to_i is declared and initialized to the address of i.
    int* pointer_to_i = &i;
    
    // Print the memory addresses of i and j
    cout << "The address of i is:          " << &i << "\n";
    cout << "The variable pointer_to_i is: " << pointer_to_i << "\n";
    cout << "The value of the variable pointed to by pointer_to_i is: " << *pointer_to_i << "\n";
}
```

Although the type of object being pointed to must be included in a pointer declaration, pointers hold the same kind of value for every type of object: just a memory address to where the object is stored.

```cpp
#include <iostream>
#include <vector>
using std::cout;
using std::vector;

int main() {
    // Vector v is declared and initialized to {1, 2, 3}
    vector<int> v {1, 2, 3};
    
    // Declare and initialize a pointer to the address of v here:
    vector<int> *vp = &v;

    // The following loops over each int a in the vector v and prints.
    // Note that this uses a "range-based" for loop:
    // https://github.com/isocpp/CppCoreGuidelines/blob/master/CppCoreGuidelines.md#Res-for-range
    for (int a: v) {
        cout << a << "\n";
    }
    
    // Dereference your pointer to v and print the int at index 0 here (note: you should print 1):
    cout<<(*vp)[0]<<"\n";
}
```

## Passing Pointers to a Function

Pointers can be used in another form of pass-by-reference when working with functions. When used in this context, they work much like the references that you used for pass-by reference previously. If the pointer is pointing to a large object, it can be much more efficient to pass the pointer to a function than to pass a copy of the object as with pass-by-value.

In the following code, a pointer to an int is created, and that pointer is passed to a function. The object pointed to is then modified in the function.

```cpp
#include <iostream>
using std::cout;

void AddOne(int* j)
{
    // Dereference the pointer and increment the int being pointed to.
    (*j)++;
}

int main() 
{
    int i = 1;
    cout << "The value of i is: " << i << "\n";
    
    // Declare a pointer to i:
    int* pi = &i;
    AddOne(pi);
    cout << "The value of i is now: " << i << "\n";
}
```

## Returning a Pointer from a Function

You can also return a pointer from a function. As mentioned just above, if you do this, you must be careful that the object being pointed to doesn't go out of scope when the function finishes executing. If the object goes out of scope, the memory address being pointed to might then be used for something else.

In the example below, a reference is passed into a function and a pointer is returned. This is safe since the pointer being returned points to a reference - a variable that exists outside of the function and will not go out of scope in the function.

```cpp
#include <iostream>
using std::cout;

int* AddOne(int& j) 
{
    // Increment the referenced int and return the
    // address of j.
    j++;
    return &j;
}

int main() 
{
    int i = 1;
    cout << "The value of i is: " << i << "\n";
    
    // Declare a pointer and initialize to the value
    // returned by AddOne:
    int* my_pointer = AddOne(i);
    cout << "The value of i is now: " << i << "\n";
    cout << "The value of the int pointed to by my_pointer is: " << *my_pointer << "\n";
}
```

