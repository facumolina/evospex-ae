## Download

Download the artifact from [here](https://mega.nz/file/JW4TFK6Q#V2S3UiSIqy-bzHpcDFAab76TXIygtvipMDHMEzrF_cQ).

## Installation

No installation step is required, our tool EvoSpex is already provided as a jar file with all the required dependencies. Having installed the tools mentioned in file [REQUIREMENTS.md](REQUIREMENTS.md) is enough to run it. 

Run the tool on the paper motivating example to verify that everything works as expected:

`./evospex.sh AvlTreeList src/test/resources/objects/AvlTreeList/add\\\(int\,java.lang.Object\\\)/3/`

## Experiments

To be able to perform the experiments, the following extra steps will be required. 

1. Download the subjects that we took from the [SF110-benchmark](https://www.evosuite.org/experimental-data/sf110/) from [here](https://mega.nz/file/TkJziSKI#y7c_8cJaTnfhW8NBlO_hbWKiWMqqrBD4iIivnII5ycM). 
2. Uncompress the dowloadad file: ```tar -xvf sf110-evospex.tar.gz```
3. Set the environment variable SF110SRC to the uncompressed directory:
```
  cd sf110-evospex
  export SF110SRC=$(pwd)
```
4. Compile the project that you will want to analyze. For instance, to compile project 2_a4j: 
```
  cd $SF110SRC/2_a4j
  ant compile
```

5. Install Daikon following the installation instructions from it's official [website](https://plse.cs.washington.edu/daikon/download/doc/daikon.html#Installation)


