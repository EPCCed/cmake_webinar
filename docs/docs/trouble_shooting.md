# Trouble shooting

## Finding MPI

Most implementations of MPI come with a compiler wrapper. It is a good practice to provide the CMake compiler wrapper to CMake. CMake will often figure out that the compiler provided is a MPI wrapper , set the `MPI_FOUND` variable to true and understand that no additional options or flags are required when building the project.

## Using find_package

The command `find_package` can be used to find any package or library the project depends on.
The command `find_package` will look for the package in a [pre-defined set of directories](https://cmake.org/cmake/help/latest/command/find_package.html?highlight=find_package#search-procedure) and will return the first one it finds. If CMake cannot find the package and you marked the package as required, it will throw a fatal error. If CMake can find a package, it will import new targets which you can later used in your project.
You can find a list of packages supported by CMake developers on the main documentation.
You can obtain a list of supported packages by using the `--help-module-list` and filtering for entries that start with "Find"

```bash
cmake --help-module-list | grep "Find"
```

If CMake cannot find a package or if it finds the wrong version, you can specify the location of the package by setting the variable `<PACKAGE_NAME>_ROOT`. CMake will then look for the package in that folder

!!! Warning
    Be aware that that behaviour of `find_package` has changed over the years and older versions of CMake use different rules to find packages. For instance older version of CMake will ignore the `<PACKAGE_NAME>_ROOT` variable. Some versions will ignore it but print a policy *warning*.


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


This appears when a default behaviour changes between different cmake versions. Whenever a behavioural change is introduced in CMake the old default will be kept for a few versions and the above deprecation warning printed on the screen. Packages developer can set the new behaviour by setting the corresponding policy to new. Reading the warning and the policy definition might help to asses whether the deprecation will affect your build .

## Tracing

When debugging a CMake installation, you may find useful to print to the screen the commands which are executed by CMake. This is possible by adding to the cmake command the flag `--trace-source=${CMAKE_FILE}`, where `${FILE}` is the name of the file containing the CMake code. For instance to debug CMake code contained in the `CMakeLists.txt` file you can use

```bash
cmake --trace-source=CMakeLists.txt 
```

By adding the flag `--trace-expand` each variable will be substituted with its current value.
