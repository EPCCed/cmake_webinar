# Getting started
First thing one needs to have installed the CMake framework. 
## Getting CMake
On own machine this can be easily installed from a package manager.

- On Ubuntu you could use
```bash
sudo apt install cmake
```
- On computing clusters CMake is usually already installed. On Archer2 you need to load the centrally installed cmake module
```bash
module load cmake
```

## Compiling a CMake package
Compiling a CMake package requires three steps

- Configuration step
- Build step
- Install step

### Configuration

In the *configuration* step one first need to created a build directory. The build directory will be populated with themporary build files, such as object files and internal cmake configuration files.
Then change the current directory to the build directory.

```bash
mkdir build 
cd build
```

You then need to tell CMake to look for compilers, check for dependencies and find where libraries are stored on your systems. Let us assume the package you wish to compile is in  `$CMAKE_PACKAGE_DIRECTORY` and you wish to install the package in the `$INSTALL_DIR_PACKAGE`.
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

### Install
Once all the executable and libraries have been generated, these need to be copied to the installation directory you specified during the configuration phase.
```
make install
```
