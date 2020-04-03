# Structures:

**Structures** allow us to create our own types ("user-defined" types) to aggregate data relevant to our needs.

**Sample Program:**
```
#include <cassert>
#include <iostream>

struct Date {
  int day = 1;
  int month = 1;
  int year = 2000;
};

int main() {
  //Create an Instance of the Date Structure
  Date date;
  assert(date.day == 1);
  assert(date.month == 1);
  assert(date.year == 2000);
  std::cout << date.day << "/" << date.month << "/" << date.year << "\n";
}
```

# Access Specifiers:

- Members of a structure can be specified as public or private.

-  By default, all members of a structure are public, unless they are specifically marked private.

- Public members can be changed directly, by any user of the object, whereas private members can only be changed by the object itself.

## Accessors And Mutators:

> To access private members, we typically define public "accessor" and "mutator" member functions (sometimes called "getter" and "setter" functions).

**Sample Code:**
```
#include <cassert>
#include <iostream>

// TODO: Define public accessors and mutators for the private member variables
struct Date {
 public:
    int Day() { return day; }
    void Day(int d) { day = d; }
    int Month() { return month; }
    void Month(int m) { month = m; }
    int Year() { return year; }
    void Year(int y) { year = y; }
 private:
  int day{1};
  int month{1};
  int year{0};
};

int main() {
  Date date;
  date.Day(29);
  date.Month(8);
  date.Year(1981);
  assert(date.Day() == 29);
  assert(date.Month() == 8);
  assert(date.Year() == 1981);
  std::cout << date.Day() << "/" << date.Month() << "/" << date.Year() << "\n";
}
```
