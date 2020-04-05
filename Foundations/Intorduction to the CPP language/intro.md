# C++ Main()
In C++, every program contains a main function which is executed automatically when the program is run. Every part of a C++ program is run directly or indirectly from main, and the most basic program that will compile in C++ is just a main function with nothing else.

main() should return an integer (an int in C++), which indicates if the program exited successfully. This is specified in code by writing the return type, followed by the main function name, followed by empty arguments:

`int main(){}`

`#include <iostream>`

- The `#include` is a preprocessor command which is executed before the code is compiled. It searches for the `iostream` header file and pastes its contents into the program. `iostream` contains the declarations for the input/output stream objects.


`using std::cout;`

- Namespaces are a way in C++ to group identifiers (names) together. They provide context for identifiers to avoid naming collisions. The `std` namespace is the namespace used for the standard library.
- The `using` command adds `std::cout` to the global scope of the program. This way you can use `cout` in your code instead of having to write `std::cout`.
- `cout` is an output stream you will use to send output to the notebook or to a terminal, if you are using one.
- Note that the second two lines in the example end with a semicolon `;`. Coding statements end with a semicolon in C++. The `#include` statement is a preprocessor command, so it doesn't need one.

`cout << "Hello!" << "\n";`

- In this line, the code is using cout to send output to the notebook. The `<<` operator is the stream insertion operator, and it writes what's on the right side of the operator to the left side. So in this case, `"Message here"` is written to the output stream `cout`.
