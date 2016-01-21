# librealsense

[ ![Release] [release-image] ] [releases]
[ ![License] [license-image] ] [license]

[release-image]: http://img.shields.io/badge/release-0.9.0-blue.svg?style=flat
[releases]: https://github.com/IntelRealSense/librealsense

[license-image]: http://img.shields.io/badge/license-Apache--2-blue.svg?style=flat
[license]: LICENSE

Platform | Build Status |
-------- | ------------ |
Linux | Travis-CI (WIP) |
OSX | Travis-CI (WIP)|
Windows | Appveyor (WIP) | 

Librealsense is a cross-platform library (Linux, OSX, Windows) for capturing data from the Intel® RealSense™ F200, SR300 and R200 cameras. This effort was initiated to better support researchers and developers in domains such as robotics, virtual reality, and the internet of things. Several often-requested features of RealSense™ devices are implemented in librealsense, including multi-camera capture.

Developer kits containing the necessary hardware to use this library are available for purchase at [this link](http://click.intel.com/realsense.html). This project is separate from the production software stack available in the [Intel® RealSense™ SDK](https://software.intel.com/en-us/intel-realsense-sdk), namely that librealsense only encompasses camera capture functionality without additional computer vision algorithms.

Librealsense is experimental and not an official Intel product. It is subject to incompatible API changes in future updates. Breaking API changes are noted through release numbers with [semver](http://semver.org/).

Librealsense requires two external dependencies, GLFW3 (all platforms) and libusb-1.0 (Mac/Linux). These dependencies should be gathered through manual steps that are enumerated as part of this readme file (i.e. these packages must be installed with apt-get on Linux and Homebrew on OSX).

# Table of Contents
* [Compatible Devices](#compatible-devices)
* [Supported Platforms](#compatible-platforms)
* [Compatible Languages](#supported-languages-and-frameworks)
* [Functionality](#functionality)
* [Installation Guide](#installation-guide)
* [Hardware Requirements](#hardware-requirements)
* [Documentation](#documentation)

## Compatible Devices

1. RealSense R200
2. RealSense F200
3. RealSense SR300

## Compatible Platforms

librealsense is written in standards-conforming C++11 and relies only on the C89 ABI for its public interface. It is developed and tested on the following platforms:

1. Windows 8.1 (Visual Studio 2013 Update 5)
2. Ubuntu 14.04.03 LTS x64 (GCC 4.9 toolchain)
3. Mac OS X 10.7+ (Clang toolchain)

Neither libuvc nor V4L2 backends have been validated on Ubuntu 12.04 LTS or Ubuntu 15.10, and several attempts to bring cameras up on these platforms have been problematic due to the requirement of a patched uvcvideo driver. It may be possible to compile and run librealsense on other platforms. Please file an issue or submit a pull request if the library has been successfully ported to a platform.

## Supported Languages and Frameworks

1. C - Core library API exposed via the C89 ABI
2. C++ - Single header file (rs.hpp) wrapper around C API, providing classes and exceptions

## Functionality

1. Native streams: depth, color, infrared
2. Synthetic streams: rectified images, depth aligned to color and vice versa, etc.
3. Intrinsic/extrinsic calibration information
4. Majority of hardware-specific functionality for individual camera generations (UVC XU controls)
5. Multi-camera capture across heterogeneous camera architectures (e.g. mix R200 and F200 in same application) 

### Firmware Update

All RealSense™ cameras ship with proprietary firmware. This firmware is periodically updated with critical bugfixes, however librealsense does not currently provide functionality to upload new firmware. A supported update path is available on Windows 8.1 and Windows 10 systems via the [Intel® RealSense™ DCM](https://downloadcenter.intel.com/download/25044/Intel-RealSense-Depth-Camera-Manager-DCM-) (Depth Camera Manager). Installing the DCM on a supported machine with an attached camera will automatically flash the latest firmware released by Intel.

# Installation Guide

librealsense communicates with RealSense™ devices directly via the UVC and USB protocols. It does not link against the RealSense SDK™ runtime. Most of the library source code is platform agnostic, but there is a small UVC abstraction layer with platform-specific backends, including:
  * A video4linux2 backend which provides kernel-space access to UVC devices on Linux.
  * A libuvc backend which provides user-space access to UVC devices on Linux and Mac OS X (built with libusb).
  * A Windows Media Foundation backend which provides kernel-space access to UVC devices on Windows 8.1 and above.

**New Users:** A comprehensive installation guide is [available here](./doc/installation.md)

## Hardware Requirements
Developer kits containing the necessary hardware to use this library are available for purchase at [this link](http://click.intel.com/realsense.html). In addition, several consumer tablets and laptops with integrated cameras may also function, such as the [HP Spectre x2 with R200](http://store.hp.com/us/en/ContentView?storeId=10151&langId=-1&catalogId=10051&eSpotName=new-detachable).

Developer kits require USB 3.0. Not all USB host chipsets are compatible with librealsense, although it has been validated with recent generations of the Intel Host Controller chipset. An exhaustive list of incompatible hardware is not presently provided.

## Documentation

Formal documentation for librealsense is incomplete and may contain the occasional inaccuracy. Please send us feedback via the Github issue tracker about areas that are unclear or which need to be improved. 

A comprehensive suite of sample and tutorial applications are provided in the `/examples` subdirectory. For new users, it is best to review the tutorial series of apps which are designed to progressively introduce API features.

  * [Installation Instructions](./doc/installation.md) - Comprehensive platform-specific installation steps
  * [The librealsense C API](./include/librealsense/rs.h) - Doxygen style comments are provided for all functions, data types, and most constants
  * [Projection in librealsense](./doc/projection.md) - A guide on coordinate systems, calibration information, and projection APIs.
  * [Developer Notes](./doc/dev_log.md) - Several informal notes gathered during internal releases.

## License

Copyright 2015 Intel Corporation

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this project except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
