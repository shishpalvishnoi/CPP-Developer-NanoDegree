# Abstraction:

**Abstraction** refers to the separation of a class's interface from the details of its implementation. The interface provides a way to interact with an object, while hiding the details and implementation of how the class works.

**Example:**
The String() function within this Date class is an example of abstraction.

**Sample Program:**

```
class Date {
 public:
  ...
  std::string String() const;
  ...
};

```

- The user is able to interact with the Date class through the String() function, but the user does not need to know about the implementation of either Date or String().

- For example, the user does not know, or need to know, that this object internally contains three int member variables. The user can just call the String() method to get data.

- If the designer of this class ever decides to change how the data is stored internally -- using a vector of ints instead of three separate ints, for example -- the user of the Date class will not need to know.

> Abstraction is used to expose only relevant information to the user. By hiding implementation details, we give ourselves flexibility to modify how the program works.
