# Bontebok

A simple consistent compilation framework based on Makefiles.

This project is written for C project compiled by GCC on Linux.

## Tutorial

The source code is inside `PROJECT_ROOT/src` folder.

The structure is
```
├── Makefile
├── h
│   ├── header1.h
│   ├── header2.h
│   ├── header3.h
│   └── header4.h
├── mod1
│   ├── Makefile
│   ├── mod11
│   │   ├── Makefile
│   │   ├── mod111
│   │   │   ├── Makefile
│   │   │   └── mod111_a.c
│   │   ├── mod112
│   │   │   ├── Makefile
│   │   │   └── mod112_a.c
│   │   └── mod11_a.c
│   ├── mod1_a.c
│   └── mod1_b.c
├── mod2
│   ├── Makefile
│   └── mod2_a.c
├── tool1
│   ├── Makefile
│   ├── tool1.c
│   └── tool1_mod1
│       ├── Makefile
│       └── tmod1.c
└── tool2
    ├── Makefile
    └── tool2_a.c
```

Execute `make` in `PROJECT_ROOT`.

The output is a new `PROJECT_ROOT/_prod` folder and all its content.
```
_prod
├── bin
│   ├── tool1
│   └── tool2
├── lib
│   ├── libmod1.a
│   ├── libmod11.a
│   ├── libmod111.a
│   ├── libmod112.a
│   ├── libmod2.a
│   └── libtool1_mod1.a
└── objs
    ├── mod1
    │   ├── mod11
    │   │   ├── mod111
    │   │   │   ├── mod111_a.d
    │   │   │   └── mod111_a.o
    │   │   ├── mod112
    │   │   │   ├── mod112_a.d
    │   │   │   └── mod112_a.o
    │   │   ├── mod11_a.d
    │   │   └── mod11_a.o
    │   ├── mod1_a.d
    │   ├── mod1_a.o
    │   ├── mod1_b.d
    │   └── mod1_b.o
    ├── mod2
    │   ├── mod2_a.d
    │   └── mod2_a.o
    ├── tool1
    │   ├── tool1.d
    │   ├── tool1.o
    │   └── tool1_mod1
    │       ├── tmod1.d
    │       └── tmod1.o
    └── tool2
        ├── tool2_a.d
        └── tool2_a.o
```

The `_prod/bin` folder contains two executables, corresponding to the `src/tool1` and `src/tool2`.

The `_prod/lib` folder contains 6 libraries, corresponding to:
* `src/mod1`, `src/mod1/mod11`, `src/mod1/mod11/mod111` and `src/mod1/mod11/mod112`.
* `src/mod2`
* `src/tool1/tool1_mod1`

* type `make` in any directory containing a Makefile file to generate libraries and/or executables.
    * e.g. the output of executing `make` in `src/mod1/mod11/mod111` is:
```
_prod
├── bin
├── lib
│   └── libmod111.a
└── objs
    └── mod1
        └── mod11
            └── mod111
                ├── mod111_a.d
                └── mod111_a.o
```
* type `make clean` in any directory containing a Makefile file to clean up what `make` generated.
* create a directory, copy src/mod1/Makefile into the directory, write one or more src.c, just `make` to generate a library.
* create a directory, copy src/tool1/Makefile into the directory, write one main.c and/or more src.c, just `make` to generate a executable.

## More details

[Bontebok Complete Documentation](https://github.com/ifdefme/bontebok/tree/master/doc)
