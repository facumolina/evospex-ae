## Download

1. Download the artifact from [DOI](http://doi.org/10.5281/zenodo.4458256)

2. Uncompress the downloaded file: ```tar -xvf evospex-all.tar.gz```, which will create the following files:
```
  evospex-all/evospex.tar.gz
  evospex-all/sf110-evospex.tgz
  evospex-all/object-generation.tgz
  Dockerfile
```

## Installation with Docker

1. Get [Docker](https://www.docker.com/)
2. Build and run the docker image:
```
  cd evospex-all
  docker build -t evospex .
  docker run -it evospex
```

**NOTE**: the build process will perform all the steps described below in the manual installation. The final image size may be 13GB. 

## Manual installation

Uncompress the file evospex-all/evospex.tar.gz and just set the environment variable EVOSPEX to the uncompressed directory:
```
  cd evospex-all
  tar -xvf evospex.tar.gz
  cd evospex
  export EVOSPEX=$(pwd)
```

EvoSpex is provided as a jar bundle containing all the required dependencies. Having the tools mentioned in [REQUIREMENTS.md](REQUIREMENTS.md) installed, is enough to run EvoSpex. 

Run the tool using the paper's motivating example, to verify that everything is working correctly:

`./evospex.sh AvlTreeList src/test/resources/objects/AvlTreeList/add\\\(int\,java.lang.Object\\\)/3/`

**Steps for the Experiments**

To reproduce the experiments in the paper, the following additional steps are required. 

1. Uncompress the selected subjects from the [SF110-benchmark](https://www.evosuite.org/experimental-data/sf110/):
```
  cd evospex-all
  tar -xvf sf110-evospex.tar.gz
```

2. Set the environment variable SF110SRC to the uncompressed directory:
```
  cd sf110-evospex
  export SF110SRC=$(pwd)
```

3. Compile the project that you would like to analyze (this step must be performed on each project). For instance, to compile project 2_a4j, do as follows: 
```
  cd $SF110SRC/2_a4j
  ant compile
```

5. Install Daikon, following the installation instructions from its official [website](https://plse.cs.washington.edu/daikon/download/doc/daikon.html#Installation)

6. Compile OASIs (the tool used for oracle assessment):
```
  cd $EVOSPEX/experiments/oasis
  javac -cp "lib/*" src/* -d bin/
```

7. Install the Pandas Python libarary:
```
  pip3 install pandas
```

**Steps for test generation Experiments**


1. Uncompress the test generation tool
```
  cd evospex-all
  tar -xzvf object-generation.tgz
```

2. Set the environment variable EVOSPEXOG to the uncompressed directory:
```
  cd object-generation
  export EVOSPEXOG=$(pwd)
```
 
You can now continue with the steps described in [README.md](README.md) to reproduce the experiments.
