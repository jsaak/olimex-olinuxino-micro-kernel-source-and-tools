# Kernel source and build tools for Olimex A20 (OLINUXINO-MICRO)

This is a copy of the linux kernel source hacked by sunxi, based on 3.4.103, and gcc to cross-compile.

Since this [description](https://github.com/OLIMEX/OLINUXINO/blob/master/SOFTWARE/A20/A20-build-3.4.103-release-5/BUILD_DESCRIPTION_A20_Olimex_kernel_3.4.103%2B_Jessie_rel_5.txt)
how to compile a kernel is out of date, i packaged all together.

## Included

- Kernel source copied from linux-sunxi 3.4 branch [here](https://github.com/linux-sunxi/linux-sunxi) (commit: d47d367036be38c5180632ec8a3ad169a4593a88)

- The "official" kernel [config](https://raw.githubusercontent.com/OLIMEX/OLINUXINO/master/SOFTWARE/A20/A20-build-3.4.103-release-5/A20-linux-3.4.103_defconfig)

- Linaro gcc for crosscompiling (gcc-linaro-arm-linux-gnueabihf-4.7-2013.01-20130125_linux)

- Two patches from mainline to support ZYTRONIC touch devices.
[HID: hid-multitouch: fix input mode feature command](https://github.com/torvalds/linux/commit/4aceed37e315e8eaa26cb4c8dfd619a32fa24669#diff-e4d9a493d18920ce5c016041e772f99e)
[HID: hid-multitouch: add support for Zytronic panels](https://github.com/torvalds/linux/commit/82d069822feaf9bf7eb85d5c9ba9a123ecc8f15f#diff-e4d9a493d18920ce5c016041e772f99e)
(MT_USB_DEVICE is back renamed to HID_USB_DEVICE)

- a20-emmc_2.patch applied

- instructions how to mount the boot partition from dd image based on this [stackexchange answer](https://raspberrypi.stackexchange.com/questions/13137/how-can-i-mount-a-raspberry-pi-linux-distro-image)
```
mount -v -o offset=17825792 -t ext3 olimex_backup_20171010 /mnt/image
```

## Dependencies

mkimage executable from u-boot-tools

```
sudo apt-get install u-boot-tools
```

## How to use

```
source set-gcc.sh
cd linux-sunxi-sunxi-3.4
```
continue according to [description](https://github.com/OLIMEX/OLINUXINO/blob/master/SOFTWARE/A20/A20-build-3.4.103-release-5/BUILD_DESCRIPTION_A20_Olimex_kernel_3.4.103%2B_Jessie_rel_5.txt)

```
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- -j4 uImage
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- -j4 INSTALL_MOD_PATH=out modules
```

to make debian pckages (for getting headers for example)

```
KBUILD_DEBARCH=armhf make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- deb-pkg
```
