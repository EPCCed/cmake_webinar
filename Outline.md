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

## Resources

- <https://cliutils.gitlab.io/modern-cmake/>
- <https://cmake.org/cmake/help/latest/>
- <https://coderefinery.github.io/cmake-workshop/testing/>
- <https://enccs.github.io/cmake-workshop/cmake-syntax/>