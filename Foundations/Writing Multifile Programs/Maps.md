# Maps: 

- **Container data structures are fantastic for storing ordered data, and classes are useful for grouping related data and functions together, but neither of these data structures is optimal for storing associated data.**

- A map (alternatively hash table, hash map, or dictionary) is a data structure that uses key/value pairs to store data, and provides efficient lookup and insertion of the data.

In the following notebook, we will learn how to use an unordered_map, which is the C++ standard library implementation of a map. Although C++ has several different implementations of map data structures which are similar, unordered_map is the structure that we will use in our project.

```cpp
#include <iostream>
#include <vector>
#include <unordered_map>
#include <string>
using std::vector;
using std::cout;
using std::unordered_map;
using std::string;


int main() {
    // Create strings to use in the hash table.
    string key = "word";

    string def_1 = "a unit of language, consisting of one or more spoken sounds or their written representation, that functions as a principal carrier of meaning";
    string def_2 = "speech or talk: to express one's emotion in words";
    string def_3 = "a short talk or conversation: 'Marston, I'd like a word with you.'";
    string def_4 = "an expression or utterance: a word of warning";

    unordered_map <string, vector<string>> my_dictionary;

    // Check if key is in the hash table.
    if (my_dictionary.find(key) == my_dictionary.end()) {
        cout << "The key 'word' is not in the dictionary." << "\n";
        cout << "Inserting a key-value pair into the dictionary." << "\n\n";
        // Set the value for the key.
        my_dictionary[key] = vector<string> {def_1, def_2, def_3, def_4};
    }

    // The key should now be in the hash table. You can access the
    // value corresponding to the key with square brackets [].
    // Here, the value my_dictionary[key] is a vector of strings.
    // We iterate over the vector and print the strings.

    cout << key << ": \n";

    auto definitions = my_dictionary[key];

    for (string definition : definitions) {
        cout << definition << "\n";
    }
}
```


