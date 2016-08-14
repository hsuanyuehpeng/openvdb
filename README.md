[Original OpenVDB README](https://github.com/hsuanyuehpeng/openvdb/blob/master/README_OpenVDB.md)

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
  - Ilmbase
  - OpenEXR
  - TBB
  
## Buliding OpenVDB lib

## Buliding OpenVDB viewer/raytracer samples

## Reference
 - [rchoetzlein/win_openvdb](https://github.com/rchoetzlein/win_openvdb)
 - [::nidclip](https://nidclip.wordpress.com/2014/02/25/compiling-openvdb-the-openvdb-viewer-on-windows-7/)
