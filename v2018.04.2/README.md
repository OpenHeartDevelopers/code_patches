# Patches for building MITK v2018.04.2 

These files are patches, which can be applied to a repository by using the command
`git apply [patchname.patch]`

### Notation
We assume the following: 
MITK's source folder is `SRC=/path/to/mitk-source`. 
BUILD folder is `BUILD=/path/to/mitk-build`.
The folder with this patches is `PATCHES=/path/to/code_patches`.

## List of files 
Not all files are needed to build CemrgApp. 
This document explains what each file changes in the code. 
Files with prefix `SRC_` correspond to changes to MITK's source code.  
Files with prefix `BUILD_` correspond to changes to the projects downloaded by MITK 
inside the build folder, for example, 

+ `BUILD_BASE_EIGEN.patch`
+ `BUILD_UBUNTU2004_CXX9.patch`
+ `SRC_BASE_MACOS.patch`
+ `SRC_BASE.patch`
+ `SRC_ROTMAT.patch`
+ `SRC_UBUNTU2004_CXX9.patch`

## `BUILD_` files 

### `BUILD_BASE_EIGEN` 

This needs to be applied the first time building CemrgApp (or MITK). 

This patch is applied to the `$BUILD/ep/src/Eigen/cmake/EigenConfigureTesting.cmake` file. 
This will add quotation marks to some input parameters of functions in the file.

Navigate to the `$BUILD/ep/src/Eigen/` folder 

```
git apply $PATCHES/v2018.04.2/BUILD_BASE_EIGEN.patch
```

### `BUILD_UBUNTU2004_CXX9` 

This patch updates the `$BUILD/ep/src/ITK/Modules/ThirdParty/VNL/src/vxl/vcl/vcl_compiler.h` file 
to allow higher versions of CXX, otherwise the compilation stops because ITK doesn't know 
which compiler is being used. 

This needs to be applied to the ITK source folder, which is downloaded to MITK automatically. 
Navigate to the folder 

```
cd $BUILD/ep/src/ITK
```

Then apply the patch: 
```
git apply $PATCHES/v2018.04.2/BUILD_UBUNTU2004_CXX9.patch
```

## `SRC_` files

To apply any of these, you need to navigate to the `$SRC` folder: 
```
cd $SRC
```

### `SRC_BASE`

This file does some basic changes to the MITK code, like disabling the compilation of MitkWorkbench, which
makes compilation take longer. 

Apply the patch: 
```
git apply $PATCHES/v2018.04.2/SRC_BASE.patch
```

### `SRC_BASE_MACOS`

This only needs to be applied in systems running macOS. 
Some basic C functions have a different names, which need to be reflected in the MITK source code. 

Apply the patch: 
```
git apply $PATCHES/v2018.04.2/SRC_BASE_MACOS.patch
```

### `SRC_ROTMAT`
This patch deals with an [MITK bug](https://github.com/OpenHeartDevelopers/CemrgApp/issues/29#issuecomment-975531614)
fixed in another branch of MITK. This file applies the changes from that file.

Apply the patch: 
```
git apply $PATCHES/v2018.04.2/SRC_ROTMAT.patch
```

### `SRC_UBUNTU2004_CXX9`

This file disables some `-Werror` flags in favour of `-Wno-error` to allow CemrgApp to be built 
on Ubuntu 20.04 and (hopefully) above. 

Apply the patch: 
```
git apply $PATCHES/v2018.04.2/SRC_UBUNTU2004_CXX.patch
```

### ``
