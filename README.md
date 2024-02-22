# How to install a 64-bit Linux distro on an iMac 24" (late 2006)

This repo describes my experience in successfully installing a 64-bit Linux distro on an old iMac 24" (late 2006) with the following specs:
* [Intel Core 2 Duo Processor T7400 @ 2.16 GHz](https://www.intel.com/content/www/us/en/products/sku/27256/intel-core2-duo-processor-t7400-4m-cache-2-16-ghz-667-mhz-fsb/specifications.html)
* 3GB of RAM (specifically DDR2 SDRAM, 667 MHz, PC2-5300) upgraded with a [Kingston KVR667D2S5/2G](https://www.kingston.com/en/memory/search/discontinuedmodels?partid=KVR667D2S5%2F2G)
* 120 GB SSD replacing the original HDD by a [Kingston SV300S3B7A/120G](https://www.kingston.com/en/memory/search/discontinuedmodels?partid=SV300S3B7A%2F120G) including a 2.5" to 3.5" adapter

## Installing the OS

Despite all my attempts to boot from a USB drive, I could only boot the system from the CD/DVD drive. Therefore, any installation image must be burned to a CD/DVD. In addition, burning an installation image from any modern 64-bit distro is useless, it simply won't boot, it gets stuck on "Select CD-ROM Boot Type".

To overcome this problem, use [Matt Gadient's approach](https://mattgadient.com/linux-dvd-images-and-how-to-for-32-bit-efi-macs-late-2006-models/) to modify the 64-bit image to make it bootable on a machine with 32-bit EFI. Basically, this consists in compiling and running `isomacprog.c` on the 64-bit ISO image that you would like to use. The commands are `cc -g -Wall isomacprog.c -o isomacprog` and `./isomacprog your-preferred-image.iso`.









