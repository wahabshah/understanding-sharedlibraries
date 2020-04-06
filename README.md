# Library Creaion on Another Developer PC e.g Qt

```sh
gcc -c -fPIC shdLibDir/src/shrdLib.cpp -o shdLibDir/build/shrdLib.o
gcc -shared shdLibDir/build/shrdLib.o -Wl,-soname=libshardLib.so.1 -o shdLibDir/build/libshrdLib.so.1.0.0
readelf -d shdLibDir/build/libshrdLib.so.1.0.0
```

```sh
shdLibDir
├── build
│   ├── libshrdLib.so.1.0.0
│   └── shrdLib.o
├── include
│   └── shrdLib.h
└── src
    └── shrdLib.cpp
```

# Library Installation on Developer PC e.g apt install libgles2-messa-dev

```sh
cp shdLibDir/build/libshrdLib.so.1.0.0 shdLibDeploy/lib
ln -srf shdLibDeploy/lib/libshrdLib.so.1.0.0 shdLibDeploy/lib/libshdLib.so
cp shdLibDir/include/shrdLib.h shdLibDeploy/include
```

```sh
shdLibDeploy
├── include
│   └── shrdLib.h
└── lib
    ├── libshdLib.so -> libshrdLib.so.1.0.0
    └── libshrdLib.so.1.0.0
```

# Linking Library to create Application using installed Library on Developer PC e.g using Qt Creator

```sh
gcc -c client/main.cpp -I./shdLibDeploy/include -o client/build/main.o
g++ client/build/main.o -L./shdLibDeploy/lib -lshdLib -o client/build/main
readelf -d client/build/main
```

```sh
client
├── build
│   ├── main
│   └── main.o
└── main.cpp
shdLibDeploy
├── include
│   └── shrdLib.h
└── lib
    ├── libshdLib.so -> libshrdLib.so.1.0.0
    └── libshrdLib.so.1.0.0
```

# Running Application on Target PC e.g apt install libgles2-mesa

```sh
cp client/build/main Prod/bin
cp shdLibDeploy/lib/libshrdLib.so.1.0.0 Prod/lib
ln -srf Prod/lib/libshrdLib.so.1.0.0 Prod/lib/libshardLib.so.1
LD_LIBRARY_PATH=./Prod/lib ./Prod/bin/main
```

```sh
LD_LIBRARY_PATH=./Prod/lib
Prod
├── bin
│   └── main
└── lib
    ├── libshardLib.so.1 -> libshrdLib.so.1.0.0
    └── libshrdLib.so.1.0.0
```