
# Classes: 

- Classes, like structures, provide a way for C++ programmers to aggregate data together in a way that makes sense in the context of a specific program.
- By convention, we use structures when member variables are independent of each other, and use classes when member variables are related by an "invariant".

## Invariants:

- An "invariant" is a rule that limits the values of member variables.

- By default, all members of a struct default to public, whereas all members of a class default to private.

**Sample Code:**

```
#include <iostream>
#include <cassert>

class Date {
 public:
  int Day() { return day; }
  void Day(int d) {
    if (d >= 1 && d <= 31) day = d;
  }
    int Month() { return month; }
    void Month(int m) {
        if(m >= 1 && m <= 12)
            month = m;
    }
    int Year() { return year; }
    void Year(int y) {
        year = y;
    }

 private:
  int day{1};
  int month{1};
  int year{0};
};

// Test in main
int main()
{
    Date date;
    date.Day(-1);
    date.Month(14);
    date.Year(2000);
    assert(date.Day() != -1);
    assert(date.Month() != 14);
    assert(date.Year() == 2000);
    std::cout << date.Day() << "/" << date.Month() << "/" << date.Year() << "\n";
}
```
