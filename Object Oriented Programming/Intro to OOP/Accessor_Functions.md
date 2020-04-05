**Accessor functions** are public member functions that allow users to access an object's data, albeit indirectly.

**const:** 
- Accessors should only retrieve data. They should not change the data stored in the object.

- The main role of the const specifier in accessor methods is to protect member data. When you specify a member function as const, the compiler will prohibit that function from changing any of the object's member data.

**Mutator Functions:**
- A mutator ("setter") function can apply logic ("invariants") when updating member data.
