# C-Study
算海团队C++作业仓库

## 作业内容
1. 安装 VTK, Eigen, MFEM, Gmsh, Mumps
(1) 安装依赖
```bash
sudo apt install libgmp-dev libmpfr-dev libboost-dev
sudo apt install zlib1g-dev libblas-dev liblapack-dev
sudo apt install libglu1-mesa-dev freeglut3-dev mesa-common-dev
sudo apt install libopenblas-dev
sudo apt install libopenmpi-dev
sudo apt install libparmetis-dev libmetis-dev
sudo apt install libscalapack-openmpi-dev
```

(2) Eigen
```bash
sudo apt install libopenblas-dev
sudo apt install libeigen3-dev
```

(3)MFEM
```bash
git clone git@github.com:weihuayi/mfem.git
cd mfem
mkdir build 
cd build
cmake -D CMAKE_BUILD_TYPE:STRING=Release -D CMAKE_INSTALL_PREFIX=~/.local/mfem ..
make -j 8
make install
```
(4) CGAL https://github.com/CGAL/cgal/archive/refs/tags/v5.6.1.tar.gz
解压下载的文件，进入文件夹，在该文件夹下打开终端，输入以下命令：
```bash
mkdir build
cd build
cmake -D CMAKE_BUILD_TYPE:STRING=Release -D CMAKE_INSTALL_PREFIX=~/.local/cgal ..
make install
```
(5) VTK https://vtk.org/download/#latest
解压下载的文件，进入文件夹，在该文件夹下打开终端，输入以下命令：
```bash
mkdir build
cd build
cmake -D CMAKE_INSTALL_PREFIX=~/.local/vtk ..
make -j8
make install
```
(6) MUMPS
```bash
sudo apt install libmumps64-scotch-dev
```

2. 创建一个自己文件夹命名为自己的名字拼音全拼，如：zhangsan.
3. 把仓库中的 test, include 文件夹，CMakeLists.txt 文件复制到自己的文件夹中。
4. 编译自己文件夹的代码
```bash
mkdir build
cd build
cmake ..
make test_cgal
```
5. 自己编写一个C++程序，实现以下功能：
(1) 基于 Eigen 定义两个10乘10的矩阵 A 和 B，计算 
    1. AB
    2. A^T B
    3. A 和 B 的内积，即 A 和 B 的对应元素相乘再相加
(2) 在 test 中的 CMakeLists.txt，模仿 test_cgal 写自己程序的编译命令，注意要链接 Eigen 库。
(3) 编译自己的代码

