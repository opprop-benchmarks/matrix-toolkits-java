[![Build Status](https://travis-ci.org/fommil/matrix-toolkits-java.svg?branch=master)](https://travis-ci.org/fommil/matrix-toolkits-java)
[![Coverage Status](https://coveralls.io/repos/fommil/matrix-toolkits-java/badge.svg?branch=master)](https://coveralls.io/r/fommil/matrix-toolkits-java?branch=master)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.googlecode.matrix-toolkits-java/mtj/badge.svg)](https://maven-badges.herokuapp.com/maven-central/com.googlecode.matrix-toolkits-java/mtj)
[![Javadoc](https://javadoc-emblem.rhcloud.com/doc/com.googlecode.matrix-toolkits-java/mtj/badge.svg)](http://www.javadoc.io/doc/com.googlecode.matrix-toolkits-java/mtj)

matrix-toolkits-java 
====================

**MTJ** is a high-performance library for developing linear algebra applications.

MTJ is based on [BLAS](http://www.netlib.org/blas) and [LAPACK](http://www.netlib.org/lapack) for its dense and structured sparse computations, and on the [Templates](http://www.netlib.org/templates) project for unstructured sparse operations.

MTJ uses the [`netlib-java`](https://github.com/fommil/netlib-java/) project as a backend,
which will automatically use machine-optimised natives, if they are available. Please read the [`netlib-java` documentation](https://github.com/fommil/netlib-java/) for the extra steps needed to ensure that you are getting the best performance for your system.

For more details on high performance linear algebra on the JVM, please watch [my talk at Scala eXchange 2014](https://skillsmatter.com/skillscasts/5849-high-performance-linear-algebra-in-scala) ([follow along with high-res slides](http://fommil.github.io/scalax14/#/)).


Performance to Other Libraries
==============================

The [java-matrix-benchmark](https://github.com/fommil/matrix-toolkits-java/issues/33) clearly shows MTJ to be the most performant Java library for large matrices:

![Relative Performance](http://i752.photobucket.com/albums/xx162/fommil/summary_stacked_area_zps13e5b28c.png)

[A more complete breakdown is available](http://code.google.com/p/java-matrix-benchmark/wiki/RuntimeCorei7v2600_2013_10): MTJ with system optimised natives wins almost every benchmark.

We recommend [common-math](http://commons.apache.org/proper/commons-math/) for small matrix requirements as it provides a large variety of mathematics features, and [EJML](http://code.google.com/p/efficient-java-matrix-library/) if performance on small matrices is more important than features.

Sparse Storage
==============

A variety of sparse matrix / vector storage classes are available:

* [`CompColMatrix`](src/main/java/no/uib/cipr/matrix/sparse/CompColMatrix.java)
* [`CompDiagMatrix`](src/main/java/no/uib/cipr/matrix/sparse/CompDiagMatrix.java)
* [`CompRowMatrix`](src/main/java/no/uib/cipr/matrix/sparse/CompRowMatrix.java)
* [`FlexCompColMatrix`](src/main/java/no/uib/cipr/matrix/sparse/FlexCompColMatrix.java)
* [`FlexCompRowMatrix`](src/main/java/no/uib/cipr/matrix/sparse/FlexCompRowMatrix.java)
* [`UnitLowerCompRowMatrix`](src/main/java/no/uib/cipr/matrix/sparse/UnitLowerCompRowMatrix.java)
* [`UpperCompRowMatrix`](src/main/java/no/uib/cipr/matrix/sparse/UpperCompRowMatrix.java)
* [`SparseVector`](src/main/java/no/uib/cipr/matrix/sparse/SparseVector.java)
* [`LinkedSparseMatrix`](src/main/java/no/uib/cipr/matrix/sparse/LinkedSparseMatrix.java)

The `LinkedSparseMatrix` storage type is a novel storage type developed under this project. It maintains two tail links, one for the next matrix element by row order and another by column order. Lookups are kept into each row and column, making multiplication and transpose multiplication very fast.

The following charts compare the `LinkedSparseMatrix` against `DenseMatrix` for increasing matrix size (`n x n`) and number of non-zero elements, `m`. Rainbow lines indicate  `m` varied from `10,000` to `100,000`. Solid lines are for dense matrix, dashed lines are the sparse matrix.

The following is time to initialise the matrix:

![init](http://i752.photobucket.com/albums/xx162/fommil/init_zpsca3b0937.png)

The following is the memory consumption:

![mem](http://i752.photobucket.com/albums/xx162/fommil/mem_zps3ad2fa94.png)

The following is the time to perform a multiplication with a dense matrix and output into a dense matrix:

![mult](http://i752.photobucket.com/albums/xx162/fommil/mult_zpscf2e6ba8.png)


Sparse Solvers
==============

MTJ provides [ARPACK](http://www.caam.rice.edu/software/ARPACK/) for very large symmetric matrices in [ArpackSym](src/main/java/no/uib/cipr/matrix/sparse/ArpackSym.java) (see the example usage in [ArpackSymTest](src/test/java/no/uib/cipr/matrix/sparse/ArpackSymTest.java)). ARPACK solves an arbitrary number of eigenvalues / eigenvectors.

In addition, implementations of the netlib Templates are available in the [`no.uib.cipr.matrix.sparse`](src/test/java/no/uib/cipr/matrix/sparse) package.

Users may wish to look at [Sparse Eigensolvers for Java](http://code.google.com/p/sparse-eigensolvers-java/) for another solver.


Legal
=====

* Copyright (C) 2003-2006 Bjørn-Ove Heimsund
* Copyright (C) 2006-2014 Samuel Halliday


History
=======

This project was originally written by Bjørn-Ove Heimsund, who has taken a step back due to other commitments.

Installation
============

Releases are distributed on Maven central:

```xml
<dependency>
    <groupId>com.googlecode.matrix-toolkits-java</groupId>
    <artifactId>mtj</artifactId>
    <version>1.0.2</version>
</dependency>
```

Unofficial single-jar builds may be available from [`java-matrix-benchmark`](https://code.google.com/p/java-matrix-benchmark/source/browse/#svn%2Ftrunk%2Flib%2Fmtj) for laggards who don't have [5 minutes to learn Maven](http://maven.apache.org/guides/getting-started/maven-in-five-minutes.html).

Snapshots may be distributed on Sonatype's Snapshot Repository (if you submit a pull request, a build will appear here when it is merged):

```xml
<dependency>
  <groupId>com.googlecode.matrix-toolkits-java</groupId>
  <artifactId>mtj</artifactId>
  <version>1.0.3-SNAPSHOT</version>
</dependency>
```

Contributing
============

Contributors are encouraged to fork this repository and issue pull
requests. Contributors implicitly agree to assign an unrestricted licence
to Sam Halliday, but retain the copyright of their code (this means
we both have the freedom to update the licence for those contributions).
