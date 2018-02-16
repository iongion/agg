Upgrade cmake to 3.10.0+
```
python -m pip install cmake --user
```

Enable conan bincrafters remote
```
conan remote add bincrafters https://api.bintray.com/conan/bincrafters/public-conan
```

Prepare the environment

```
mkdir build && cd build
conan install ..
cmake .. -G "Unix Makefiles" -DCMAKE_BUILD_TYPE=Release
make clean && make
```
