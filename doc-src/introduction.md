# Introduction

This repository contains artifact evaluation guide for
ACSAC'22 submission
*SPACELORD: Private and Secure Smart Space Sharing*.

The Spacelord artifacts can be broadly separated into four categories:

1. Hub image (4.3)
    * This is a disk image uploaded to the board.
      It contains Spacelord bootloader, image downloader,
      and the signature generator.
2. User token and OS image (4.2, 4.4, 4.5)
    * User token communicates with Spacelord bootloader to upload user image
      after verifying the identity of the hub.
    * We provide reference implementation of user token as a Linux userspace program.
3. Peripheral image (4.6)
    * Reference implementation of Spacelord protocol on ESP32-based camera device.
4. Image and storage server

All artifacts can be downloaded at this [OneDrive link](https://1drv.ms/u/s!Apa8Zxdex5yci51AXOjjKVZ6cbgTRA?e=3ec1mX).

*Note:* "Sledgehammer" is the old codename for this project and may appear in some of the artifacts.
