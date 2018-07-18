# plutosdr-fw
PlutoSDR Firmware for the [ADALM-PLUTO](https://wiki.analog.com/university/tools/pluto "PlutoSDR Wiki Page") Active Learning Module

Latest binary Release : [![GitHub release](https://img.shields.io/github/release/analogdevicesinc/plutosdr-fw.svg)](https://github.com/analogdevicesinc/plutosdr-fw/releases/latest)

[Instructions from the Wiki: Building the image](https://wiki.analog.com/university/tools/pluto/building_the_image)

* Build Instructions
 ```bash
      sudo apt-get install git build-essential fakeroot libncurses5-dev libssl-dev ccache 
      sudo apt-get install dfu-util u-boot-tools device-tree-compiler libssl1.0-dev mtools
      git clone --recursive https://github.com/epiqsolutions/plutosdr-fw.git
      cd plutosdr-fw
      export CROSS_COMPILE=arm-xilinx-linux-gnueabi-
      export PATH=$PATH:/opt/Xilinx/SDK/2016.2/gnu/arm/lin/bin:/opt/Xilinx/SDK/2016.2/bin
      export VIVADO_SETTINGS=/opt/Xilinx/Vivado/2017.4/settings64.sh
      make TARGET=sidekiqz2
 
 ```
   
 * Updating your local repository 
 ```bash 
      git pull
      git submodule update --init --recursive
 ```
   
* Build Artifacts
 ```bash
      user@dev-machine:~/devel/plutosdr-fw$ ls -AGhl build
	total 55M
        -rw-rw-r-- 1 user   69 May 29 12:46 boot.bif
        -rw-rw-r-- 1 user 446K May 29 12:46 boot.bin
        -rw-rw-r-- 1 user 446K May 29 12:46 boot.dfu
        -rw-rw-r-- 1 user 575K May 29 12:46 boot.frm
        -rw-r--r-- 1 user 5.3M May 29 12:45 rootfs.cpio.gz
        drwxrwxr-x 6 user 4.0K May 29 12:45 sdk
        -rw-rw-r-- 1 user 9.4M May 29 12:46 sidekiqz2.dfu
        -rw-rw-r-- 1 user 9.4M May 29 12:46 sidekiqz2.frm
        -rw-rw-r-- 1 user   33 May 29 12:46 sidekiqz2.frm.md5
        -rw-rw-r-- 1 user 9.4M May 29 12:46 sidekiqz2.itb
        -rw-rw-r-- 1 user  18M May 29 12:46 sidekiqz2-fw-v0.28-12-g1017.zip
        -rw-rw-r-- 1 user 470K May 29 12:46 sidekiqz2-jtag-bootstrap-v0.28-12-g1017.zip
        -rw-rw-r-- 1 user 943K May 29 12:46 system_top.bit
        -rw-rw-r-- 1 user 670K May 29 12:45 system_top.hdf
        -rwxrwxr-x 1 user 409K May 29 12:46 u-boot.elf
        -rw-rw---- 1 user 128K May 29 12:46 uboot-env.bin
        -rw-rw---- 1 user 129K May 29 12:46 uboot-env.dfu
        -rw-rw-r-- 1 user 4.7K May 29 12:46 uboot-env.txt
        -rwxrwxr-x 1 user 3.2M May 29 12:44 zImage
        -rw-rw-r-- 1 user  21K May 29 12:45 zynq-sidekiqz2-revb.dtb
 ```
 
 * Main targets
 
     | File  | Comment |
     | ------------- | ------------- | 
     | sidekiqz2.frm | Main Sidekiq Z2 firmware file used with the USB Mass Storage Device |
     | sidekiqz2.dfu | Main Sidekiq Z2 firmware file used in DFU mode |
     | boot.frm  | First and Second Stage Bootloader (u-boot + fsbl + uEnv) used with the USB Mass Storage Device |
     | boot.dfu  | First and Second Stage Bootloader (u-boot + fsbl) used in DFU mode |
     | uboot-env.dfu  | u-boot default environment used in DFU mode |
     | sidekiqz2-fw-vX.XX.zip  | ZIP archive containg all of the files above |
     | sidekiqz2-jtag-bootstrap-vX.XX.zip  | ZIP archive containg u-boot and Vivao TCL used for JTAG bootstrapping |
 
  * Other intermediate targets

     | File  | Comment |
     | ------------- | ------------- |
     | boot.bif | Boot Image Format file used to generate the Boot Image |
     | boot.bin | Final Boot Image |
     | sidekiqz2.frm.md5 | md5sum of the sidekiqz2.frm file |
     | sidekiqz2.itb | u-boot Flattened Image Tree |
     | rootfs.cpio.gz | The Root Filesystem archive |
     | sdk | Vivado/XSDK Build folder including  the FSBL |
     | system_top.bit | FPGA Bitstream (from HDF) |
     | system_top.hdf | FPGA Hardware Description  File exported by Vivado |
     | u-boot.elf | u-boot ELF Binary |
     | uboot-env.bin | u-boot default environment in binary format created form uboot-env.txt |
     | uboot-env.txt | u-boot default environment in human readable text format |
     | zImage | Compressed Linux Kernel Image |
     | zynq-sidekiqz2-sdr-revb.dtb | Device Tree Blob for Rev.B |

