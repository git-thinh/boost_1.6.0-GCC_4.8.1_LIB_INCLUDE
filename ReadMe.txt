mingw-w64-x86_64-gcc4.8.1-win32-sjlj

git clone https://github.com/google/protobuf.git
cd protobuf
mkdir install_dir
mkdir cmake_build
cd cmake_build
cmake -DCMAKE_INSTALL_PREFIX=../install_dir -DCMAKE_INSTALL_LIBDIR=lib -Dprotobuf_BUILD_TESTS=OFF -DCMAKE_CXX_FLAGS="-std=c++11" -DCMAKE_BUILD_TYPE=Release -G "MinGW Makefiles" ../cmake
mingw32-make
mingw32-make install

g++ -I"C:/C++/protobuf/protobuf.3.5.1-gcc.5.1.0/include" -L"C:/C++/protobuf/protobuf.3.5.1-gcc.5.1.0/lib" main.cpp addressbook.pb.cc -lprotobuf -pthread -static-libgcc -std=c++11

----------------------------------------------------------------------------
Installing boost libraries for GCC (MinGW) on Windows

GCC 4.8.1 for C++11: https://sourceforge.net/projects/mingw-w64/files/Toolchains%20targetting%20Win64/Personal%20Builds/mingw-builds/4.8.1/threads-win32/sjlj/x86_64-4.8.1-release-win32-sjlj-rt_v3-rev2.7z/download
Boost 1.6.0: http://sourceforge.net/projects/boost/files/boost/1.60.0/boost_1_60_0.zip

Folder setup
	Extract downloaded boost source, e.g. C:\Program Files\boost_1_60_0.
	Create a folder for Boost.Build installation, e.g. C:\Program Files\boost-build.
	Create a folder within for building, i.e. C:\Program Files\boost_1_60_0\build.
	Create a folder for installation, e.g. C:\Program Files\boost.
	
GCC setup
	Open Command Prompt.
	Run g++ --version.
	If the output contains g++ version number then GCC should be set up properly to run from command line and you can continue.
	
Boost.Build setup
	Open Command Prompt and navigate to C:\Program Files\boost_1_60_0\tools\build.
	Run bootstrap.bat mingw.
	Run b2 install --prefix="C:\Program Files\boost-build".
	Add C:\Program Files\boost-build\bin to Windows PATH.

Boost building
	Open Command Prompt and navigate to C:\Program Files\boost_1_60_0.
	Run
	b2 --build-dir="C:\Program Files\boost_1_60_0\build" --prefix="C:\Program Files\boost" toolset=gcc install

It is still possible to explicitly specify target 
Windows version by defining BOOST_USE_WINAPI_VERSION to a numeric version of Windows API. 
For example, building Boost for Windows XP can be done with the following command:

	b2 release define=BOOST_USE_WINAPI_VERSION=0x0501 --build-dir="C:\Program Files\boost_1_60_0\build" --prefix="C:\Program Files\boost-xp"

Project setup
	Add include folder, i.e. C:\Program Files\boost\include\boost-1_60.
	Add linker folder, i.e. C:\Program Files\boost\lib.
	Link required libraries, e.g. libboost_regex-mgw48-mt-1_60.a.

BOOST_160_GCC_481_LIB 		= C:\Program Files\boost\lib
BOOST_160_GCC_481_INCLUDE 	= C:\Program Files\boost\include\boost-1_60

