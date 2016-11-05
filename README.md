# tensorflow-windows-build

tensorflow wheel file builded on Windows.  
The build flow is following the [cmake build guide](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/contrib/cmake/README.md).

tenforlow version is `0.11.0rc2`.

## How to install

```
pip install tensorflow-windows-build/cpu/tensorflow-0.11.0rc2_cmake_experimental-py3-none-any.whl
```

## Build environment

* Windows10(x64, Intel Core i7)
* Python 3.5.2
* Visual Studio Community 2015
 * You have to choose Visual C++ option, if you want to build tensorflow yourself.
* cmake 3.6.3
 * caution! 3.3.1 causes error when build
* numpy: 1.11.2
* swig: 3.0.10
* zlib: 1.2.8

You can create build environment by [`conda`](http://conda.pydata.org/miniconda.html).

```
conda create -n tensorflow-win swig numpy zlib
```

(`cmake` of conda is `3.3.1`, and it causes build error, so you have to install `cmake` yourself from [here](https://cmake.org/download/).)

build script is like below.

```
cmake .. -A x64 -DCMAKE_BUILD_TYPE=Release ^
-DSWIG_EXECUTABLE=<your_conda_env_path>\Library\bin\swig.exe ^
-DPYTHON_EXECUTABLE=<your_conda_env_path>\python.exe ^
-DPYTHON_LIBRARIES=<your_conda_env_path>\libs\python35.lib
```

To build the tenforflow, you need below resource.

* About `2G` disk space
* About `1 ~ 1.5 hours` to build (8G memory, Core i7)

And You have to change some of step.

* If you can't find `vcvarsall.bat`, you can use `vcvars64.bat` instead.
* I have to apply [this fix](https://github.com/tensorflow/tensorflow/pull/5411) (it fix is already merged at mater branch).

