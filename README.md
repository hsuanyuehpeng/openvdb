[Original OpenVDB README](https://github.com/hsuanyuehpeng/openvdb/blob/master/README_OpenVDB.md)

##Note: This readme is not yet finished, more details are needed to be filled in.. (Aug 14, 2016 HY)

#OpenVDB Building on Windows, VS2013, x64

## Purpose
This readme is made by Hsuan-Yueh Peng, which aims to compile the openvdb lib on:
    
    OS/IDE: windows visual studio 2013
    Platform: x64
    Lib type: static lib

## Prerequisites
This requires the basic knowledge on:
  - Software/Building Tools
    - Visual Studio 2013
    - CMake
  - Dependent libraries
    - [Boost](https://sourceforge.net/projects/boost/files/boost-binaries/) (I use prebuilt binaries)
    - [zlib](http://www.winimage.com/zLibDll/index.html) (sources)
    - [Ilmbase](http://www.openexr.com/downloads.html) (*ilmbase-2.2.0.tar.gz* used here)    
    - [OpenEXR](http://www.openexr.com/downloads.html) (*openexr-2.2.0.tar.gz* used here)
    - [TBB](https://www.threadingbuildingblocks.org/download#stable-releases)(*4.4 Update 5* statble release used here)
  - Extra/Optional dependencies
    - [python] (https://www.python.org/downloads/windows/) (*Windows x86-64 build* version: 2.7.* whichever you feel comfortable) This will be used in boost and openvdb.
    - [glew](http://glew.sourceforge.net/) (*source*) Only if you want to build the sample viewer/tracer.
    - [glfw](http://www.glfw.org/) (*source*) Only if you want to build the sample viewer/tracer.

## Building prerequisites
  - Boost
    - Once you download and extract the boost prebuilt package, you can put it somewhere in your filesystem. For me I put the package under:
    ```
      D:\libs\boost\v1.57.0\prebuilt
    ```
    - You will see the extracted package sits in (I know the structure looks dump, but that's how I do it :P):
    ```
      D:\libs\boost\v1.57.0\prebuilt\boost_1_57_0
    ```
  - zlib
    - Downdload and extract your zlib sources into
    ```
      D:\libs\zlib\source
    ```
    - To be clear, you should see the full path of zlib.h like this
    ```
      D:\libs\zlib\source\zlib.h
    ```
    - Use cmake to point the source path to
    ```
      D:\libs\zlib\source
    ```
    - Build path to
    ```
      D:\libs\zlib\build
    ```
    - Configure with Visual Studio 2013 win64
    - Generate
    - Open the zlib vs2013 solution (D:\libs\zlib\build\zlib.sln)
    - Turn the code generation into
      - /MT for Release build
      - /MTd for Debug build
    - Build the solution on both Release and Debug configuration (and pay attention to the built destination)
    
  - Ilmbase
    - Downdload and extract ilmbase sources into
    ```
      D:\libs\ilmbase\v2.2.0\source
    ```
    - CMake source path
    ```
      D:\libs\ilmbase\v2.2.0\source
    ```
    - Cmake build path
    ```
      D:\libs\ilmbase\v2.2.0\build
    ```
    - Configure -> Generate -> Tuning *Code Generation* as in zlib build step -> Build solution on both Release and Debug configs.
    
  - OpenEXR
    - Same as Ilmbase, downdload and extract openexr sources into
    ```
      D:\libs\openexr\v2.2.0\source
    ```
    - CMake source path
    ```
      D:\libs\openexr\v2.2.0\source
    ```
    - Cmake build path
    ```
      D:\libs\openexr\v2.2.0\build
    ```
    - Configure -> Generate -> Tuning *Code Generation* as in zlib build step -> Build solution on both Release and Debug configs.
    
  - TBB
    - Downdload and extract openexr sources into
    ```
      D:\libs\tbb\v44u5\source
    ```
  
## Buliding OpenVDB lib
  - [vs2013 syntax error when compiling LeafNode.h](http://www.openvdb.org/forum/?place=msg%2Fopenvdb-forum%2FVHJelGwmo8I%2FoExDaKvCbMsJ)
    When you encounter:
```
error C2226: syntax error : unexpected type 'SIZE'	openvdb\tree\LeafNode.h 79
error C2065: 'LEVEL' : undeclared identifier	openvdb\tree\InternalNode.h	74
... and more
```
  - t

## Buliding OpenVDB viewer/raytracer samples

## Reference
 - [rchoetzlein/win_openvdb](https://github.com/rchoetzlein/win_openvdb)
 - [::nidclip](https://nidclip.wordpress.com/2014/02/25/compiling-openvdb-the-openvdb-viewer-on-windows-7/)
