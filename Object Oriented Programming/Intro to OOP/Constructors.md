Constructors are member functions of a class or struct that initialize an object. 

> constructor: an operation that initializes (“constructs”) an object. Typically a constructor establishes an invariant and often acquires resources needed for an object to be used (which are then typically released by a destructor).

- A constructor can take arguments, which can be used to assign values to member variables.

**Sample Program:**

#include <cassert>

class Date {
 public:
  Date(int d, int m, int y) {
    Day(d);
    Month(m);
    Year(y);
  }
  int Day() { return day; }
  void Day(int d) {
    if (d >= 1 && d <= 31) day = d;
  }
  int Month() { return month; }
  void Month(int m) {
    if (m >= 1 && m <= 12) month = m;
  }
  int Year() { return year; }
  void Year(int y) { year = y; }

 private:
  int day{1};
  int month{1};
  int year{0};
};

// Test in main
int main() {
  Date date(8,29,1981);
  assert(date.Day() == 8);
  assert(date.Month() == 29);
  assert(date.Year() == 1981);
}

We can initialize an object of this class, even though this class does not explicitly define a constructor.

This is possible because of the default constructor. The compiler will define a default constructor, which accepts no arguments, for any class or structure that does not contain an explicitly-defined constructor.
