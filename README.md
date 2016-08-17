[Original OpenVDB README](https://github.com/hsuanyuehpeng/openvdb/blob/master/README_OpenVDB.md)

##Note: This readme is not 100% complete yet, but it should get you going in building openvdb static lib.

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
    - [python] (https://www.python.org/downloads/windows/) (*Windows x86-64 build* version: 2.7.* whichever you feel comfortable) This will be used in boost and openvdb.
  - Extra/Optional dependencies
    - [glew](http://glew.sourceforge.net/) (*source*) Only if you want to build the sample viewer/tracer.
    - [glfw](http://www.glfw.org/) (glfw3 *source*) Only if you want to build the sample viewer/tracer. Some people say you can only build the sample viewer/tracer on glfw2, that's __NOT__ true, you can easily build the current version with glfw3.

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
    - Side note: if you seen any other lib's cmake configuration erorr: *Could NOT find ZLIB (missing: ZLIB_LIBRARY ZLIB_INCLUDE_DIR)* that depends on zlib (according to [this](http://stackoverflow.com/questions/24808150/how-to-point-cmake-to-zlib-include-path)):
      - check the "Advanced" checkbox in cmake gui
      - set "ZLIB_LIBRARY" to your zlib library folder, where zlib.lib or zlibstatic.lib is contained
      - set "ZLIB_INCLUDE_DIR" to your zlib include folder, where zlib.h is contained
      
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
    - Tuning *Configure -> Generate -> Code Generation* as in zlib build step -> Build solution on both Release and Debug configs.
    
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
    - Tuning *Configure -> Generate -> Code Generation* as in zlib build step -> Build solution on both Release and Debug configs.
    
  - TBB
    - Downdload and extract openexr sources into
    ```
      D:\libs\tbb\v44u5\source
    ```
  - python
    - Download from [here](https://www.python.org/download/releases/2.7/) and make sure you click "Windows X86-64 MSI Installer (2.7.0)" for x64 installation
    - python3 should also work, although in my openvdb build, I'm using python2
    
  - glew & glfw
    - Similar cmake with static preprocessor*, will not include in this breakdown readme
  
## Buliding OpenVDB lib
  - One thing you need to make sure is that we are not using cmake to build openvdb (you could, if you follow [this](https://github.com/rchoetzlein/win_openvdb)), so we need to add all dependencies' include paths manually. This could take a bit of time, but all you need to do is to find the headers for each lib into where OpenVDB is looking for. For example, I put Ilmbase related headers in *[D:\libs\ilmbase\v2.2.0\source\include\OpenEXR]* and add *[D:\libs\ilmbase\v2.2.0\source\include]* into the project's additional include directories so that it can find *[OpenEXR\half.h]*. If you understand that, the same analogy applies onto other libs as well.
  - You can drag all the source(s) (*.cpp/*.h) into a new visual studio solution with a new empty project. Then exclude all the main.cpp's and Test*.cc's from the build process.
  - Switch to static lib build and make sure you have /MT and /MTd for Release and Debug config. respectively
  - Preprocessor
    ```
      BOOST_PYTHON_STATIC_LIB // for boost linking correctly
      
      OPENVDB_OPENEXR_STATICLIB
      
      GLEW_STATIC             // <= only if you also want to build sample viewer/tracer
      
      OPENVDB_USE_GLFW_3		// <= only if you also want to build sample viewer/tracer
    ``` 
  - Macro define before including some headers
    - Whenever you see vs2013 complaining about min/max function name(s) (Coord.h, ..etc.)
    ```
      #define NOMINMAX //(thx vs2013..)
    ```
    - In Compression.cc (based on [this](http://www.winimage.com/zLibDll/index.html) with *"Make sure to define ZLIB_WINAPI before including zlib.h."*)
    ```
       #define ZLIB_WINAPI
    ```
  
  - [vs2013 syntax error when compiling LeafNode.h](http://www.openvdb.org/forum/?place=msg%2Fopenvdb-forum%2FVHJelGwmo8I%2FoExDaKvCbMsJ)
    When you encounter:
    ```
      error C2226: syntax error : unexpected type 'SIZE'	openvdb\tree\LeafNode.h 79
      error C2065: 'LEVEL' : undeclared identifier	openvdb\tree\InternalNode.h	74
    ```
    
    Replace:
    ```
    static const Index
		LOG2DIM = Log2Dim,      // needed by parent nodes
		TOTAL = Log2Dim,      // needed by parent nodes
		DIM = 1 << TOTAL,   // dimension along one coordinate direction
		NUM_VALUES = 1 << 3 * Log2Dim,
		NUM_VOXELS = NUM_VALUES,  // total number of voxels represented by this node
		SIZE = NUM_VALUES,
        	LEVEL       = 0;            // level 0 = leaf
    ```
    with:
    ```
    static const Index
		LOG2DIM = Log2Dim,      // needed by parent nodes
		TOTAL = Log2Dim,      // needed by parent nodes
		DIM = 1 << TOTAL,   // dimension along one coordinate direction
		NUM_VALUES = 1 << 3 * Log2Dim,
		NUM_VOXELS = NUM_VALUES;   // total number of voxels represented by this node
	static const Index
		SIZE = NUM_VALUES,
        	LEVEL       = 0;            // level 0 = leaf
    ```

## Buliding OpenVDB viewer/raytracer samples
  - Viewer
    - Make another project under the same solution and add *[D:\libs\openvdb\v3.2.0\source\openvdb\cmd\openvdb_view\main.cc]* into the project, where you see its the first include is:
    ```
      #include <openvdb/viewer/Viewer.h>
    ```
    - Find all files that do this:
    ```
      #include <GL/gl.h>
      #include <GL/glu.h>
    ```
      and replace them with
    ```
      #include <GL/glew.h>
    ```
    - Add OPENVDB_USE_GLFW_3 into your preprocessor and replace *#include <GL/glfw.h>* with *#include <GLFW/glfw3.h>*
    - Add *openvdb* static lib project into your project reference (Proj. Properties -> Common Properties -> References -> Add New Reference...)
    - Don't forget to add glew/glfw into your include folder path, also inputs to the linker
    - Also need to add opengl32.lib and glu32.lib from windows' sdk
    - You should be able to compile and run the viewer after this
    - According to [::nidclip](https://nidclip.wordpress.com/2014/02/25/compiling-openvdb-the-openvdb-viewer-on-windows-7/), the viewer fails to initialize the gl function pointers before calling for each thread. So add "glewInit();" to some blocks like this:
  
  ```
    Viewer
    init(const std::string&amp; progName, bool verbose)
    {
      glewInit();  // added
      …
    }
  ```
  ```
    ShaderProgram::ShaderProgram():
      mProgram(0),
      mVertShader(0),
      mFragShader(0)
    {
      glewInit(); // added
    }
  ```
  
  - Raytracer
    - Similar to viewer building process, make project, add *[D:\libs\openvdb\v3.2.0\source\openvdb\cmd\openvdb_render]*, add lib reference, build and run
    - Somehow I got msvcrt.lib/msvcrtd.lib not included error when compiling the sample raytracer. By adding msvcrt.lib/msvcrtd.lib into the linker manually (w.r.t. $(Configuration)) solves the problem. Still have no idea yet..
  
## Reference
 - [rchoetzlein/win_openvdb](https://github.com/rchoetzlein/win_openvdb)
 - [::nidclip](https://nidclip.wordpress.com/2014/02/25/compiling-openvdb-the-openvdb-viewer-on-windows-7/)
 - [Wen tao. Wang](http://www.cnblogs.com/warpengine/p/3462359.html) (Chinese only)
