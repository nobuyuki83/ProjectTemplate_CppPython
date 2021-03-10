# Mixed Cpp & Python Project Template

## How to Builld

First, download the project from GitHub 
```
git clone 
```

Then, download the dependent module (pybind11)
```bash
git submodule update --init
```

Build the python module writenn in C++ 
```bash
cd my_cpp_module
mkdir build
cd build
cmake ..
make
```

A dynamic library `c_.***` will appear in in the `my_cpp_module` folder. You can use this module by importing this module from python. 

```bash
python hello_world.py
```

enjoy~
