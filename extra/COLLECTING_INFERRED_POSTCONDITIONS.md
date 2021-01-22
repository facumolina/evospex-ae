## Collecting the postconditions inferred by the tools

In order to analyze the quality of the postconditions produced by the techniques, the inferred assertions needs to be collected and manually placed in the corresponding Java files that will later be the input for OASIs. For instance, a class analyzed for project *2_a4j* is *net.kencochrane.a4j.beans.FullProduct*, and the classes of interest of such a case can be listed by doing `ls $SF110SRC/2_a4j/src/main/java/net/kencochrane/a4j/beans/FullProduct*`:
```
src/main/java/net/kencochrane/a4j/beans/FullProduct.java
src/main/java/net/kencochrane/a4j/beans/FullProductDaikon.java
src/main/java/net/kencochrane/a4j/beans/FullProductEvoSpex.java
```

The class FullProduct is the one from which the postconditions were computed. And the two extra classes FullProductEvoSpex and FullProductDaikon are a copy of the original one, but containing the assertions learned by the corresponding tools.

### Postconditions inferred by EvoSpex

Assuming that the command `./experiments/sf110/run-evospex-project.sh 2_a4j 10` has been successfully executed, to collect the postconditions the user should move to the folder containing the results:
```
cd $EVOSPEX/experiments/sf110/2_a4j/evospex-results
```
The directory will contain one folder for each analyzed class, being the folder of interest the one with name *FullProduct*. Such folder will contain 11 files for each method, 10 txt files containing the logs of each single execution and 1 csv file containing the summary of the 10 executions. To determine what is the most common postcondition inferred by the algorithm through the 10 executions for a method, let's say *addAccesory*, perform the next steps:
```
cd $EVOSPEX/experiments/
python3.7 process-csv.py sf110/2_a4j/evospex-results/FullProduct/addAccesory.csv
```

The python script will list the executions containing the *Best* postconditions (w.r.t the fitness function) and then the executions containing the most Common postcondition (the one that was inferred ). Here, just look at the list of the most common postcondition, take any of the execution numbers (column exec_number) on that list, and open the txt containing the logs of such execution. For instance, if the exex_number is 2, open the file *sf110/2_a4j/evospex-results/FullProduct/addAccesory-2.txt*. At the end will be the postcondition that needs to be collected:
```
Assertions:  
  assert(
    this.details != null &&
    old_this.similarItems == this.similarItems &&
    ExpressionEvaluator.evaluateSetMembership(arg0,"this . accessories",this)
  );
```

Once identified, just copy the postcondition assertion as the final statement of method *addAccessory* in class *$SF110SRC/2_a4j/src/main/java/net/kencochrane/a4j/beans/FullProductEvoSpex.java*. And then, compile the project again: 
```
cd $SF110SRC/2_a4j/
ant compile
```

Finally, perform the mentioned steps for every method and the class *FullProduct* will be ready for quality analysis with the technique EvoSpex. 

### Postconditions inferred by Daikon

