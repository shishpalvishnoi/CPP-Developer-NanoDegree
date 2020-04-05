# Templates

Templates enable generic programming by generalizing a function to apply to any class. Specifically, templates use types as parameters so that the same implementation can operate on different data types.

At compile time, the compiler then expands the code using the types that are passed as parameters.

```
template <typename Type> Type Sum(Type a, Type b) { return a + b; }

int main() 
{ 
    std::cout << Sum<double>(20.0, 13.7) << "\n"; 
}
```

Sum() is defined with a template, when the program calls Sum() with doubles as parameters, the function expands to become:

```
double Sum(double a, double b) {
    return a+b;
}
```
