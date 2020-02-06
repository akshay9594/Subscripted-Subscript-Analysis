## The Project

A number of scientific applications comprise of loops wherein there is an array subscripted by another array. When such arrays are written into in the loops, current compile-time techniques are incapacble of detecting such loops as parallelizable. If left unparallelized, these loops can in-turn prevent the performance obtained through automatic parallelization, matching that of the hand parallelized version. Hence, Subscripted subscript analysis is the next big challenge in Automatic Parallelization. 

The Project has been divided into the following stages:

### Stage-1 : Analysis of Subscripted subscript Patterns

In this stage, we go through several Benchmark suites - NAS Parallel Benchmarks, SuiteSparse, SPEC CPU 2006 etc. and try to analyze the subscripted subscript patterns inorder to come up with properties that characterize these patterns. These properties aid in parallelizing the loops. Injectivity and Monotonicity were the most important and the most pervasive properties that we came across in our analysis. In addition to the aforementioned properties, we have also discovered certain complex properties that require advanced symbolic analysis techniques.

Following is an example pattern:

```C

  for(i = 0 ; i < n; i++){
      a[b[i]] = expr;
  }

```
In the above example, the loop is parallelizable if array "b" is injective.

### Stage-2 : Compile-time Algorithm for Subscripted-subscripts

After having completed the analysis of the subscript array patterns in the benchmark codes, we propose a compile time algorithm based on Symbolic Range Aggregation that will help us detect some of the properties discovered in stage 1 and help prove parallelism. We have applied our algorithm by hand to some representative patterns of the benchmark codes.

A paper detailing the above 2 stages is available as a pre-print as of now at: [Paper link](https://arxiv.org/pdf/1911.05839)


