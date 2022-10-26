# GEMM Pybind11 Learning

这个项目仅仅是为了学习练手pybind11和CUDA性能优化而编写的。为了缩短调试时间，我直接选取了最简单的矩阵乘法案例。
这里直接使用了[Yujia Zhai](yujiazhai94@gmail.com)的[优化实现](https://github.com/yzhaiustc/Optimizing-SGEMV-on-NVIDIA-GPUs)作为子模块。
cmake子文件夹的内容来自[modern CMake/Cuda](https://developer.download.nvidia.com/video/gputechconf/gtc/2019/presentation/s9444-build-systems-exploring-modern-cmake-cuda-v2.pdf)。
CMakeLists改写自[pkestene](https://github.com/pkestene/pybind11-cuda)
## 构建流程

本项目使用CMake（最低版本3.12）作为构建工具，后续可能会添加setuptools以及scikit-build的支持：

直接使用`git clone --recurse-submodules https://github.com/dongdongban/gemm-pybind-learning`或者分开来写：
```bash
git clone https://github.com/dongdongban/gemm-pybind-learning
cd gemm-pybind-learning
git submodule init
git submodule update
```

如果使用版本不低于3.18的CMake可以直接`cmake -S . -B build -DCMAKE_CUDA_ARCHITECTURES="75" && cd build`或者手动进行generate：
```bash
mkdir build && cd build
export CUDAFLAGS="-arch=sm_75"
cmake ..
```

然后`cmake --build .`进行构建

验证代码：
```bash
cd Optimizing-SGEMV-on-NVIDIA-GPUs
python -c 'import mygemm; mygemm.host(4096, 4096, 1); mygemm.host(4096, 4096, 2)'
```
即可测试矩阵乘法代码与CUBLAS的相对性能！
