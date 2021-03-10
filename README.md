# Mixed Cpp & Python Project Template

## How to Builld

First, download the project from GitHub 
```
git clone https://github.com/nobuyuki83/ProjectTemplate_CppPython.git
```

Then, download the dependent module (pybind11)
```bash
git submodule update --init
```

Finally, build the python module writenn in C++. Currently this module has just one function to write "Hello World!" to the standard output.
```bash
cd my_cpp_module
mkdir build
cd build
cmake ..
make
```

A dynamic library `c_.***` will appear in in the `my_cpp_module` folder. You can use this module by importing this module from python. Check if the module can be used by running `hello_world.py`

```bash
python hello_world.py
```

enjoy~
