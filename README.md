# Custom FFmpeg Static Auto-Builds

This Repository is built by slightly modifying code provided by https://github.com/BtbN/FFmpeg-Builds to meet our needs. All rights and licenses are reserved to their respective owners.

## Auto-Builds

Builds run monthly on 25th at 12:00 UTC (or GitHubs idea of that time) and are automatically released on success.

**Auto-Builds run ONLY for win32 & win64. There are no linux or linux-arm auto-builds, though you can produce builds yourself following the instructions below.**


## Package List

For a list of included dependencies check the scripts.d directory.
Every file corresponds to its respective package.

## How to make a build

### Prerequisites

* bash
* docker

### Build Image

* `./makeimage.sh target variant [addins]`

### Build FFmpeg

* `./build.sh target variant [addins]`

On success, the resulting zip file will be in the `artifacts` subdir.

### Targets, Variants and Addins

Available targets:
* `win64` (x86_64 Windows)
* `win32` (x86 Windows)
* `linux64` (x86_64 Linux, glibc>=2.23, linux>=4.4)
* `linuxarm64` (arm64 (aarch64) Linux, glibc>=2.27, linux>=4.15)

The linuxarm64 target will not build some dependencies due to lack of arm64 (aarch64) architecture support or cross-compiling restrictions.

* `davs2` and `xavs2`: aarch64 support is broken.
* `libmfx` and `libva`: Library for Intel QSV, so there is no aarch64 support.

Available:
* `gpl` Includes all dependencies, even those that require full GPL instead of just LGPL.
* `lgpl` Lacking libraries that are GPL-only. Most prominently libx264 and libx265.
* `nonfree` Includes fdk-aac in addition to all the dependencies of the gpl variant.
* `gpl-shared` Same as gpl, but comes with the libav* family of shared libs instead of pure static executables.
* `lgpl-shared` Same again, but with the lgpl set of dependencies.
* `nonfree-shared` Same again, but with the nonfree set of dependencies.

All of those can be optionally combined with any combination of addins.
* `4.4` to build from the 4.4 release branch instead of master.
* `5.0` to build from the 5.0 release branch instead of master.
* `debug` to not strip debug symbols from the binaries. This increases the output size by about 250MB.
