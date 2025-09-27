

## The Project

[Link to the GitHub Repository](https://github.com/akshay9594/The-Cetus-Project/tree/SubSub_Analysis)

A number of scientific applications comprise of loops wherein an array is subscripted by another array - a[b[i]]. With write references to the host array (array 'a') within a loop, current compile-time techniques are incapable of detecting such loops as parallelizable. If left unparallelized, these loops can in-turn prevent the performance obtained through automatic parallelization matching that of the hand parallelized version. Hence, Subscripted subscript analysis is the next big challenge in Automatic Parallelization. 

The Project has been divided into the following stages with all three stages now complete:

### Stage-1 : Analysis of Subscripted subscript Patterns

In this stage, we go through several Benchmark suites - NAS Parallel Benchmarks, SuiteSparse, SPEC OMP 2012 etc. and try to analyze the subscripted subscript patterns inorder to come up with properties that characterize the subscript array. These properties aid in parallelizing the loops. Monotonicity was the most important and the most pervasive property that we came across in our analysis. In addition to the aforementioned properties, we have also discovered certain complex properties that require advanced symbolic analysis.

Following is an example of a subscripted subscript pattern:

```C

  for(i = 0 ; i < n; i++){
      a[b[i]] = expr;
  }

```
Above loop is parallelizable if array "b" is strictly monotonic or injective.

### Stage-2 : Compile-time Algorithm for Subscripted-subscripts

We propose a compile time algorithm based on Symbolic Range Aggregation that can detect some of the properties discovered in stage 1 and help prove parallelism. We have implemented the algorithm in the 
[**Cetus**](https://sites.udel.edu/cetus-cid/) source to source compiler infrastructure and have applied it on subscripted subscript loops in scientific applications. The list of the applications can be found in the GitHub Repository linked above as well as in the publications below.
Refer to the following publications for more details:

### Publications:
* Akshay Bhosale and Rudolf Eigenmann, “Recurrence analysis for automatic parallelization of subscripted subscripts,” in Proceedings of the 29th ACM SIGPLAN Symposium on Principles and Practice of Parallel Programming, ser. PPoPP ’24, Edinburgh, United Kingdom: Association for Computing Machinery, 2024, pp. 392–403, isbn: 97984007043522403. doi: 10.1145/3627535.3638493.

* Akshay Bhosale and Rudolf Eigenmann. 2021. [On the automatic parallelization of subscripted subscript patterns using array property analysis](https://dl.acm.org/doi/10.1145/3447818.3460424). In Proceedings of the ACM International Conference on Supercomputing (ICS '21). Association for Computing Machinery, New York, NY, USA, 392–403. [_Erratum_](https://akshayud.me/Erratum_ICS2021.pdf)

* Akshay Bhosale, and Rudolf Eigenmann. "[Compile-time Parallelization of Subscripted Subscript Patterns](https://ieeexplore.ieee.org/abstract/document/9150392?casa_token=t0g4f4I0ce0AAAAA:qM6cBc5kn9EEtWBCc-BJKqLzxdfFv-B48LH4v_oJZ0ikzHyl9sQm6nI7S8pkTREOHxNJn5Sgyw)" 2020 IEEE International Parallel and Distributed Processing Symposium   Workshops (IPDPSW). IEEE, 2020.

### Stage-3 : Extending the Cetus Dependence Test

We will have extended the Data Dependence Test in Cetus to disprove dependencies in loops with subscript arrays and parallelize the enclosing loops. The dependence test queries the analysis algorithm for information about the subscript array properties. The extended data dependence test will be described in a forthcoming contribution.

#### Benchmark Suites used for analysis:

Here are some popular benchmark suites wherein you can find loops with subscripted-subscript patterns:

* [NAS Parallel Benchmark Suite](https://www.nas.nasa.gov/publications/npb.html)
* [SuiteSparse](http://faculty.cse.tamu.edu/davis/suitesparse.html)
* [Sparselib++](https://math.nist.gov/sparselib++/)




