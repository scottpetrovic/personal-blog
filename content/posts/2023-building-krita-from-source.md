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
Before we can start any building or installing, our OS needs to have some tools and packages to build and work with code. 

Packages needed to get the cmake and compiler just buiding
    sudo apt install git cmake build-essential extra-cmake-modules

Packages needed for Qt frameowork:
    sudo apt install libkf5archive-dev libkf5completion-dev libkf5config-dev libkf5coreaddons-dev libkf5guiaddons-dev libkf5i18n-dev libkf5itemmodels-dev  libkf5itemviews-dev libkf5widgetsaddons-dev libkf5windowsystem-dev libkf5kiocore5 qtbase5-dev libqt5svg5-dev qtdeclarative5-dev libqt5x11extras5-dev libqt5opengl5-dev qtmultimedia5-dev qttools5-dev

Other packages:
    sudo apt install gettext libcurl4-gnutls-dev libtiff5-dev libjpeg-turbo8-dev libeigen3-dev libxi-dev libboost-all-dev libopenexr-dev libexiv2-dev  libgsl-dev liblcms2-dev libpoppler-qt5-dev shared-mime-info libraw-dev libfftw3-dev libopencolorio-dev vc-dev libpng-dev python3-sip-dev python3-pyqt5 pyqt5-dev libquazip5-dev libmypaint-dev freetype lib-freetype-dev libfontconfig1-dev



## Step 2: Start creating folders and download Krita source code

Create a folder where we will store everything. I have mine here:
~/git/krita

Open a terminal and navigate to the location above. Run this command 

    git clone https://invent.kde.org/graphics/krita.git

After it is done, I change the folder name from "krita" to "source" as that is more descriptive.
    mv krita source

Build out a few more folders. We will need them to build out everything needed for Krita:

krita folder
- build folder
- install folder
- source folder
- deps-build folder
- deps-download folder

So we will end up with 5 folders in the end inside the ~/git/krita folder


## Step 3: CMake configuration Part 1 - Dependencies

Move the command line current directory so you are in your "deps-build" folder.
   cd deps-build

Run this command to set a variable:
    BUILDROOT=~/git/krita

Then:
    cmake ../source/3rdparty -DINSTALL_ROOT=$BUILDROOT/install -DEXTERNALS_DOWNLOAD_DIR=$BUILDROOT/deps-download -DCMAKE_INSTALL_PREFIX=BUILDROOT/install


That sets up the cmake build settings. Now we need to actually build the dependencies like this:

cmake --build . --config RelWithDebInfo --target ext_lager

What this does is goes into our source files, looks at the library to build, builds it, then copies the files to the install folder. 

NOTE: ffmpeg is failing to build with error "No package metadata was found for meson". 


## Step 3.1 Building Dependency - HarfBuzz

You need a specific version of Harfbuzz...which is a lot newer than what is in ubuntu 20.04.

1. Download the 4.4.1 release from here (get the tar.xz archive and extrace it anywhere): https://github.com/harfbuzz/harfbuzz/releases/tag/4.4.1
2. Extract the folder in your downloads
3. Make a new folder called something like "harfbuzz-build". Open the termaimal up in this build folder
4. run the cmake command in it to get it ready: cmake -S ../harfbuzz-4.4.1 -B .
5. If all is good with that build it: sudo make install

We need the sudo...otherwise the terminal won't have access to copy the final files to the /usr/local/ folder.

If we go back to and try to build Krita, it should say Harfbuzz is found.


## Step 3.2 Building Dependency - Unibreak

https://github.com/adah1972/libunibreak/releases/tag/libunibreak_5_1




### Step 4: Building Krita

Go into the build directory. This where we will build Krita
    cd ~/git/krita/build

Run the following command. This will show us if we have everything we need to actually build Krita.
    cmake -DCMAKE_INSTALL_PREFIX=$HOME/git/krita/install $HOME/git/krita/source -DCMAKE_BUILD_TYPE=RelWithDebInfo -DBUILD_TESTING=OFF -DPYTHON_EXECUTABLE=/usr/bin/python3 -DPYQT_SIP_DIR_OVERRIDE=/usr/share/sip/PyQt5

There is pretty much a 100% chance this isn't going to go to completion when you first run in. What follows is probably the most difficult part of getting Krita with getting all the dependencies working.




