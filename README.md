# Batched Refactorization in cuSolver

:exclamation: This software contains source code provided by NVIDIA Corporation.

Only some partially completed code snippets can be found in the documentation of cuSolver (CUDA 10.1) that are related to [batched refactorization](https://docs.nvidia.com/cuda/archive/10.1/cusolver/index.html#cuSolverRFbatch-example1).
In this repository, a complete example is provided to demonstrate the usage of related functions including ```cusolverRfBatchSetupHost```, 
```cusolverRfBatchAnalyze```, 
```cusolverRfBatchResetValues```, 
```cusolverRfBatchRefactor```, 
and ```cusolverRfBatchSolve()```.
This project is developed based on the unbatched refactorization example from Nvidia's official CUDA samples ```7_CUDALibraries/cuSolverRf```.

A 30x speedup was observed with the commands below.
```bash
./cuSolverRf -P=symamd -file=./lap2D_5pt_n100.mtx # 0.000708 sec for each linear system
./cuSolverRfBatch -P=symamd -file=./lap2D_5pt_n100.mtx -bs=256 # 0.000021 sec for each linear system
```
