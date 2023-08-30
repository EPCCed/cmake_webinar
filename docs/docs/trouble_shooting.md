# Trouble shooting

## Cmake policy warning
Sometimes the output in CMake reports a message
!!! error
    CMake Warning (dev) at CMakeLists.txt:6 (find_package):
    Policy CMP0074 is not set: find_package uses <PackageName>_ROOT variables.
    Run "cmake --help-policy CMP0074" for policy details.  Use the cmake_policy
    command to set the policy and suppress this warning.

    Environment variable MPI_ROOT is set to:

    /mnt/lustre/indy2lfs/sw/intel/compilers_and_libraries_2020.4.304/linux/mpi/intel64

    For compatibility, CMake is ignoring the variable.
    This warning is for project developers.  Use -Wno-dev to suppress it.


This appears when a default behaviour changes between different cmake versions. Whenever a behavioural change is introduced in CMake the old default will be kept for a few versions and the above deprecation warning printed on the screen. The new behaviour can be enabled by the package developer by setting the corresponding policy to new.
Seeing this warning might suggest you are using an outdated version of cmake. Reading the warning and the policy definition might help to see if the deprecation will affect your build or not.


## Using find_package

The command `find_package` can be used to find any package the project depends on.
CMake will look for a  `Find<Packagename>.cmake` file. The module can be either provided by CMake developers or defined by a package developers. 
You can optionally specify if the package is optional or if it is required for a successful build. 
The command `find_package` will look for the package in a [pre-defined set of directories](https://cmake.org/cmake/help/latest/command/find_package.html?highlight=find_package#search-procedure) and will return the first one it finds. If no package is found and the package is marked as required a fatal error will be thrown.
If a package is found it will import targets which can be included in the project.
For packages supported by CMake developers, the list of imported targets can be found on the main documentation.
A list of supported `Find` modules can be obtained with

```bash
cmake --help-module-list | grep "Find"
```

If a package is not found or the wrong version is found you can specify the folder where to look by defining the variable `<PACKAGE_NAME>_ROOT`. If defined `cmake` will try to find the package in that folder.

!!! Warning
    Be aware that that behaviour of `find_package` has changed over the years and older versions of CMake use different rules to find packages. For instance older version of CMake will ignore the `<PACKAGE_NAME>_ROOT` variable. Some versions will ignore it but print a policy *warning*.
## Finding MPI

Most implementations of MPI come with a compiler wrapper. It is a good practice of providing to CMake the compiler wrapper. CMake will often figure out that the compiler provided is a MPI wrapper , set the `MPI_FOUND` variable to true and understand that no additional options or flags are required in order to use MPI.

## Tracing

When debugging a CMake installation it is possible to have CMake print out each command it executes.

```bash 
cmake --trace-source=CMakeLists.txt 
```

By adding the flag `--trace-expand` each variable will be substituted with its current value.
