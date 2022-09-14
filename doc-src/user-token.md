# User Token

User token verifies the current status of Spacelord hub
and hands over space configuration
and user secrets (e.g., LUKS password)
once the hub's identity and the integrity are verified.

User token can be downloaded at `token`
which is a static Linux binary.
Please add the execution permission (`chmod +x ./token`) after downloading it.

## User OS Image

Spacelord compatible user OS images establish a connection with the user token after booting the kernel.
After the identity and the integrity of the board is confirmed by the user token,
the user token sends over the user secrets that are required to decrypt the user layer.

Sample user OS image for each board can be downloaded at the following locations.
Decompress the downloaded image **and keep the original `.lz4` file**.

- RockPro64: `os-images/rockPro64-user.img.lz4`
- iMX8MQ: `os-images/imx8mq-evk-user.img.lz4`
- QEMU (for artifact evaluation without hardware): `hub_images/qemu-user.img.lz4`
