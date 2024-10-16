FROM python:3.10
MAINTAINER Sarnath Kannan (skannan.maf@gmail.com)

RUN apt-get update
RUN apt-get -y install --no-install-recommends git subversion gcc g++ make wget gfortran patch pkg-config file
RUN apt-get -y install --no-install-recommends libgfortran-5-dev libblas-dev liblapack-dev libmetis-dev libnauty2-dev
RUN apt-get -y install --no-install-recommends ca-certificates
RUN apt-get install -y glpk-utils libglpk-dev libglpk40
# RUN apt-get update && apt-cache search libgfortran (Helped debug the version of libgfortran-dev to use)
# Run the command above if you encounter issues with version of libgfortran-?-dev below
RUN apt-get update && apt-get install -y libgfortran-12-dev
RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/coin-or/coinbrew /var/coin-or
WORKDIR /var/coin-or
RUN ./coinbrew fetch COIN-OR-OptimizationSuite@stable/1.9 --skip="ThirdParty/Blas ThirdParty/Lapack ThirdParty/Metis" --no-prompt
RUN ./coinbrew build  COIN-OR-OptimizationSuite --skip="ThirdParty/Blas ThirdParty/Lapack ThirdParty/Metis ThirdParty/Glpk" --no-prompt --prefix=/usr ADD_FCFLAGS=-fallow-argument-mismatch ADD_FFLAGS=-fallow-argument-mismatch
