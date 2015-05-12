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
1. Rebuild .lib (both Debug and Release) according to your Visual Studio version (located in Libraries/Effects11).
2. Include "dxerr.h" and "dxerr.cpp" in Box project (located in Libraries/dxerr/).
3. In Box project, set project properties. (Include Directories, Library Directories)
4. Add "#include <d3d11.h>" in "d3dUtil.h".
5. Modify code of Line 40, DXTrace function call in "d3dUtil.h": Type of parameter 1 converts to WCHAR* -> (WCHAR*)FILE
6. Modify code of Line 310, DXTrace function call in "BoxDemo.cpp": Type of parameter 1 converts to WCHAR* -> (WCHAR*)FILE
7. Compile and build it.