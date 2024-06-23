# Game and Watch flash Guide

IMPORTANT NOTICE:

 - Don't use newer OS like fedora 39 or something else. It turned out to have
   issues with stlink communications. Try ubuntu 18 or 20 and they would be more
   reliable.
 - Only connect SWDIO, SWCLK, GND to stlink.

## Debugger Connections

![68747470733a2f2f7261772e67697468756275736572636f6e74656e742e636f6d2f427269616e507567682f676e776d616e616765722f6d61696e2f6173736574732f73746c696e6b76322e706e67](https://github.com/cysin/openocd-gw/assets/209019/0cde8b0f-c242-4cf0-84b2-6524ede30a7e)


## Install patched openocd

 1. If you are on ubuntu just follow https://github.com/kbeckmann/ubuntu-openocd-git-builder
 2. Or checkout this repo:

		git clone --recurse-submodules https://github.com/cysin/openocd-gw.git
		sudo dnf install libtool
		sudo dnf install libusb1-devel
		sudo dnf install hidapi-devel
		sudo dnf install libftdi-devel
		./bootstrap
		./configure --prefix=/opt/openocd-git --enable-maintainer-mode --disable-werror --enable-dummy --enable-rshim --enable-ftdi --enable-stlink --enable-ti-icdi --enable-ulink --enable-usb-blaster-2 --enable-ft232r --enable-vsllink --enable-xds110 --enable-cmsis-dap-v2 --enable-osbdm --enable-opendous --enable-armjtagew --enable-rlink --enable-usbprog --enable-esp-usb-jtag --enable-cmsis-dap --enable-nulink --enable-kitprog --enable-usb-blaster --enable-presto --enable-openjtag --enable-buspirate --enable-jlink --enable-parport --disable-parport-ppdev --enable-parport-giveio --enable-jtag_vpi --enable-vdebug --enable-jtag_dpi --enable-amtjtagaccel --enable-bcm2835gpio  --enable-imx_gpio --enable-am335xgpio --enable-ep93xx --enable-at91rm9200 --enable-gw16012 --enable-sysfsgpio --enable-xlnx-pcie-xvc --enable-jimtcl-maintainer --enable-internal-libjaylink --enable-remote-bitbang

	and
	
		export OPENOCD="/opt/openocd-git/bin/openocd"

## Install GCC

 1. Use package manager to install arm gcc toolchain
 2. Download [arm-gcc-none-eabi toolchain](https://developer.arm.com/tools-and-software/open-source-software/developer-tools/gnu-toolchain/gnu-rm/downloads) or  https://developer.arm.com/downloads/-/gnu-rm
 3. unpack and set env variable:
    
   		export GCC_PATH='/home/user/gcc-arm-none-eabi-10.3-2021.10/bin/'

## Backup and unlock

 1. Follow https://github.com/ghidraninja/game-and-watch-backup
 2. Make sure you have got all the dumps correctly
 3. If you have problems while flashing cfw, just run step 5 to restore firmware and try again

## Install retro game

 1. Follow https://github.com/sylverb/game-and-watch-retro-go
 2. Copy roms to 'roms' directory
 3. Run

	    make romdef
	    make -j8 EXTFLASH_SIZE_MB=12 EXTFLASH_OFFSET=4194304 INTFLASH_BANK=2 GNW_TARGET=zelda flash

## Make Patch

 - Follow https://github.com/BrianPugh/game-and-watch-patch
 - Copy dumped bin files to this repo
 - Run

	    make PATCH_PARAMS="--device=zelda" flash
## Useful Links

 - https://www.reddit.com/r/GameAndWatchMods/comments/mr8hxs/click_here_for_links/
 - https://www.reddit.com/r/GameAndWatchMods/wiki/index/
 - https://www.reddit.com/r/GameAndWatchMods/wiki/flash-upgrade/

