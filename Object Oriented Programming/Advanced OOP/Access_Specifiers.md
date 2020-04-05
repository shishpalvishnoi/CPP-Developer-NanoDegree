# Inherited Access Specifiers
Just as access specifiers (i.e. public, protected, and private) define which class members users can access, the same access modifiers also define which class members users of a derived classes can access.

**Public inheritance:** the public and protected members of the base class listed after the specifier keep their member access in the derived class

**Protected inheritance:** the public and protected members of the base class listed after the specifier are protected members of the derived class

**Private inheritance:** the public and protected members of the base class listed after the specifier are private members of the derived class.

```
// This example demonstrates the privacy levels
// between parent and child classes
#include <iostream>
#include <string>
using std::string;

class Vehicle {
public:
    int wheels = 0;
    string color = "blue";
    
    void Print() const
    {
        std::cout << "This " << color << " vehicle has " << wheels << " wheels!\n";
    }
};

class Car : public Vehicle {
public:
    bool sunroof = false;
};

class Bicycle : protected Vehicle {
public:
    bool kickstand = true;
    void Wheels(int w)
    {
        wheels = w;
    }
};

class Scooter : private Vehicle {
public:
    bool electric = false;
    void Wheels(int w)
    {
        wheels = w;
    }
};

int main() 
{
    Car car;
    car.wheels = 4;
    Bicycle bicycle;
    bicycle.Wheels(2);
    Scooter scooter;
    scooter.Wheels(1);
};

```
