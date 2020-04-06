# major differences between malloc/free and new/delete:

1. Constructors / Destructors Unlike malloc( sizeof(MyClass) ), the call new MyClass() calls the constructor. Similarly, delete calls the destructor.

2. Type safety malloc returns a void pointer, which needs to be cast into the appropriate data type it points to. This is not type safe, as you can freely vary the pointer type without any warnings or errors from the compiler as in the following small example: 

```cpp
MyObject *p = (MyObject*)malloc(sizeof(int));
```

In C++, the call `MyObject *p = new MyObject()` returns the correct type automatically - it is thus type-safe.

3. Operator Overloading As malloc and free are functions defined in a library, their behavior can not be changed easily. The new and delete operators however can be overloaded by a class in order to include optional proprietary behavior. We will look at an example of overloading new further down in this section.

# Creating and Deleting Objects
- As with malloc and free, a call to new always has to be followed by a call to delete to ensure that memory is properly deallocated. If the programmer forgets to call delete on the object (which happens quite often, even with experienced programmers), the object resides in memory until the program terminates at some point in the future causing a **memory leak**.

```cpp
myClass = new MyClass();
myClass->setNumber(42); // works as expected
delete myClass;
```

The call to new has the following consequences:

1. Memory is allocated to hold a new object of type MyClass
2. A new object of type MyClass is constructed within the allocated memory by calling the constructor of MyClass
3. The call to delete causes the following:
	- The object of type MyClass is destroyed by calling its destructor
	- The memory which the object was placed in is deallocated

# Overloading new and delete
One of the major advantages of new/delete over free/malloc is the possibility of overloading. While both malloc and free are function calls and thus can not be changed easily, new and delete are operators and can thus be overloaded to integrate customized functionality, if needed.

The syntax for overloading the new operator looks as follows:

```cpp
void* operator new(size_t size);
```

The operator receives a parameter size of type size_t, which specifies the number of bytes of memory to be allocated. The return type of the overloaded new is a void pointer, which references the beginning of the block of allocated memory.

**Code:**

```cpp
#include <iostream>
#include <stdlib.h>

class MyClass
{
    int _mymember;

public:
    MyClass()
    {
        std::cout << "Constructor is called\n";
    }

    ~MyClass()
    {
        std::cout << "Destructor is called\n";
    }

    void *operator new(size_t size)
    {
        std::cout << "new: Allocating " << size << " bytes of memory" << std::endl;
        void *p = malloc(size);

        return p;
    }

    void operator delete(void *p)
    {
        std::cout << "delete: Memory is freed again " << std::endl;
        free(p);
    }
};

int main()
{
    MyClass *p = new MyClass();
    delete p;
}

**To Create and Array of Objects:**
```cpp
void* operator new[](size_t size);
void operator delete[](void*);
```

**Sample Program:**

```cpp
#include <iostream>
#include <stdlib.h>

class MyClass
{
    int _mymember;

public:
    MyClass()
    {
        std::cout << "Constructor is called\n";
    }

    ~MyClass()
    {
        std::cout << "Destructor is called\n";
    }

    void *operator new[](size_t size)
    {
        std::cout << "new: Allocating " << size << " bytes of memory" << std::endl;
        void *p = malloc(size);

        return p;
    }

    void operator delete[](void *p)
    {
        std::cout << "delete: Memory is freed again " << std::endl;
        free(p);
    }
};

int main()
{
    MyClass *p = new MyClass[3]();
    delete[] p;
}
```

# Reasons for overloading new and delete:

Now that we have seen how to overload the new and delete operators, let us summarize the major scenarios where it makes sense to do this:

1. The overloaded new operator function allows to add additional parameters. Therefore, a class can have multiple overloaded new operator functions. This gives the programmer more flexibility in customizing the memory allocation for objects.

2. Overloaded the new and delete operators provides an easy way to integrate a mechanism similar to garbage collection capabilities (such as in Java), as we will shorty see later in this course.

3. By adding exception handling capabilities into new and delete, the code can be made more robust.

4. It is very easy to add customized behavior, such as overwriting deallocated memory with zeros in order to increase the security of critical application data.



