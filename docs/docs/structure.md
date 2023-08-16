# Structure of a CMake package

Occasionally one needs to modify a CMake package in order to make it work and being able to recognize the different components of a CMake package is useful knowledge even when one is not developing a CMake package. This page gives an overview of the structure of a CMake package.
A CMake package needs to contain at least one `CMakeLists.txt` file.
This file describes the cmake package.

```cmake
cmake_minimum_required(VERSION 3.2)
project( wind_tunnel LANGUAGES FORTRAN CUDA )

option(USE_CUDA "Enable using CUDA for optimization" ON )
option(TESTS "Enable Tests" OFF )

find_package(OpenMP REQUIRED)

add_subdirectory( src )

enable_testing()

add_subdirectory(tests)
```

The example code above contains the typical structure of a CMake package.

- define the **project** name and languages: C/C++, Fortran, Python and Cuda are all supported langauges
- **variables**: define cmake variables. Some of them can be set by the user at configure time
- **options**: A special case of variables. These are logical variables which can be turned on or off by the user at configure time. They can be used to enable compilation of additional components or providing support for additional parallel paradigms. In this example the option is used tu turn on/off support for gpu.
- **include subdirectories**: CMake projects are often modular. Often subdirectories will contain different components of the project. Each directory will contain its own *CMakeLists.txt* describing its own build process . 
- **find_package** : This command looks for a specific package. You can optionally specify if the package is optional or if it is required for a successful build. Call to `find_package` obtain need hints from  the user in order to find the correct packages. In this example cmake looks if the compiler has support for OpenMP and figure out which flag needs to be added.
- **tests** : CMake contains a mechanism to run tests called `ctest`. These need to be explicitly enabled.

## Adding targets