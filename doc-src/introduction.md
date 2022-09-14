# Introduction

This repository contains artifact evaluation guide for
ACSAC'22 submission
*SPACELORD: Private and Secure Smart Space Sharing*.

The Spacelord artifact submission consists of four components:

1. Hub image
    * This is a disk image uploaded to the board.
      It contains Spacelord bootloader, image downloader,
      and the signature generator.
2. User token and OS image
    * User token communicates with Spacelord bootloader to upload user image
      after verifying the identity of the hub.
    * We provide reference implementation of user token as a Linux userspace program.
3. Peripheral image
    * Reference implementation of Spacelord protocol on ESP32-based camera device.
4. Web server
    * A web server that stores encrypted user files.

All artifacts can be downloaded at this [OneDrive link](https://1drv.ms/u/s!Apa8Zxdex5yci51ALONC_FURN_GnNw?e=No9NnK).

*Note:* "Sledgehammer" is the old codename for this project and may appear in some of the artifacts.

TODO: make this link read-only

TODO: mention paper chapters for each component
