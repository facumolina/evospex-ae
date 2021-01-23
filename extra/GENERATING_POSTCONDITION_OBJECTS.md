## Generation of object instances for learning postconditions

As described in [README.MD](README.md), EvoSpex recieves as input sets of valid and invalid pre/post state pairs (i.e., state pairs that represent, and do not represent, the method’s current behavior, respectively). Valid pre/post state pairs are obtained by generating executions of the method under analysis, while invalid ones are obtained by mutating the valid pairs. Here we describe how to reproduce the generation of pre/post state pairs.

## Download and install

1. Follow the steps in [INSTALL.MD](INSTALL.md) to install EvoSpex and SF110 (don't forget to set environment variables EVOSPEX and SF110SRC!).

2. Download the artifact from [here](https://mega.nz/file/z4Bx3CqI#JFuPyHmZadCHlyYN-c_F7mYN74JvhTZ3etKbyDKzL_8).

3. Uncompress the artifact
```
  tar -xzvf object-generation.tgz

```

4. Set the environment variable EVOSPEXOG to the uncompressed directory:
```
  cd object-generation
  export EVOSPEXOG=$(pwd)
```

## Generation of objects for the SF110 case studies

Here we are going to generate sets of pre/post state pairs for the *Artists* class of SF110's *2_a4j* (for this class we considered methods *getArtist* and *getArtistArray*). For this, we run 

```
./generate-objects/generate_objects_sf110_class.sh 2_a4j Artists
```

The generated objects are stored in:

```
$EVOSPEX/src/test/resources/sf110/<project>/<method>/<scope>/objects
```

For the above run, the objects' path is (notice that we use a scope of 2 in SF110 experiments):

```
# ls $EVOSPEX/src/test/resources/sf110/2_a4j/Artists/getArtist/2/objects

in0.xml  mut0.xml  mut1.xml  mutations0.txt  out0.xml  out1.xml
```

Method *getArtist* has one input object (the state of the receiver before executing the method), and two output objects, the receiver (after executing the method) and the return value (of String[] type). The generated inputs for the method (receivers) are stored in file *in0.xml*, and the generated outputs in files *out0.xml* (possibly updated receiver), *out1.xml* (return value). Position *i* of each file contains a single valid input/output tuple *(i0,o0,o1)* for *getArtist*. (All files have the same length). *mut0.xml* and *mut1.xml* correspond to mutations performed either to the receiver (an object in *out0.xml*) or the return value (an object in *out1.xml*). Thus, position *i* of *in0.xml*, *mut0.xml* and *mut1.xml* contains an tuple *(i0,m0,m1)* that corresponds to an invalid execution escenario for *getArtist* (i.e. with one mutated object).

Finally, the tests produced (following a bounded exhaustive approach) to generate the execution scenarios for *getArtist* described above can be found in:

```
$EVOSPEX/src/test/resources/sf110/2_a4j/Artists/getArtist/2/tests
```

As our tool is a customized Randoop version (modified to perform bounded exhuastive generation), tests are generated for the JUnit testing framework:

```
# ls $EVOSPEX/src/test/resources/sf110/2_a4j/Artists/getArtist/2/tests/net/kencochrane/a4j/beans/RegressionTest*

$EVOSPEX/src/test/resources/sf110/2_a4j/Artists/getArtist/2/tests/net/kencochrane/a4j/beans/RegressionTest0.java
$EVOSPEX/evospex/src/test/resources/sf110/2_a4j/Artists/getArtist/2/tests/net/kencochrane/a4j/beans/RegressionTestDriver.java
```

**NOTE**: File *object-generation/README-sf110.txt* contains a description of the available projects and classes for this experiment.

## Generation of objects for contract reproduction case studies

In this section, we deal with the generation of objects for learning invariants for classes with existing, manually written contracts. As an example, we are going to generate sets of pre/post state pairs for Eiffel's *DoublyLinkedListNode* class. The generation will be performed for scope 3 (at most 3 nodes in the lists). To achieve this, run the following command:

```
cd object-generation
./generate-objects-datastr/generate_objects.sh casestudies.eiffel.DoublyLinkedListNode 3
```

The methods under analysis for this class are:

```
insert_right\(casestudies.eiffel.DoublyLinkedListNode\)
remove\(\)
```

Resulting objects will be stored (in a similar format to that explained above for SF110 experiments) in folder:

```
$EVOSPEX/src/test/resources/objects/<case study>/<method>/<scope>
```

For *insert_right*, objects are saved in:

```
$EVOSPEX/src/test/resources/objects//DoublyLinkedListNode/insert_right\(casestudies.eiffel.DoublyLinkedListNode\)/3/
```

JUnit tests generated to produce the execution scenarios for *insert_right* are saved in:

```
$EVOSPEX/src/test/java
```

The path for *insert_right* tests is:

```
# ls $EVOSPEX/src/test/java/casestudies/eiffel/DoublyLinkedListNodeinsert_right3S*

$EVOSPEX/src/test/java/casestudies/eiffel/DoublyLinkedListNodeinsert_right3Suite.java
$EVOSPEX/src/test/java/casestudies/eiffel/DoublyLinkedListNodeinsert_right3Suite0.java
```

**NOTE**: File *object-generation/README-datastr.txt* contains a description of the available case studies for this experiment.
