C# MVC 4 API Unit Test Example Project
=========================================

The following must be run using the `Developer Command Prompt for VS2013` or by executing the following in a command prompt beforehand from the root of the project:
	
	C:\Program Files\Microsoft Visual Studio 12.0\Common7\Tools\VsDevCmd.bat


To build the project:

	msbuild ci.build /t:Jenkins

To test the project (Must be built first):
    	
	mstest /testcontainer:MvcApplicationTest.Tests\bin\Debug\MvcApplicationTest.Tests.dll

### Jenkins/Hudson ###
Running in a CI environment can be rough. The following observations may assist you.

If you are running a newer VisualStudio ('10 SP1, '12 or '13) you can save yourself some time by using the MSBuild installation geared to your version. This can be found at:

	C:\Program Files\MSBuild\12.0\Bin\MSBuild.exe

Of course substituting `Program Files` for `Program Files (x86)` where necessary and `12.0` for whatever version you are running.

- Visual Studio 2010 = 10.0
- Visual Studio 2012 = 11.0
- Visual Studio 2013 = 12.0

