# gemm-pybind-learning

[简体中文README](README.zh.md)
=======
This repo demonstrates how to use pybind11 to provide python interface for highly optimized CUDA code. It only contains basic functionality.
Present work uses [modern CMake/Cuda](https://developer.download.nvidia.com/video/gputechconf/gtc/2019/presentation/s9444-build-systems-exploring-modern-cmake-cuda-v2.pdf) and [Yujia Zhai](yujiazhai94@gmail.com)'s [GEMV implementention](https://github.com/yzhaiustc/Optimizing-SGEMV-on-NVIDIA-GPUs) approach. 
CmakeLists comes from [pkestene](https://github.com/pkestene/pybind11-cuda)

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
python -c 'import mygemm; mygemm.host(4096, 4096, 1); mygemm.host(4096, 4096, 2)'
```

