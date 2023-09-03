---
title: "2023 Building Krita from Source on Ubuntu"
date: "2023-09-02"
draft: true
---

## Step 0: OS
We need to currently use Ubuntu 20.04. One of the big reasons is that the Python version that Krita uses is 3.8. It needs to be that exact version, otherwise there are issues building dependencies. The OS itself has a dependency on a specific version of Python. Changing the Python version could also likely destroy the OS. 

You can get the Ubuntu 20.04 (Focal Fossa) image here:
https://releases.ubuntu.com/focal/

Windows: You can use the program "Rufus" to burn the ISO to a USB for installing
Ubuntu: You can use the program "Startup Disk Creator" to burn the USB for installing

## Step 1: OS packages for building
Before we can start any building or installing, our OS needs to have some tools to build and work with code. This is the command I use to install everything as a base.

sudo apt install build-essential libcurl4-gnutls-dev libtiff5-dev libjpeg-turbo8-dev gettext cmake git extra-cmake-modules libkf5archive-dev libkf5completion-dev libkf5config-dev libkf5coreaddons-dev libkf5guiaddons-dev libkf5i18n-dev libkf5itemmodels-dev  libkf5itemviews-dev libkf5widgetsaddons-dev libkf5windowsystem-dev libkf5kiocore5 qtbase5-dev libqt5svg5-dev qtdeclarative5-dev libqt5x11extras5-dev libqt5opengl5-dev libeigen3-dev libxi-dev libboost-all-dev libopenexr-dev libexiv2-dev  libgsl-dev liblcms2-dev libpoppler-qt5-dev shared-mime-info libraw-dev libfftw3-dev libopencolorio-dev vc-dev qtmultimedia5-dev libpng-dev python3-sip-dev python3-pyqt5 pyqt5-dev qttools5-dev libquazip5-dev libmypaint-dev


## Step 2: Start creating folders and download Krita source code

Create a new folder structure that looks like this:

kritadev folder
- build folder
- install folder
- source folder
- b folder
- d folder


So we have created 4 folders. Three of the folders are inside the kritadev folder. Next, grab the source code from your git fork. Navigate to your kritadev folder in the command line. Run this command 

git clone https://invent.kde.org/scottpetrovic/krita

After it is done, I change the folder name from "krita" to "source" as that is more descriptive.


## Step 3: Using Python 3.8
By default Ubuntu 23.04 uses Python 3.11. This is too new. Certain things won't work with this version like building the ffmpeg library. 


## Step 3: CMake configuration Part 1 - Dependencies

Move the command line current directory so you are in your "b" folder.

BUILDROOT=~/kritadev

Then:

cmake ../source/3rdparty \
        -DINSTALL_ROOT=$BUILDROOT/install \
        -DEXTERNALS_DOWNLOAD_DIR=$BUILDROOT/d \
        -DCMAKE_INSTALL_PREFIX=BUILDROOT/install


That sets up the cmake build settings. Now we need to actually build the dependencies like this:

cmake --build . --config RelWithDebInfo --target ext_lager
cmake --build . --config RelWithDebInfo --target ext_ffmpeg


NOTE: ffmpeg is failing to build with error "No package metadata was found for meson". 


