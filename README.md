# How to install 64-bit Linux on an iMac 24" (late 2006)

This repo describes my experience in installing a 64-bit Linux distro on an old iMac 24" (late 2006) with the following specs:
* [Intel Core 2 Duo Processor T7400](https://www.intel.com/content/www/us/en/products/sku/27256/intel-core2-duo-processor-t7400-4m-cache-2-16-ghz-667-mhz-fsb/specifications.html) @ 2.16 GHz, supporting a 64-bit instruction set
* 3 GB of RAM (specifically DDR2 SDRAM, 667 MHz, PC2-5300), upgraded with a [Kingston KVR667D2S5/2G](https://www.kingston.com/en/memory/search/discontinuedmodels?partid=KVR667D2S5%2F2G)
* 120 GB SSD, by replacing the original HDD with a [Kingston SV300S3B7A/120G](https://www.kingston.com/en/memory/search/discontinuedmodels?partid=SV300S3B7A%2F120G), including a 2.5" to 3.5" adapter
* NVIDIA GeForce 7600 GT graphics card

## OS image

Despite all my attempts to boot from a USB drive, I could only boot externally from the CD/DVD drive. Therefore, any installation image must be burned to a CD/DVD. However, burning an installation image from any modern 64-bit distro is useless, as it simply won't boot, getting stuck on "Select CD-ROM Boot Type".

To overcome this problem, I used [Matt Gadient's approach](https://mattgadient.com/linux-dvd-images-and-how-to-for-32-bit-efi-macs-late-2006-models/) of modifying the 64-bit image to make it bootable on a machine with 32-bit EFI, as is the case with this iMac. Basically, this consists in compiling and running `isomacprog.c` on the 64-bit ISO image that you would like to use. The commands are:
* To compile: `cc -g -Wall isomacprog.c -o isomacprog`
* To run: `./isomacprog your-preferred-64-bit-image.iso`.

## Xubuntu

After downloading an installation image for [Ubuntu 22.04 LTS](https://ubuntu.com/download/desktop) and modifying it by running `isomacprog`, I was in for a surprise. The image was 5 GB, but my DVDs were 4.7 GB capacity. On the other hand, I thought that mainstream Ubuntu, with the GNOME desktop environment, was probably too much for this machine. (A previous experiment with [Debian i386](https://www.debian.org/distrib/netinst) and GNOME made me feel so.)

Therefore, I opted for [Xubuntu 22.04 LTS](https://xubuntu.org/download/), whose installation image of about 3 GB was easier to download, modify, and burn into a DVD.

## WiFi card

After installing Xubuntu, almost everything worked out of the box (including brightness control, which didn't work on Debian). However, there were some final touches that needed to be done. One of them was the WiFi adapter. For this to work, I had to `sudo apt install firmware-b43-installer` (rather than `bcmwl-kernel-source`, which apparently worked, but provided no network connectivity).

## iSight camera

Another thing that needed to be set up was the built-in camera. For this, I used [Jarret B's approach](https://www.linux.org/threads/installing-linux-on-an-imac.26009/) of installing `isight-firmware-tools` and providing the path to `AppleUSBVideoSupport`. The command is `sudo apt install isight-firmware-tools` and then, during installation, specify the path to the downloaded `AppleUSBVideoSupport` file, for it to extract the camera firmware. Reboot and _voilà_!

## Wrapping up

That's it! I've got an old iMac running a modern 64-bit Xubuntu, where I can install software such as [Chrome](https://www.google.com/chrome/?platform=linux), [Zoom](https://zoom.us/download?os=linux), [VSCode](https://code.visualstudio.com/), etc. For Chrome and VSCode to work properly, I had to disable hardware acceleration, since this was buggy with the old graphics card.