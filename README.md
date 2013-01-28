rk3066-kernel
=============

Linux/Android kernel for the Rockchip RK3066 SoC

How to bake it for mk808
========================

* `sudo apt-get install libusb-dev`
* `git clone https://github.com/gefire/mk808-tools`
* `cd mk808-tools; make`
* `gcc -o rkflashtool rkflashtool.c -lusb-1.0 -O2 -W -Wall -s`
* `gcc -o rkcrc rkcrc.c -O2 -W -Wall -s`
* `sudo cp -rf rkcrc rkflashtool /usr/local/bin/`
* `cd rk3066-kernel`
* `make -j 4 CROSS_COMPILE=arm-linux-gnueabihf- zImage`
* `cp -rf arch/arm/boot/zImage .`
* `rkcrc -k zImage zImage.img`
* `sudo rkflashtool w 0x00004000 0x00004000 < zImage.img`