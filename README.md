# Doc2SMT

Doc2SMT generating strong functional constraints for library methods based on their documentations. 

It employs a set of general rules to translate descriptions of method functionalities into a large number of candidate OCL expressions. 

A novel two-step validation is then introduced to find out the constraints that comply with the behaviours of the method: 
- In static validation, a domain model that can be manually enhanced incrementally is used to filter out OCL expressions that do not "fit" the problem domain
- Dynamic validation checks whether a candidate constraint rightly abstracts the method under consideration through testing

# How to use it

This repository contains an executable jar file of Doc2SMT under the *tool* folder. To see how Doc2SMT works you need to check out the following steps:

## Java version

Make sure your Java version is [Java 8](https://docs.oracle.com/javase/8).

## Z3 version

Doc2SMT employs [Z3 prover](https://github.com/Z3Prover/z3) to check candidate constraints during dynamic validation. In order to run it correctly you need to make sure [Z3-4.8.4](https://github.com/Z3Prover/z3/releases/tag/z3-4.8.4) be built on your machine. For Windows users, you also need to add ```$Z3_HOME/bin``` to the environment variables.

## Download Doc2smt release version

Download [a release version](https://github.com/doc2smt/doc2smt/releases/download/v1.0/doc2smt-tool.tar.gz) of Doc2smt on the release page and extract it.

## Get started

Run ```java -Xmx8g -jar doc2smt.jar``` command under the _tool_ folder and you can see this instruction:

```
Input a target class from the following classes: 
(input "all" to operate on all classes, input "sample" to operate sample API)
[Collection, AbstractCollection, Set, AbstractSet, HashSet, SortedSet, NavigableSet, TreeSet, List, AbstractList, AbstractSequentialList, ArrayList, LinkedList, Map, AbstractMap, HashMap, SortedMap, NavigableMap, TreeMap]

```

You can also input "q" or "quit" to exit the program.

# Input and Output

The input files are:
- __container_doc.txt__ contains the JavaDoc text of our subject Collections classes
- __containermodel.ecore__ contains the enhanced domain model
- __ocl2smt.json__ contains the handcrafted constraints of meta-operations

The output files are:
- __container.ocl__ contains the generated OCL expressions of all APIs of subject classes
- ___CLASS_-smt.txt__ contains the generated SMT constraints of all APIs of the corresponding class
