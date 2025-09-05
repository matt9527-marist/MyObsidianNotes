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
	- Tedious to track and manage multiple files



