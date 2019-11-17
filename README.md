# buildOpenCV
Scripts for build OpenCV on the NVIDIA Jetson Nano Developer Kit

<b>Work in Progress</b>

This is a long build, it is recommended to write to a log file:

<blockquote>$ ./buildOpenCV.sh |& tee openCV_build.log</blockquote>

The log will be written to openCV_build.log for later review.

Usage: 
usage: ./buildOpenCV.sh [[-s sourcedir ] | [-h]]
   -s | --sourcedir   Directory in which to place the opencv sources (default /home/jetsonhacks)
   -i | --installdir  Directory in which to install opencv libraries (default /usr/local)
   --no_package       Do not package OpenCV as .deb file (default is true)
   -h | --help        Print help


Building for:
 Jetson Nano
 L4T 32.2.1/JetPack 4.2.2
 OpenCV 4.1.1
 Packaging Option ( Builds package by default; --no_package does not build package)
