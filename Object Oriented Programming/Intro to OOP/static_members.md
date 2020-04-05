# Static Members:
Class members can be declared static, which means that the member belongs to the entire class, instead of to a specific instance of the class. More specifically, a static member is created only once and then shared by all instances (i.e. objects) of the class. That means that if the static member gets changed, either by a user of the class or within a member function of the class itself, then all members of the class will see that change the next time they access the static member.

static members are declared within their class (often in a header file) but in most cases they must be defined within the global scope. That's because memory is allocated for static variables immediately when the program begins, at the same time any global variables are initialized.

```
#include <cassert>

class Foo {
 public:
  static int count;
  Foo() { Foo::count += 1; }
};

int Foo::count{0};

int main() {
  Foo f{};
  assert(Foo::count == 1);
}
```

- An exception to the global definition of static members is if such members can be marked as constexpr. In that case, the static member variable can be both declared and defined within the class definition:

```
struct Kilometer {
  static constexpr int meters{1000};
};
```

## Static Method:
In addition to static member variables, C++ supports static member functions (or "methods"). Just like static member variables, static member functions are instance-independent: they belong to the class, not to any particular instance of the class.

**One corollary to this is that we can method invoke a static member function without ever creating an instance of the class.**


