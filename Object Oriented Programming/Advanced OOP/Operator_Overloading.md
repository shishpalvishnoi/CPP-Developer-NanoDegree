In order to overload an operator, use the operator keyword in the function signature:

```cpp
Complex operator+(const Complex& addend) {
  //...logic to add complex numbers
}
```

Imagine vector addition. You might want to perform vector addition on a pair of points to add their x and y components. The compiler won't recognize this type of operation on its own, because this data is user defined. However, you can overload the + operator so it performs the action that you want to implement.

```cpp
#include <assert.h>

class Point {
public:
  // public constructor
  Point(int x = 0, int y = 0) : x(x), y(y) {}

  // + operator overload
  Point operator+(const Point& addend) {
    Point sum;
    sum.x = x + addend.x;
    sum.y = y + addend.y;
    return sum;
  }

  // attributes x and y
  int x, y;
};

// Test in main()
int main() {
  Point p1(10, 5), p2(2, 4);
  Point p3 = p1 + p2; // An example call to "operator +";
  assert(p3.x == p1.x + p2.x);
  assert(p3.y == p1.y + p2.y);
}
```
