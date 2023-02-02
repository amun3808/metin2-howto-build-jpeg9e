# How to compile libjpeg

1. Unzip `jpegsr9e.zip` and copy `win32.mak` into the folder(where all the files are)

2. Open Visual Studio, click `Tools` -> `Command Line` -> `Developer Command Prompt`

3. Cd into the folder where you unzipped the archive

4. Run `nmake /f makefile.vc setup-v17` in the Dev Command Prompt

```
setup-v17 is for visual studio 2019 - 2022 (I think)
If you don't have v17, just try all of them from 10 to 17, until you find one.
You can just upgrade the project once it's generated.
```
5. Open jpeg.sln, right click on the project -> `C/C++` -> `Code Generation` and change `Multi-threaded DLL (\MD)` to `Multi-threaded (\MT)` otherwise you'll get warnings when linking the client.

5. Make sure you have win32 selected and compile

## To compile in debug

1. Right click on the project -> Configuration -> Click on the dropdown(Where it says 'release') and click "New"
Name it "Debug" and copy configuration settings(from release)

2. Change the target name to something different(Like $(ProjectName)_$(Configuration), for example)

3. Click on C/C++ -> General and change `Debug Information Format` to `Program Database for Edit and Continue (\ZI)` or `C7 Compatible(\Z7)`, whatever you want.

4. Click on `Optimization` and change 
	- `Optimization` to `Disabled`
	- `Enable Fiber-Safe Optimizations` to `No`
	- `Whole Program Optimization` to `No`

5. Click on `Preprocessor` and replace `Preprocessor Definitions` with `WIN32;_DEBUG;DEBUG;_LIB;_CRT_SECURE_NO_WARNINGS`

6. Click on `Code Generation` and make sure `Runtime Library` is set to `Multi-threaded Debug (/MTd)`
	NOTE: Make sure it's not Multi-threaded Debug DLL (\MDd) otherwise you'll get warnings, because all the other libs are static.


## After it's compiled

Replace your jpeg include folder with jpeg-9e(you can unzip the archive again, so you don't copy VS files for no reason) and copy/paste `jpegliblink.h` to that folder.  

Rename jpeg.lib to jpeg-9eMT.lib
Rename jpeg_Debug.lib to jpeg-9eMTd.lib

If you want to avoid doing this, you can just change the output name to these values, or change the lib name in `jpegliblink.h` and you're good to go.