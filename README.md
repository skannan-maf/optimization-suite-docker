This is a Docker image containing an installed version of the [COIN-OR
Optimization Suite](https://github.com/coin-or/COIN-OR-OptimizationSuite).

# Install and Use From Docker Hub

This image is now on [Docker
Hub](https://hub.docker.com/r/tkralphs/coinor-optimization-suite/). To use,
simply install Docker (see instructions below) and then do

```
docker pull <To Be Done>
```

This retrieves a docker image containing the COIN-OR Optimization Suite. Once
you have the image, you can create a container, which is a running version of
the image. Note that this container is completely isolated from the OS you are
working in, so to run any useful commands inside it, you need to first copy
the files in to the container, then copy the results back out. To do this,
first create and start a container, as follows:

```
docker create --name=coin-or -it <To-Be-Done>
docker start coin-or
```

Now copy in any files you need:

```
docker cp example.mps coin-or:/tmp
```

Here, we are copying into the `/tmp` directory inside the container. Finally,
execute a solver command.

```
docker /var/coin-or/bin/cbc /tmp/example.mps > /tmp/output
```

and finally, copy the output back out

```
docker cp coin-or:/tmp/output .
```

Note that you are as root by default inside the container, but this is not
much of a risk inside a docker container, since it can be recreated easily.

# Build from Source

## Linux

Just clone the repository and build the docker image by

```
git clone https://github.com/skannan-maf/optimization-suite-docker
cd optimization-suite-docker
sudo docker build -t coin-or image/
```

Now follow the instructions for running a solver from above, but note that all
commands will have to be executed with `sudo`.

## Windows

First install Docker Desktop for Windows (in older versions of Windows without
built-in virtualization, the instructions may be different). From a Powershell
terminal, clone the repository and build the docker image by the commands

```
git clone https://github.com/skannan-maf/optimization-suite-docker
cd optimization-suite-docker
docker build -t coin-or image/
```

Finally, follow the instructions for running a solver from above.

## Mac OSX

Install "Docker desktop"

```
git clone https://github.com/skannan-maf/optimization-suite-docker
cd optimization-suite-docker/
docker build -t optimization-suite image/
```

Now follow the instructions for running a solver from above.
