## Collecting the postconditions inferred by the tools

In order to analyze the quality of the postconditions produced by the techniques, the inferred assertions needs to be collected and manually placed in the corresponding Java files that will later be the input for OASIs. For instance, a class analyzed for project *2_a4j* is *net.kencochrane.a4j.beans.FullProduct*, and the classes of interest of such a case can be listed by doing `ls $SF110SRC/2_a4j/src/main/java/net/kencochrane/a4j/beans/FullProduct*`:
```
src/main/java/net/kencochrane/a4j/beans/FullProduct.java
src/main/java/net/kencochrane/a4j/beans/FullProductDaikon.java
src/main/java/net/kencochrane/a4j/beans/FullProductEvoSpex.java
```

The class FullProduct is the one from which the postconditions were computed. And the two extra classes FullProductEvoSpex and FullProductDaikon are a copy of the original one, but containing the assertions learned by the corresponding tools.

### Collecting postconditions inferred by EvoSpex

### Collecting postconditions inferred by Daikon


