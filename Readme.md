# CMake webinar

This repository contains the source material for a Archer2 EPCC webinar on CMake.

## Build instructions

You will need to install mkdocs-material. This can be installed as a python package

```bash
pip install mkdocs-material
```

The documentation can be built on the fly by running.

```bash
mkdocs serve
```

This will start a local server on localhost and display the address at which the documentation is served. By default this will be on localhost. Copy the address and paste it in the address bar of your favorite browser in order to browse the lessons.

## Outline of live-coding

- Go trough the images in the Introduction pages. Present cmake as a build generator tool, and higher level of abstraction for compiling
- Go to the Hello World example and demonstrate the configure/build/install process 
- Go to WindTunnel example and try to compile. Show how to see the list of variables and what they mean
- Try to recompile `windtunnel` using the intel compilers and intel mpi.
- Try to recompile using the unwrapped MPI wrapper compiler and an external implementation of openmpi. Goal is to teach usage of `-DPACKAGE_NAME_ROOT`
- Go to MPI hello world example. Goal is to give the concept of a target and target properties
- Show the need for policies by trying to use -DMPI_ROOT

## Using in Docker

You should serve the container on url 0.0.0.0 ( instead of localhost )

```bash
mkdocs serve -a 0.0.0.0:8887  
````
