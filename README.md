# gsmartcontrol-pop22.04-nvme
A custom build of gsmartcontrol 2.0.1 with NVMe support, using smartmontools 7.4, specifically for Pop!_OS 22.04. This version enables NVMe drive support, which is missing in the default build for Pop!_OS.

This repository contains a custom build of gsmartcontrol with smartmontools version 7.4 for Pop!_OS 22.04. The default version of smartmontools on Pop!_OS 22.04 is outdated (7.2 from 2020), and this build upgrades it to the latest release, enabling compatibility with newer hardware and features.



## Installation Steps

1. Install Dependencies
```
sudo apt update
sudo apt install -y build-essential g++-11 libglibmm-2.4-dev libgtkmm-3.0-dev \
libsigc++-2.0-dev libatkmm-1.6-dev libpangomm-1.4-dev \
libcairomm-1.0-dev libudev-dev gettext autopoint \
libx11-dev libatasmart-dev git
```

or

```
sudo apt update
sudo apt install -y build-essential automake autoconf libtool pkg-config libgtk-3-dev libglib2.0-dev libudev-dev libpci-dev libboost-system-dev libboost-filesystem-dev libboost-program-options-dev g++ gcc libglibmm-2.4-dev libgtkmm-3.0-dev libsigc++-2.0-dev libatkmm-1.6-dev libpangomm-1.4-dev libcairomm-1.0-dev libx11-dev libatasmart-dev git autopoint libwxgtk3.0-gtk3-dev
```

2. Clone the Latest GSmartControl Git Repository
   
```
git clone https://github.com/ashaduri/gsmartcontrol.git
cd gsmartcontrol
```
If you already cloned it before and want to update to the latest version:

```
cd gsmartcontrol
git pull
```

3. Configure and Compile with GCC 11 (Set the compiler version:)
```
export CXX=g++-11
export CC=gcc-11
```

4. CMake command
```
cmake .. -DCMAKE_C_COMPILER=gcc-11 -DCMAKE_CXX_COMPILER=g++-11 -G "Unix Makefiles"
```

5. Proceed with building GSmartControl by running:
```
make -j$(nproc)
```

6. You can test running GSmartControl with:
```
./gsmartcontrol
```

7. Install the Compiled Version system-wide
```
sudo make install
```

8. To verify the installation:
```
gsmartcontrol --version
```

9. Cleanup
If you want to remove the compiled files but keep the source code:
```
make clean
```
To remove everything and start fresh:
```
git clean -xdf
```


## Incompatible smartctl version
If you're encountering  this error your system may not be compatible with the version expected by gsmartcontrol 2.0.1.

Run the following command to verify the version of smartctl:
```
smartctl --version
```

10. To install smartmontools 7.4 from source. Download and extract the source code.
```
wget https://sourceforge.net/projects/smartmontools/files/smartmontools/7.4/smartmontools-7.4.tar.gz
tar -xvzf smartmontools-7.4.tar.gz
cd smartmontools-7.4
```

11. Build the source:
```
./configure
make
sudo make install
```
12. Once that's done, verify that the new version of smartctl is installed:
```
smartctl --version
```

   

Credits

    gsmartcontrol: https://github.com/AdvancesInTech/gsmartcontrol
    smartmontools: https://github.com/smartmontools/smartmontools
