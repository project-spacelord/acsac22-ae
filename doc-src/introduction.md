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

TODO: Mention paper's chapters where possible
