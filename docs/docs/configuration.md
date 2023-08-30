# Configuring a build

When building a package one often needs to configure the build. One may need to specify which compiler to use or turn on/off some functionality in the package, specify which libraries to link with and what compiler to use.



## Setting variables

When compiling a package often a package defines some variables that can be set by the user. Some of these variables are builtin in the cmake framework, while other are set by the user.

### Listing variables

A list of all variables, including variables defined by the cmake package and built-in variables, can be found with

```bash
cmake ${CMAKE_PACKAGE_DIRECTORY} -LHA
```

by using the options

- `-L` : list all variables
- `-A` : list all advanced variables. Variables marked as `advanced` are hidden by default and usually do not need to be changed by the package user.
- `-H` : show helper strings. An helper string is associated with a variable and is meant to provide a description of the variable.

An alternative option is to use the interactive tool

```bash
ccmake ${CMAKE_PACKAGE_DIRECTORY}
```
This will open an interactive program. The user interface allows to view and modify variables which can be defined by the user.

### Specifying variables
One you know the name of a variable and which value you want to set it to, you can specify a variable at configure time by adding the argument `-DVAR_NAME=${VAR_VALUE}`
```
cmake ${CMAKE_PACKAGE_DIRECTORY} -DVAR_NAME=${VAR_VALUE}
```
In the example above one configures the project by defining a variable named `VAR_NAME` and setting its value to `${VAR_VALUE}`.

### Builtin variables

Some variables defined by CMake are commonly used on many projects.

- **CMAKE_BUILD_TYPE**: This can be set to one of Debug, Release, RelWithDebInfo, MinSizeRel. It an be used to turn on optimization flags ( Release ) or debugging flags ( Debug )
- **CMAKE_INSTALL_PREFIX**: Directory where to copy targets after being built. After running the install step, this directory will contain any binary, library and header file built by CMake.

A list of all pre-defined variables can be obtained with

```bash
cmake --help-variable-list
```

## Specifying the compilers

Most CMake projects will require a compiler. If not specified CMake will look for one compiler and use the first it finds.
!!! Warning
    If multiple compilers are present on the system cmake may find the wrong compiler, without returning any error. This may result in errors at building or run time.
The easier way to specify a variable is to set an environment variable before configuring the project. The name of the variable will depend on the choice of compiler. Common variables are `CXX`,`CC` and `FC` , respectively for the `C++`,`C` and `Fortran` languages.
On a Cray machine one may want to type in

```bash
export CXX=CC
export CC=cc
export FC=ftn
```

before running cmake.

Alternatively, the compilers can be specified as CMake variables

```bash
 cmake ${CMAKE_PACKAGE_DIRECTORY} -DCMAKE_Fortran_COMPILER=ftn -DCMAKE_C_COMPILER=cc -DCMAKE_CXX_COMPILER=CXX
```
