

## The Project

A number of scientific applications comprise of loops wherein an array is subscripted by another array - a[b[i]]. With write references to the host array (array 'a') within a loop, current compile-time techniques are incapable of detecting such loops as parallelizable. If left unparallelized, these loops can in-turn prevent the performance obtained through automatic parallelization, matching that of the hand parallelized version. Hence, Subscripted subscript analysis is the next big challenge in Automatic Parallelization. 

Here is a short video describing the project and the current progress, published in proceedings of the International Conference on Supercomputing (ICS) '21:

<html>
<body>

<iframe width="560" height="315" src="https://www.youtube.com/embed/eG6lrRdyNtM" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

</body>
</html>
<p>&nbsp;</p>


The Project has been divided into the following stages:

### Stage-1 : Analysis of Subscripted subscript Patterns

In this stage, we go through several Benchmark suites - NAS Parallel Benchmarks, SuiteSparse, SPEC CPU 2006 etc. and try to analyze the subscripted subscript patterns inorder to come up with properties that characterize the subscript array. These properties aid in parallelizing the loops. Injectivity and Monotonicity were the most important and the most pervasive properties that we came across in our analysis. In addition to the aforementioned properties, we have also discovered certain complex properties that require advanced symbolic analysis.

Following is an example of a subscripted subscript pattern:

```C

  for(i = 0 ; i < n; i++){
      a[b[i]] = expr;
  }

```
Above loop is parallelizable if array "b" is injective.

### Stage-2 : Compile-time Algorithm for Subscripted-subscripts

After having completed the analysis of the subscript array patterns in the benchmark codes, we propose a compile time algorithm based on Symbolic Range Aggregation that will help us detect some of the properties discovered in stage 1 and help prove parallelism. We have applied our algorithm by hand to example loops from real scientific application. The algorithm and performance results have been described in detail in our ICS'21 paper below. Currently the algorithm can handle a class of subscripted
subscripts.

Refer to the following publications for more details:

### Publication:
* Akshay Bhosale and Rudolf Eigenmann. 2021. [On the automatic parallelization of subscripted subscript patterns using array property analysis](https://dl.acm.org/doi/10.1145/3447818.3460424). In Proceedings of the ACM International Conference on Supercomputing (ICS '21). Association for Computing Machinery, New York, NY, USA, 392–403. 

* Akshay Bhosale, and Rudolf Eigenmann. "[Compile-time Parallelization of Subscripted Subscript Patterns](https://ieeexplore.ieee.org/abstract/document/9150392?casa_token=t0g4f4I0ce0AAAAA:qM6cBc5kn9EEtWBCc-BJKqLzxdfFv-B48LH4v_oJZ0ikzHyl9sQm6nI7S8pkTREOHxNJn5Sgyw)" 2020 IEEE International Parallel and Distributed Processing Symposium   Workshops (IPDPSW). IEEE, 2020.

### Stage-3 : Implementation of the techniques inside Cetus

Our eventual goal is to implement the symbolic analysis techniques proposed in stage 2 inside the [**Cetus**](https://engineering.purdue.edu/Cetus/) source to source compiler infrastructure. The implemented technique would enable analysis and parallelization of the subscripted-subscript patterns within benchmark codes identified in stage 1. We will
also be extending the Data Dependence Test in Cetus to disprove dependencies in loops with subscript arrays in the presence of a property, and parallelize the enclosing loops.

#### Benchmark Suites used for analysis:

Here are some popular benchmark suites wherein you can find loops with subscripted-subscript patterns:

* [NAS Parallel Benchmark Suite](https://www.nas.nasa.gov/publications/npb.html)
* [SuiteSparse](http://faculty.cse.tamu.edu/davis/suitesparse.html)
* [SPEC CPU 2006](https://www.spec.org/cpu2006/)
* [Crossroads Benchmark Suite](https://www.lanl.gov/projects/crossroads/benchmarks-performance-analysis.php)
* [Sparselib++](https://math.nist.gov/sparselib++/)




