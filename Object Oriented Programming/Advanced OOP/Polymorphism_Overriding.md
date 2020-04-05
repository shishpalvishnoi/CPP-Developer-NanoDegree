# Polymorphism: Overriding
"Overriding" a function occurs when:

- A base class declares a virtual function.
- A derived class overrides that virtual function by defining its own implementation with an identical function signature (i.e. the same function name and argument types).

```cpp
class Animal {
public:
  virtual std::string Talk() const = 0;
};

class Cat {
public:
  std::string Talk() const { return std::string("Meow"); }
};
```

# Function Hiding
- Function hiding is closely related, but distinct from, overriding.

- A derived class hides a base class function, as opposed to overriding it, if the base class function is not specified to be virtual.

```cpp
class Cat { // Here, Cat does not derive from a base class
public:
  std::string Talk() const { return std::string("Meow"); }
};

class Lion : public Cat {
public:
  std::string Talk() const { return std::string("Roar"); }
};
```

In this example, Cat is the base class and Lion is the derived class. Both Cat and Lion have Talk() member functions.

When an object of type Lion calls Talk(), the object will run Lion::Talk(), not Cat::Talk().

In this situation, Lion::Talk() is hiding Cat::Talk(). If Cat::Talk() were virtual, then Lion::Talk() would override Cat::Talk(), instead of hiding it. Overriding requires a virtual function in the base class.

# Override
"Overriding" a function occurs when a derived class defines the implementation of a virtual function that it inherits from a base class.

It is possible, but not required, to specify a function declaration as override.

```cpp
class Shape {
public:
  virtual double Area() const = 0;
  virtual double Perimeter() const = 0;
};

class Circle : public Shape {
public:
  Circle(double radius) : radius_(radius) {}
  double Area() const override { return pow(radius_, 2) * PI; } // specified as an override function
  double Perimeter() const override { return 2 * radius_ * PI; } // specified as an override function

private:
  double radius_;
};
```

- This specification tells both the compiler and the human programmer that the purpose of this function is to override a virtual function. The compiler will verify that a function specified as override does indeed override some other virtual function, or otherwise the compiler will generate an error.

- Specifying a function as override is good practice, as it empowers the compiler to verify the code, and communicates the intention of the code to future users.


