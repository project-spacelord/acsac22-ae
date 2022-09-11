# Testing

## Functionality Testing

Make sure you have downloaded artifacts listed in the [Introduction](/introduction.html).

TODO: provide downloader script

1. Boot the board
    * Connect the board to the ethernet and turn it on.
      The board will boot into the hub manager
      and print a message:
      `Please connect to <your_ip>`
    * For QEMU-based testing,
      use script XXX.
      TODO: provide QEMU launch script.
2. Run user token
    * Run user token with the following command:
      `./token <printed_ip> <expected_os_image>`
    * User token reads configuration from `config.toml` file.
      TODO: Should we ask reviewers to run their own server?
    * The token program connects to the hub manager
      (port number 15758)
      and informs it where it can download the base image (system + hardware layer).
      It also chooses a nonce for this session.
      * This configuration comes from `IMAGE_SERVER_URL` field.
3. Authenticated boot
    * The hub manager downloads the base image and reboots into the bootloader.
      The bootloader calculates the hash of the downloaded image
      and generates a certificate based on the measurement result and the nonce.
    * Concurrently, the token program calculates the expected hash.
    * When the both parts finishes their work,
      the board boots into the device image and runs the agent application
      that performs authenticated key exchange with the user token.
      The reference implementation uses TLS handshake with client auth (port number 15759).
    * If the authentication succeeds,
      the user token sends user credentials that are necessary to mount the user layer.
4. User layer mount
    * As the last step, the user layer is mounted and the board is ready to be used.

TODO: Config migration - @Marcus?

## Performance Testing

TODO: @Sabartha
