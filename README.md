# C++ Starter Project

Here are some of my default settings I like to use for C++

# Configure and Build Instructions

```
conan install . --install-folder build --build=missing -s build_type=Debug -pr:b=default
cmake -B build -DCMAKE_BUILD_TYPE=Debug -DCMAKE_EXPORT_COMPILE_COMMANDS=1 -DCMAKE_TOOLCHAIN_FILE=conan_toolchain.cmake . -GNinja -DBUILD_TESTING=1
cmake --build build
```
