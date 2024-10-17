This is a Dockerfile that will help you create a Docker image containing an installed version of the [COIN-OR
Optimization Suite](https://github.com/coin-or/COIN-OR-OptimizationSuite).

This Dockerfile is based on Python:3.10 image and has latest versions of gcc, gfortran (version 12.2.0)
NOTE that these versions are post the "cxx14" era and so by default some old features will not be supported.
Use the CXXFLAGS to enable cxx14 support to compile old programs (like I did in the Dockerfile)
Similarly for Fortran flags (See the Dockerfile)

This image can serve as a great base image for python programmers interested in developing optimization programs.
For e.g. Python programs that use Pyomo library (or) any other optimization library that can benefit from the solvers built into this image.

Cheers!

# Building from sources (2 hrs mininum)

I have not published the image on docker-hub. So you will need to clone the Github repo and build it.
Building this can take 2 hours or more depending on your setup.

Install "Docker desktop" on your machine

```
git clone https://github.com/skannan-maf/optimization-suite-docker
cd optimization-suite-docker
sudo docker build -t coin-or:latest image/
docker create --name=coin-or -it coin-or:latest
docker start coin-or
```

Now copy in any files you need:

```
docker cp example.mps coin-or:/tmp
```

Here, we are copying into the `/tmp` directory inside the container. Finally,
execute a solver command.

```
docker exec coin-or /usr/bin/cbc /tmp/example.mps > /tmp/output
```

and finally, copy the output back out

```
docker cp coin-or:/tmp/output .
```

Note that you are as root by default inside the container, but this is not
much of a risk inside a docker container, since it can be recreated easily.

