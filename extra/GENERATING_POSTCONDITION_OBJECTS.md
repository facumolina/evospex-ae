## Generation of object instances for learning postconditions

As described in [README.MD](README.md), EvoSpex recieves as input sets of valid and invalid pre/post state pairs (i.e., state pairs that represent, and do not represent, the method’s current behavior, respectively). Valid pre/post state pairs are obtained by generating executions of the method under analysis, while invalid ones are obtained by mutating the valid pairs. Here we describe how to reproduce the generation of pre/post state pairs.

## Download and install

1. Follow the steps in [INSTALL.MD](INSTALL.md) to install EvoSpex and SF110 (don't forget to set environment variables EVOSPEX and SF110SRC!).

2. Download the artifact from [here](REPLACE WITH MEGA LINK).

3. Set the environment variable EVOSPEXTG to the uncompressed directory:
```
  cd test-generation 
  export EVOSPEXTG=$(pwd)
```

## Generation of objects by means of bounded exhaustive test generation

Here we are going to generate sets of pre/post state pairs for the *Artists* class of SF110's *2_a4j* (for this class we considered methods *getArtist* and *getArtistArray*). For this, we run 

```
./generate-objects/generate_objects_sf110_class.sh 2_a4j Artists
```

The generated objects are stored in:

```
$EVOSPEX/src/test/resources/sf110/<project>/<method>/<scope>/objects
```

For the above run, this is instanced to (notice that we use a scope of 2 in SF110 experiments):

```
# ls $EVOSPEX/src/test/resources/sf110/2_a4j/Artists/getArtist/2/objects

in0.xml  mut0.xml  mut1.xml  mutations0.txt  out0.xml  out1.xml
```

*getArtist* has one input object (the state of the receiver before executing the method), and two output objects, the receiver (after executing the method) and the return value (of Artist type). The generated inputs are stored in file in0.xml, and the generated outputs in files out0.xml (receiver), out1.xml (return value). Position *i* of each file (all have the same length) contains a single valid input/output tuple *(i0,o0,o1)* for *getArtist*. mut0.xml and mut1.xml correspond to mutations performed either to the receiver (an object in out0.xml) or the return value (an object in out1.xml). Thus, position *i* of in0.xml, mut0.xml and mut1.xml contains an tuple *(i0,m0,m1)* that corresponds to an invalid execution escenario for *getArtist) (i.e. with one mutated object).

Finally, the tests produced (bounded exhaustively) to generate the above tuples can be found in:

```
$EVOSPEX/src/test/resources/sf110/2_a4j/Artists/getArtist/2/tests
```


```
# ls $EVOSPEX//src/test/resources/sf110/2_a4j/Artists/getArtist/2/tests/net/kencochrane/a4j/beans/RegressionTest*

$EVOSPEX/src/test/resources/sf110/2_a4j/Artists/getArtist/2/tests/net/kencochrane/a4j/beans/RegressionTest0.java
$EVOSPEX/evospex/src/test/resources/sf110/2_a4j/Artists/getArtist/2/tests/net/kencochrane/a4j/beans/RegressionTestDriver.java
```


**NOTE**: the instructions in this section assumes that the project being analyzed is *2_a4j*. The classes and methods to analyze for project *2_a4j* are listed in file *$EVOSPEX/src/test/resources/sf110/2_a4j/target-classes.txt*. To analyze other projects, just use any of the names listed when doing `ls $EVOSPEX/src/test/resources/sf110`. Again, the classes and methods to analyze for a particular project are listed in the file *target-classes.txt* of the corresponding folder. 
