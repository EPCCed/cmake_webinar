# Cmake webinar

## Cmake Arguments

- Introduction: what it is and why we use it ?
  - generation of build files ( Makefile for Unix systems)
  - Supports all OS , competitor of GNU autotools
- build process
  - ( cd build; cmake ..;make; make install )
  - make VERBOSE=1
- typical project  structure description
  - CMakeLists.txt
  - project requirement
  - Subdirectories 
  - Languages
- Cached variables. How to define variables, ccmake .. to get a list of cached variables.
- Common configurations: Setting up compilers, CMAKE_BUILD_TYPE, CMAKE_INSTALL_PREFIX, CMAKE_PREFIX_PATH
- findXXX ( findMPI)

- Debugging
  - Output inspection
  - --trace-expand, --trace, --fresh
  - Gotchas
    - findXXX does not find anything ( Blas, MPI , etc... )
    - findXXX finds the wrong library
    - old policy warnings
- CTests ( ??? )



### Presentation 
First we give an high level overview of what CMake is and what it can be used for.

- Go trough the images in the Introduction pages. Present cmake as a build generator tool, and higher level of abstraction for compiling
- Go to the Hello World example and demonstrate the configure/build/install process 
- Go to WindTunnel example and try to compile. Show how to see the list of variables and what they mean
- Try to recompile `windtunnel` using the intel compilers and intel mpi
- Try to recompile using the unwrapped MPI wrapper compiler and an external implementation of openmpi. Goal is to teach usage of -DPACKAGE_NAME_ROOT=

- Go to MPI hello world example. Goal is to give the concept of a target and target properties
- Show the need for policies by trying to use -DMPI_ROOT