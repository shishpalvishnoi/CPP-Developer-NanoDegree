# CMake and Make: 

- Many larger C++ projects use a build system to manage all the files during the build process. The build system allows for large projects to be compiled with a few commands, and build systems are able to do this in an efficient way by only recompiling files that have been changed.

- When we compile a project with g++, g++ actually performs several distinct tasks:

1. The preprocessor runs and executes any statement beginning with a hash symbol: #, such as #include statements. This ensures all code is in the correct location and ready to compile.
2. Each file in the source code is compiled into an "object file" (a .o file). Object files are platform-specific machine code that will be used to create an executable.
3. The object files are "linked" together to make a single executable. In the examples you have seen so far, this executable is a.out, but you can specify whatever name you want.

- It is possible to have g++ perform each of the steps separately by using the -c flag. For example,

```cpp
g++ -c main.cpp
```

will produce a main.o file, and that file can be converted to an executable with
```cpp
g++ main.o
```
**Running Multifile:** 

```cpp
g++ -c *.cpp
g++ *.o
./a.out
```

> CMake is an open-source, platform-independent build system. CMake uses text documents, denoted as CMakeLists.txt files, to manage build environments, like make.

**CMakeLists.txt**
- CMakeList.txt files are simple text configuration files that tell CMake how to build your project. There can be multiple CMakeLists.txt files in a project. In fact, one CMakeList.txt file can be included in each directory of the project, indicating how the files in that directory should be built.

- These files can be used to specify the locations of necessary packages, set build flags and environment variables, specify build target names and locations, and other actions.

**CMake Step 1:**
```cpp
cmake_minimum_required(VERSION 3.5.1)

set(CMAKE_CXX_STANDARD 14)
```

These lines set the minimum cmake version required to 3.5.1 and set the environment variable CMAKE_CXX_STANDARD so CMake uses C++ 14.

**CMake Step 2:**
CMake requires that we name the project, so we should choose a name for the project and then add the following line to CMakeLists.txt:

```cpp
project(<your_project_name>)
```

**CMake Step 3:**
Next, we want to add an executable to this project. we can do this with the add_executable command by specifying the executable name, along with the locations of all the source files that we will need. CMake has the ability to automatically find source files in a directory, but for now, we can just specify each file needed:

```cpp
add_executable(your_executable_name  path_to_file_1  path_to_file_2 ...)
```

**CMake Step 4:**
A typical CMake project will have a build directory in the same place as the top-level CMakeLists.txt.

```cpp
mkdir build && cd build
```

From within the build directory, we can now run CMake as follows:

```cpp
cmake ..
make
```

- The first line directs the cmake command at the top-level CMakeLists.txt file with ... This command uses the CMakeLists.txt to configure the project and create a Makefile in the build directory.

- In the second line, make finds the Makefile and uses the instructions in the Makefile to build the project.

**CMake Step 5:**
- If everything has worked correctly, we should now be able to run your executable from the build folder:

```
./your_executable_name
```

This executable should print the output. 

- If we don't remember the name of your executable, the last line of the make output should tell us:

```cpp
[100%] Built target <your_executable_name>
```

**CMake Step 6:**

- Now that our project builds correctly, try modifying one of the files. When we are ready to run the project again, we'll only need to run the make command from the build folder, and only that file will be compiled again. 

- In general, CMake only needs to be run once for a project, unless we are changing build options (e.g. using different build flags or changing where you store your files).

- Make will be able to keep track of which files have changed and compile only those that need to be compiled before building.

> Note: If we do re-run CMake, or if we are having problems with our build, it can be helpful to delete our build directory and start from scratch. Otherwise, some environment variables may not be reset correctly.
we can choose any name we want, but be sure to change <your_project_name> to the actual name of the project!

## CMake Review:

> CMake is a build system that uses text files named CMakeLists.txt to configure and build your project. Once the CMakeLists.txt is written, we only need the cmake and make commands to build our project again and again, so it is very convenient to use!

```cpp
cmake_minimum_required(VERSION 3.5.1)

set(CMAKE_CXX_STANDARD 14)

project(ExampleProject)

add_executable(example src/main.cpp src/vect_add_one.cpp src/increment_and_sum.cpp)
```
