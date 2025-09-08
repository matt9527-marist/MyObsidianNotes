C++ without CMake can make compiling large projects rather cumbersome. 
We need a build system to manage large projects with hundreds
or thousands of header/source files.

#CMake is a **cross-platform build system generator** that makes it easier to manage the complexity of compiling and linking large C++ projects. Instead of writing platform-specific build scripts (like Makefiles for Linux or Visual Studio project files for Windows), developers describe their project in a single `CMakeLists.txt` file. CMake then generates the appropriate build system for the host platform. 

This is especially useful for C++ projects since they often rely on external libraries, compiler options, and platform-specific settings. 

For small projects, compiling a few single files may suffice, but as the project grows, **scalability** becomes an issue. 

## CMake

Has **3 compilation steps**
![[Pasted image 20250905174213.png]]

**Efficiency of Incremental Compilation vs. Manual Tracking:**
- Compiling only changed files reduces build time significantly in larger projects. 
- Challenges to manual processing:
	- Tedious to track and manage multiple changed files manually. 
	- Risk of human error in forgetting to compile some modified files. 
*Solution*: Use a build system to automate all of this.

![[Pasted image 20250905174444.png]]
We may also create just the build subfolder inside of greeting. 
However, this may be preferable for larger parallel programs. This structure, if it is clear, it is easier to identify what functions we are using. 

Example CMakeLists.txt:
```CMake
cmake_minimum_required(VERSION 3.10)  

# Set the C++ standard to C++23  
set(CMAKE_CXX_STANDARD 23)  
set(CMAKE_CXX_STANDARD_REQUIRED ON)  

# used internally by CMake to identify your project  
project(greeting)  

# Include the directory headers are located  
include_directories(${CMAKE_SOURCE_DIR}/include)  

# Add the main executable  
add_executable(greeting src/main.cpp src/greeting.cpp)
```

#MinGW
**CMake on Windows with MinGW**
![[Pasted image 20250905174737.png]]
Execute the *cmake* command from within the "build" subfolder. It will require CMakeLists.txt properly set up in the parent directory. Executing this command will add several files used by the CMake program. 
![[Pasted image 20250905174743.png]]
Command *cmake --build .* will create the target executable file. 
![[Pasted image 20250905174757.png]]
## Catch 2
**Unit Testing via Catch2**
This is also for the larger projects that we want to generate test cases for. In massive parallel programs, such as weather forecasting or large games, programs will be executed by multiple CPUs. Two CPUs may be doing calculations and the output should be the same as when performed serially. To debug the systems to find where an error is occurring, we use Catch2. 

We define the structure as follows:
![[Pasted image 20250908192013.png]]
In this case, we need not directly install Catch2, we need only use the catch.hpp header file for Catch2.  
Obtain this file via:
github.com/catchorg/Catch2/releases/download/v2.13.7/catch.hpp

**Addition in CMakeLists.txt**
```C++
####################################################  
# Add the test executable  
add_executable(my_test src/greeting.cpp tests/test.cpp)  

# Include directories for the test target  
target_include_directories(my_test PRIVATE ${PROJECT_SOURCE_DIR}/include)  

# Enable testing  
enable_testing()  

# Register the test executable with CTest (optional)  
add_test(NAME my_test COMMAND my_test)
```
