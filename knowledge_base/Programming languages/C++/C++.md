# C++
C++ is **one of the world's most popular programming languages**. C++ can be found in today's operating systems, Graphical User Interfaces, and embedded systems. C++ is an object-oriented programming language which gives a clear structure to programs and allows code to be reused, lowering development costs.
[Wikipedia page](https://en.wikipedia.org/wiki/C%2B%2B)
C++ is extremely general purpose, which makes is capable of doing basically anything and running on basically any system (granted that you have the proper compiler for that machine's architecture/[[CPU]])
C++ can be considered to be a lower level programming language, as it requires a certain level of understanding of how machines work;
some of the notions required to be able to properly code in c++ are :
- [[Memory]]
- [[Logical Addressing]]
- [[CPU]]
- [[Operating System]]
- [[Parallel programming]] (not needed for simple programming)
- [[Mutex]] understanding (needed for threading and parallel programming)
- [[Threading]] (not needed for simple programming)
there is countless other programming notions that a good programmer would need depending on the type of project they will code (for example, Video game developers would need a good understanding of Mathematics and physics, specially if they are going to be building game engines)
>**NOTE:** it's good to note that most video games engines today are written in c++, while they might provide a more simple scripting language for end users ([[LUA]], [[Programming languages/C#]]) but the core engine is probably written in c++

C++ is still under active development with any 3rd party libraries and a massive community improving it and adding features to it.
but it's good to note that c++ is very renown for its high performance which caused by two main factors, the level of control it gives the developers who need to write high performing code, and most importantly, the amazing optimised c++ [[compilers]] out there, mainly [[GCC]] (for [[Linux]] systems) or [[MSVC]] (for [[Windows]] systems) to name a few, the compilation process of c++ would generate a very optimised machine code ([[assembly]] code), but still, the developer is responsible for creating high performing applications with well written code
## Getting started with c++
Writing c++ code is not enough, a good c++ developer needs to be able to handle the library/executable creation process, which happens after compilation, since you would often need to link multiple code files and [[headers]] together, you might even need to link external libraries. all of this is done by telling the [[compilers]] what to do via extremely long and complicated commands.
now, all of this is done with the help of frameworks/files, in the old day that would be done with [[Makefile]] which will contain the project information and then be used to compile projects, but this proved to be mostly very complicated, so a new more friendly approach is gaining popularity with the help of [[CMake]], which basically comes down to creating ``CMakeLists.txt`` files in the different folders of the project which link the libraries and files together. these ``CMakeLists.txt`` files are then used in the compilation process to generate the libraries [[executables]] and link them together