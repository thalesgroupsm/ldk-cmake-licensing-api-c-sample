This is the CMake sample to demostrate how to generate LDK licensing api sample project files on Windows or make file on Linux.

## Step 1
You need to use master wizard with physical master key to download required LDK licensing api libaries, and copy them into lib folder.

## Step 2
Update CMakeLists.txt, and rename all the libraries name to the exact libary file names.
For example, rename libhasp_windows_x64_demo.lib to libhasp_windows_x64_xxxx.lib which you download it via master wizard.

## Step 3
mkdir build && cd build
cmake .. -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX=.. -DBUILD_SHARED_LIBS=ON
make
