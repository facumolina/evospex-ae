## Download

1. Download the artifact from [here](https://mega.nz/file/JW4TFK6Q#V2S3UiSIqy-bzHpcDFAab76TXIygtvipMDHMEzrF_cQ).

2. Uncompress the downloaded file: ```tar -xvf evospex.tar.gz```

3. Set the environment variable EVOSPEX to the uncompressed directory:
```
  cd evospex
  export EVOSPEX=$(pwd)
```

## Installation

No installation step is required. EvoSpex is provided as a jar bundle containing all the required dependencies. Having the tools mentioned in [REQUIREMENTS.md](REQUIREMENTS.md) installed, is enough to run EvoSpex. 

Run the tool using the paper's motivating example, to verify that everything is working correctly:

`./evospex.sh AvlTreeList src/test/resources/objects/AvlTreeList/add\\\(int\,java.lang.Object\\\)/3/`

## Experiments

To reproduce the experiments in the paper, the following additional steps are required. 

1. Download the selected subjects from the [SF110-benchmark](https://www.evosuite.org/experimental-data/sf110/) from [here](https://mega.nz/file/TkJziSKI#y7c_8cJaTnfhW8NBlO_hbWKiWMqqrBD4iIivnII5ycM). 
2. Uncompress the downloaded file: ```tar -xvf sf110-evospex.tar.gz```
3. Set the environment variable SF110SRC to the uncompressed directory:
```
  cd sf110-evospex
  export SF110SRC=$(pwd)
```
4. Compile the project that you would like to analyze (this step must be performed on each project). For instance, to compile project 2_a4j, do as follows: 
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
 
You can now continue with the steps described in [README.md] to reproduce the experiments.
