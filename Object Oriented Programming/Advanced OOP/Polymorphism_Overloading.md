# Polymorphism
Polymorphism is means "assuming many forms".

In the context of object-oriented programming, polymorphism describes a paradigm in which a function may behave differently depending on how it is called. In particular, the function will perform differently based on its inputs.

**Polymorphism can be achieved in two ways in C++: overloading and overriding.** In this exercise we will focus on overloading.

## Overloading
In C++, you can write two (or more) versions of a function with the same name. This is called "overloading". Overloading requires that we leave the function name the same, but we modify the function signature. For example, we might define the same function name with multiple different configurations of input arguments.

```cpp
#include <iostream>

class Human {};
class Dog {};
class Cat {};

void hello() { std::cout << "Hello, World!\n"; }

void hello(Human human) { std::cout << "Hello, Human!\n"; }
void hello(Dog dog) { std::cout << "Hello, Dog!\n"; }
void hello(Cat cat) { std::cout << "Hello, Cat!\n"; }

int main()
{
    hello();
    hello(Human());
    hello(Dog());
    hello(Cat());
}
```
