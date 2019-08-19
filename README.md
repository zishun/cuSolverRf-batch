# Batched Refactorization in cuSOLVER

> A complete example of batched refactorization in CUDA cuSOLVER.

[Batched refactorization module](https://docs.nvidia.com/cuda/archive/10.1/cusolver/index.html#glu-reference) in cuSOLVER provides an efficient method to solve batches of linear systems with fixed left hand side sparse matrix (or matrices with fixed sparsity pattern but varying cofficients) and varying right hand sides, based on LU decomposition.
Only some partially completed [code snippets](https://docs.nvidia.com/cuda/archive/10.1/cusolver/index.html#cuSolverRFbatch-example1) can be found in the official documentation (as of CUDA 10.1) that are related to it.
In this repository, a complete example is provided to demonstrate the usage of related functions including 
* ```cusolverRfBatchSetupHost```, 
* ```cusolverRfBatchAnalyze```, 
* ```cusolverRfBatchResetValues```, 
* ```cusolverRfBatchRefactor```, 
* and ```cusolverRfBatchSolve```.

## Build
This project is developed based on the unbatched refactorization example ```7_CUDALibraries/cuSolverRf``` from NVIDIA's official CUDA samples. You may modify ```CUDA_PATH``` in ```Makefile``` to build this project.

## Usage
A 30x speedup was observed with the commands below.
```sh
./cuSolverRf -P=symamd -file=./lap2D_5pt_n100.mtx # 0.000708 sec for each linear system
./cuSolverRfBatch -P=symamd -file=./lap2D_5pt_n100.mtx -bs=256 # 0.000021 sec for each linear system
```

## License
This software contains source code provided by NVIDIA Corporation. See [End User License Agreement](https://github.com/zishun/cuSolverRf-batch/blob/master/EULA.txt) for more information.
