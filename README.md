# DirectX
Visual Studio 2015 version of Frank D. Luna's book "Introduction to 3D Game Programming using DirectX 11" and various samples related to DirectX 11, 12.

## Frank D. Luna's Issues
When you use Frank D. Luna's "Introduction to 3D Game Programming using DirectX 11" book samples in different version of Visual Studio, it occurs linking errors.

### Effects11
Effects11d.lib (Debug) and Effects11.lib (Release) are dependent to Visual Studio version.
If you use different version of Visual Studio, rebuild .lib using Effects11 project.

References: https://fx11.codeplex.com/wikipage?title=Effects%2011

### Dxerr
One of the little utility in the DirectX SDK is a static library for converting HRESULTs to text strings for debugging and diagnostics known as Dxerr.lib. There were once even older versions of this library, Dxerr8.lib and Dxerr9.lib, but they were removed from the DirectX SDK many years back in favor of a unified Dxerr.lib. The DirectX Error Lookup Utility is nothing more than a little front-end UI tool for getting results from Dxerr.lib.

References: http://blogs.msdn.com/b/chuckw/archive/2012/04/24/where-s-dxerr-lib.aspx

### Solutions ("Box" Example)
1. Rebuild .lib (both Debug and Release) according to your Visual Studio version (located in "Libraries/Effects11/").
2. Rename "Effects11.lib" of debug version to "Effects11d.lib".
3. Crop "Effects11d.lib" and "Effects11.lib" in "Libraries/Effects11/Debug/" and "Libraries/Effects11/Release/", then paste it in "DirectX 11/Frank D. Luna/Common/".
4. Copy "dxerr.h" and "dxerr.cpp" in "Libraries/dxerr/", then paste it in "DirectX 11/Frank D. Luna/Common/".      
5. Add "dxerr.h" and "dxerr.cpp" to Box project.
6. In Box project, set project properties (Include Directories, Library Directories).
  - Include Directories: $(IncludePath);`(Absolute Path)`\DirectX 11\Common;$(DXSDK_DIR)Include  
  - Library Directories: $(LibraryPath);`(Absolute Path)`\DirectX 11\Common;$(DXSDK_DIR)Lib\x86
7. Copy "d3dx11effect.h" in "Libraries/Effects11/inc/", then paste it in "DirectX 11/Frank D. Luna/Common/". 
8. Include "d3d11.h" file in "d3dUtil.h".

    `#include <d3d11.h>`
9. Modify code of Line 40, DXTrace function call in "d3dUtil.h".

    `DXTrace((WCHAR*)__FILE__, (DWORD)__LINE__, hr, L#x, true);`
10. Modify code of Line 310, DXTrace function call in "BoxDemo.cpp".

    `DXTrace((WCHAR*)__FILE__, (DWORD)__LINE__, hr, L"D3DX11CompileFromFile", true);`
11. Compile and build it.