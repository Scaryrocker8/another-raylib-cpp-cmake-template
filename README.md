# Another Raylib C++ CMake Template

This repo was originally a fork of Andrea Tupini and Matthieu Dorier's [raylib-cpp-cmake-template](https://github.com/tupini07/raylib-cpp-cmake-template).

However I wanted to break it down even further and make it as barebones as possible to start any new raylib project fresh in VSCode and C++, 
as well as be able to easily add additional libraries via CMake.

I removed the original assets and renamed the source and assets folders to more conventional C/C++ names. 

I also modified the CMakeLists.txt file to only include raylib as a dependency. 

This allows any developer who wants to use raylib in VSCode with C++ and CMake to easily get started on a brand new empty project.

If there are any fixes or quality of life changes that could be implemented please let me know!

As a C++ raylib game dev scrub I also wanted to include some tips I painfully learned to help get started with this template...


## How to actually build this

To actually compile and run this you'll need VSCode's C/C++ Extension, CMake, a compiler and a debugger.

Some common compilers include MinGW(Windows), Clang(Mac) or GCC(Linux), but there are dozens to choose from.

Some common debuggers include WinDbg and x64dbg(Windows), LLDB(Mac) or GDB(Linux). Again, there are dozens others to choose from.

CMake is needed to build the project with the CMakeLists.txt file that is included. 

Once these are all installed, when your open this template in VSCode for the first time, a compiler kit will need to be chosen.

Once chosen, raylib-build, raylib-src and raylib-subbuild should build and be added to the "build/_deps" folder.

Once raylib is built, just hit F5 and you should see the raylib core basic window pop up!


## How to change project name and built executable

To change the project name and built executable you must change the name in ALL 3 locations...

In the .vscode folder:

- launch.json - "program": "${workspaceRoot}/build/[your project name here]"

- tasks.json - "targets": ["your project name here"],

In the root directory:

- CMakeLists.txt - project("your project name here")

All three locations MUST have the EXACT SAME name for raylib to build and run in VSCode. This took me FOREVER to figure out. 

I'm hoping this can maybe at least also help anybody else struggling to get VSCode to build C/C++ projects properly.


## How to add additional libraries

Additional libraries will need to be added via the CMakeList.txt file in root.

To add additional libraries, you'll need to.

1. Open up the CMakeLists.txt file

2. Under "## ADD ANY ADDITIONAL PROJECT DEPENDENCIES HERE ---", see how raylib is being added as a dependency. 

Copy and paste raylib's dependency structure and replace the name, git link, and version with any git repository you would like to include.

(To keep your project size smaller, you can also choose what to disclude when building dependencies.

For raylib, in example, we are discluding BUILD_EXAMPLES and BUILD_GAMES, as these are not needed in our project and only take up space.)

3. Under "## TARGET LINK LIBRARIES HERE ---", make sure you also LINK any additional dependencies you add. This step is HIGHLY missable, and will not allow your project to build if a dependency link is missing.

To link, just copy how raylib is being linked, and paste with the added library you want to link. Whether you want it linked as PRIVATE, PUBLIC or INTERFACE is up to you, but most libraries used with raylib are static.

[Ted James][Examples of when PUBLIC/PRIVATE/INTERFACE should be used in cmake](https://medium.com/@fixitblog/solved-examples-of-when-public-private-interface-should-be-used-in-cmake-7382b6a7d1ed)


## Additional Resources

For a better understanding of CMake and how C/C++ projects are built in general, I would highly recommend these videos that helped me. Although you could always just use a template,
It's better to understand exactly how your computer is building your projects under the hood, as it will help with debugging larger projects and issues in the later future!

[Michael Forest][C++ Libraries For Beginners](https://youtu.be/a5kUr-u2UNo?si=C7f1WMmUve_uo0-f)

[Code, Tech, and Tutorials][How-To Use C++ Libraries (without relying on a package manager)](https://youtu.be/xBfwQv8mxCI?si=VpASive06ipGMDw7)

[Code, Tech, and Tutorials][How To Use VS Code for C++ | With CMake & Any Compiler](https://youtu.be/gGxi500Q5uE?si=TkOn5I2dG4argsQ4)

Thank you for downloading, and happy raylibing!

Created by Jonnie Gieringer