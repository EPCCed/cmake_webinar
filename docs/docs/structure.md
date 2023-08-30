# Writing a CMake package

Occasionally one needs to modify a CMake package in order to make it work and being able to recognize the different components of a CMake package is useful knowledge even when one is not developing a CMake package. This page gives an overview of how a CMake package is written, without going into too many details.

## Targets

A **target** defines an object to be build by cmake. A target may be either an *executable* or a *library*. Each target have a set of properties which define how the target is built. Valid target properties are file sources, compiling flags , link flags, libraries to link with etc..

<figure markdown>
![Compilation process](images/targets.png)
<figcaption> The output executable my_exec is defined as a target. In order to build the target, we set the target properties source_files and link_libraries. A property can contain a list of elements and those elements can be other targets.</figcaption>
</figure>
To define an executable we can type
```cmake
add_executable( my_exec source1.f90 source2.f90 )
```
The command `add_executable` defines a target named `my_exec` . Successive arguments will set the sources property of the target. The property is set to a list of source files used to build the target.

```cmake
target_link_libraries( my_exec  MPI::MPI_Fortran)
``` 

The command `target_link_libraries` sets the `link_libraries` property for a target. The property tells cmake which libraries to link with when creating the executable.

```cmake
target_include_directories( my_exec PUBLIC ${MPI_FORTRAN_DIRS} )
```

The `include_directories` property tells CMake which files should be included when compiling the executable. For `C/C++` this may be a directory containing header files , while for `Fortran` one many wish to include a directory containing module source files.
Here the variable ${MPI_FORTRAN_DIRS contains a list of directories with the MPI header files. The list of directories is preceded by the declaration `PUBLIC`. The declaration tells cmake that the property should be forwarded to other targets who depent on `my_exec`.
Valid accessor values are

- **PUBLIC** : the property gets forwarded to targets which depend on the current target.
- **PRIVATE** : the property is used for the current target and is forwarded to other targets which depend on the current target
- **INTERFACE** : the property is not used for the current target, but is forwarded to other targets which depends on the current target


## Structure of a CMake project
A CMake package needs to contain at least one `CMakeLists.txt` file.
This file describes the cmake package using the CMake programming language. The CMake programming language is a complete programming language. One can define variables, conditionals , loops and all the features you may expect from a modern programming language.

### Project definition

The file starts by defining the minimum version of cmake cmake and which compiler languages are supported.
Then one defines the **project** . The command takes as arguments the name of the project and a list of languages used to write the package.
```cmake
cmake_minimum_required(VERSION 3.2)
project( wind_tunnel LANGUAGES FORTRAN CUDA )
```
### Variables

A package can define custom variables. CMake variables are usually local in scope to the function that they are defined with. Outside of a function, they are local to the subdirectory. Hence, a variable defined in a subfolder will not be accessible from the parent directory. The main exception are variables defined as `CACHE` which are global variables. `CACHE` variables can be accessed from anywhere in the project, no matter where they are defined and their values are preserved between different cmake invocations.

```cmake
set( USE_CUDA OFF)
```
The value of a variable can be accessed by prefixing with a `$` sign

```cmake
${USE_CUDA}
```

### Options
These are logical variables which can be turned on or off by the user at configure time. They can be used to enable compilation of additional components or providing support for additional parallel paradigms. In this example the option is used to turn on/off support for gpu.
```cmake

option(USE_CUDA "Enable using CUDA for optimization" ON )
```

### Include subdirectories

CMake projects are often modular, whith different components in separate directories. Each directory often contains its own *CMakeLists.txt* describing the build process for that component.

```cmake
add_subdirectory( src )
```

### find_package

This command looks for a specific package. The recipe will be defined in a `Find<Packagename>.cmake` file. You can optionally specify if the package is optional or if it is required for a successful build. The command `find_package` will look for the package in a [pre-defined set of directories](https://cmake.org/cmake/help/latest/command/find_package.html?highlight=find_package#search-procedure) and will return the first one it finds. If no package is found and the package is marked as required a fatal error will be thrown.If a package is found it will define targets and/or variables which can used later in the project.

### Tests
 CMake contains a mechanism to run tests called `ctest`. These need to be explicitly enabled.