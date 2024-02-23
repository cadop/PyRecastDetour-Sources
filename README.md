make a venv

pip install pybind11
pip install cmake


find where the pybind11 is. 
python -c "import pybind11; print(pybind11.get_cmake_dir())"

Use that directory to insert into the next step of cmake

create a CMakeLists.txt

```
cmake_minimum_required(VERSION 3.5)
project(ExamplePybind)

# Find pybind11
set(pybind11_DIR "directory_path")

find_package(pybind11 CONFIG REQUIRED)

# add_subdirectory(pybind11)
pybind11_add_module(example src/example.cpp)

```

Create a sample cpp file `example.cpp`


```
#include <pybind11/pybind11.h>

int add(int i, int j) {
    return i + j;
}

PYBIND11_MODULE(example, m) {
    m.doc() = "pybind11 example plugin"; // optional module docstring
    m.def("add", &add, "A function which adds two numbers");
}

```

mkdir build
cd build
cmake ..
cmake --build . --config Release