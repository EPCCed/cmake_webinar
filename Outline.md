# Cmake webinar


### Presentation 
First we give an high level overview of what CMake is and what it can be used for.

- Go trough the images in the Introduction pages. Present cmake as a build generator tool, and higher level of abstraction for compiling
- Go to the Hello World example and demonstrate the configure/build/install process
- Go to WindTunnel example and try to compile. Show how to see the list of variables and what they mean
- Try to recompile `windtunnel` using the intel compilers and intel mpi.
- Try to recompile using the unwrapped MPI wrapper compiler and an external implementation of openmpi. Goal is to teach usage of -DPACKAGE_NAME_ROOT=

- Go to MPI hello world example. Goal is to give the concept of a target and target properties
- Show the need for policies by trying to use -DMPI_ROOT