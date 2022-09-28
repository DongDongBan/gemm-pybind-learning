# gemm-pybind-learning

[简体中文README](README.zh.md)
=======
This repo demonstrates how to use pybind11 to provide python interface for highly optimized CUDA code. It only contains basic functionality.

## Build and Install
This project requires CMake>=3.18, it can be built with code below:
```bash
git clone --recurse-submodules https://github.com/dongdongban/gemm-pybind-learning
cmake -S . -B build -DCMAKE_CUDA_ARCHITECTURES="75" && cd build
cmake --build .
```
The device architecture "sm_75" should be replaced by your native GPU capability.

### Verification
if Nothing went wrong, check your module with these codes:
```bash
cd Optimizing-SGEMV-on-NVIDIA-GPUs
python -c 'import mygemm; mygemm.host(4096, 4096, 1); mygemm(4096, 4096, 2)'
```

