eader files, or .h files, allow related function, method, and class declarations to be collected in one place. The corresponding definitions can then be placed in .cpp files. The compiler considers a header declaration a "promise" that the definition will be found later in the code, so if the compiler reaches a function that hasn't been defined yet, it can continue on compiling until the definition is found. This allows functions to be defined (and declared) in arbitrary order.

## Single File Code:
```cpp
#include <iostream>
#include <vector>
using std::vector;
using std::cout;


int IncrementAndComputeVectorSum(vector<int> v) {
    int total = 0;
    AddOneToEach(v);

    for (auto i: v) {
        total += i;
    }
    return total;
}

void AddOneToEach(vector<int> &v) {
    for (auto& i: v) {
        i++;
    }
}

int main() {
    vector<int> v{1, 2, 3, 4};
    int total = IncrementAndComputeVectorSum(v);
    cout << "The total is: " << total << "\n";
}

```

# Multifile Code:

**vect_add_one.h:**

```cpp
#ifndef VECT_ADD_ONE_H
#define VECT_ADD_ONE_H

#include <vector>
using std::vector;

// AddOneToEach method declaration.
void AddOneToEach(vector<int> &v);

#endif
```

**vect_add_one.cpp:**
```cpp
#include "vect_add_one.h"

void AddOneToEach(vector<int> &v) 
{
    for (auto& i: v) {
        i++;
    }
}

increment_and_sum.h

#ifndef INCREMENT_AND_SUM_H
#define INCREMENT_AND_SUM_H

#include <vector>
using std::vector;

// IncrementAndComputeVectorSum method declaration.
int IncrementAndComputeVectorSum(vector<int> v);

#endif
```

**increment_add_sum.cpp:**

```cpp
#include "vect_add_one.h"

int IncrementAndComputeVectorSum(vector<int> v) {
    int total = 0;
    AddOneToEach(v);

    for (auto i: v) {
        total += i;
    }
    return total;
}
```

**main.cpp:**
```cpp
#include <iostream>
#include <vector>
#include "increment_and_sum.h"
using std::vector;
using std::cout;

int main() 
{
    vector<int> v{1, 2, 3, 4};
    int total = IncrementAndComputeVectorSum(v);
    cout << "The total is: " << total << "\n";
}
```

- vect_add_one.h is included in increment_and_sum.cpp.
- Only the header file needs to be included in another file.


**Run Code:**

` g++ -std=c++17 ./code/main.cpp ./code/increment_and_sum.cpp ./code/vect_add_one.cpp && ./a.out `


