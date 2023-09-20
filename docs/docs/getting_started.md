# Getting started

In order to build a cmake package you first need to install cmake.

## Getting CMake

You can install CMake from several package managers. For instance, on Ubuntu, you can install it with

```bash
sudo apt install cmake
```

On computing clusters CMake is usually already centrally installed. On the Archer2 machine, you can load the centrally installed  module.

```bash
module load cmake
```

## Compiling a CMake package

Compiling a CMake package requires three steps

- A Configuration step
- A Build step
- An install step

### Configuration

First you need to create a build directory. 
The build directory will be populated with temporary build files, such as object files and internal cmake configuration files.
You then need to change the current directory to the build directory.

```bash
mkdir build 
cd build
```

You also need to tell CMake to look for compilers, check for dependencies and find where libraries are stored on your system. Let us assume you wish to compile the source code in  `$CMAKE_PACKAGE_DIRECTORY`. Moreover, let us assume you wish the resulting binaries to be installed in the `$INSTALL_DIR_PACKAGE`.
From the build directory type

```bash
cmake $CMAKE_PACKAGE_DIRECTORY -DCMAKE_INSTALL_PREFIX=$INSTALL_DIR_PACKAGE .
```

This will generate a build system in the build directory. On UNIX based systems, the default build system is `Makefile`.

### Build

Upon successful completion of the configuration step cmake will output a `Makefile` in your build directory.
In order to compile the package you can type

```bash
make
```

If you whish to see some more verbose output, including the compilation commands being executed type

```bash
make VERBOSE=1
```

After a successful build, the binary files will be saved somewhere in the build directory.

### Install

Once all the executable and libraries have been generated, these need to be copied to the installation directory you specified during the configuration phase. You can copy the binaries in your specified install directory by typing

```bash
make install
```

### Tests

CMake contains a mechanism to run tests. This can be useful to test that the package was successfully  installed. If tests have been defined by the CMake package developers, from the build directory you can type

```bash
ctest 
```

This command will run all the tests. If a test fails it will print out an error message.

!!! Exercise
    Try to build the hello world CMake package contained in `demos/hello_world_cmake`.