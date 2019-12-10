# buildOpenCV
Script for building OpenCV 4 on the NVIDIA Jetson Nano Developer Kit

Building for:
* Jetson Nano
* L4T 32.2.1/JetPack 4.2.2
* OpenCV 4.1.1
* Packaging Option ( Builds package by default; --no_package does not build package)

<em><b>Note: </b>The script does not check to see which version of L4T is running before building, understand the script may only work with the stated versions.</em>

### Building
This is a long build, you may want to write to a log file, for example:

<blockquote>$ ./buildOpenCV.sh |& tee openCV_build.log</blockquote>

While the build will still be written to the console, the build log will be written to openCV_build.log for later review.

On the Jetson Nano, this is a challenging build. There is not enough memory on the Nano to make with multiple jobs (i.e)

<blockquote>$ make -j4</blockquote>

without using a significant amount of swap file space. With L4T 32.2.1, there is a default swap space. However, if you are using a SD card, this can result in long compile times as both physcial memory and the swap file memory exhaust. Recommend using a USB drive for building. If you use a SD card, consider setting the environment variable NUM_JOBS in the buildOpenCV.sh script to 1. The build time may be longer, but you will not have the same amount of memory/SD card thrashing. If you are using a USB drive, you may want to add a swapfile: https://github.com/JetsonHacksNano/installSwapfile.

Note that if you are building for Python, you most definitely will benefit from building with a swap file and running on a USB drive. See: https://github.com/JetsonHacksNano/installSwapfile 

### Usage

<blockquote>usage: ./buildOpenCV.sh [[-s sourcedir ] | [-h]]<br>
&nbsp;&nbsp;&nbsp;&nbsp; -s | --sourcedir   Directory in which to place the opencv sources (default $HOME ; this is usually ~/)<br>
&nbsp;&nbsp;&nbsp;&nbsp; -i | --installdir  Directory in which to install opencv libraries (default /usr/local)<br>
&nbsp;&nbsp;&nbsp;&nbsp; --no_package       Do not package OpenCV as .deb file (default is true)<br>
&nbsp;&nbsp;&nbsp;&nbsp; -h | --help        Print help</blockquote>

## Build Parameters
OpenCV is a very rich environment, with many different options available. Check the script to make sure that the options you need are included/excluded. By default, the buildOpenCV.sh script selects these major options:

* CUDA on
* GStreamer
* V4L - (Video for Linux)
* QT - (<em>No gtk support built in</em>)
* Python 2 bindings
* Python 3 bindings

## Packaging
By default, the build will create a OpenCV package. The package file will be found in:
<blockquote>opencv/build/_CPACK_Packages/Linux/STGZ/OpenCV-4.1.1-<<em>commit</em>>-aarch64.sh</blockquote>

The advantage of packaging is that you can use the resulting package file to install this OpenCV build on other machines without having to rebuild. Whether the OpenCV package is built or not is controlled by the CMake directive <b>CPACK_BINARY_DEB</b> in the script.

## Notes

<b>November 2019, Initial Release</b>

* Jetson Nano
* L4T 32.2.1/JetPack 4.2.2
* OpenCV 4.1.1
* Packaging Option ( Builds package by default; --no_package does not build package)
