# Hub Image

- RockPro64: `hub-images/rockpro64-downloader.img`
- iMX8MQ: `hub-images/imx8mq-evk-downloader.img`
- QEMU (for artifact evaluation without hardware): `qemu-testing/qemu-downloader.img` and `qemu-testing/run-qemu.sh`.

For hardware based evaluation,
the target board, an NVME SSD, and an eMMC card are required.
Download the corresponding hub image
and upload the image to the eMMC card with a disk flashing tool
(e.g., Etcher, dd - [example](https://wiki.radxa.com/Rockpi4/install/eMMC)).

To minimize the hardware requirement,
we disabled TPM requirement for RockPro64 hub image.
TPM requirement do not affect the system performance
because TPM is only used to store secret keys at the boot stage.
