# How to build libipt (Intel PT) on Windows

This is generally a huge pain in the ass so I'm going to add detailed instructions on how to do this for any future people (or myself)

```
git clone https://github.com/intelxed/mbuild mbuild
git clone https://github.com/intelxed/xed

mkdir xed-build
cd xed-build
python3 ..\xed\mfile.py examples
cd ..

mkdir xed-build32
cd xed-build32
python3 ..\xed\mfile.py --host-cpu=ia32 examples
cd ..

git clone https://github.com/intel/libipt libipt
cd libipt

mkdir build
cd build
cmake -G "Visual Studio 15 2017 Win64" -DPTDUMP=1 -DPTXED=1 -DXED_INCLUDE=..\..\xed-build\obj\wkit\include\xed -DXED_LIBDIR=..\..\xed-build\obj\wkit\lib ..
msbuild PT.sln /p:Configuration=Debug /p:Platform="x64"
msbuild PT.sln /p:Configuration=Release /p:Platform="x64"
msbuild PT.sln /p:Configuration=RelWithDebInfo /p:Platform="x64"
cd ..

mkdir build32
cd build32
cmake -G "Visual Studio 15 2017" -DPTDUMP=1 -DPTXED=1 -DXED_INCLUDE=..\..\xed-build\obj\wkit\include\xed -DXED_LIBDIR=..\..\xed-build32\obj\wkit\lib ..
msbuild PT.sln /p:Configuration=Debug /p:Platform="Win32"
msbuild PT.sln /p:Configuration=Release /p:Platform="Win32"
msbuild PT.sln /p:Configuration=RelWithDebInfo /p:Platform="Win32"
cd ..

cd ..
```
