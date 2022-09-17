# Testing

## Spacelord authorized boot testing

Make sure to download artifacts listed in the [introduction page](introduction.md)
based on your hardware requirement.

### Preconfiguration

1. Run the image server
    * Run your favorite HTTP static file server
      (e.g., [static-web-server](https://github.com/joseluisq/static-web-server),
[Python SimpleHTTPServer](https://www.digitalocean.com/community/tutorials/python-simplehttpserver-http-server))
      at the location where lz4 compressed user images are stored.
2. Run the storage server
    * Follow the guide in the [server setup guide page](server.md)
      to run the storage server in QEMU.
3. Edit `config.toml` based on the location of the image server and the web server.
    `server.IMAGE_SERVER_URL` should point to the image server including the protocol and the port number
    (e.g., `http://localhost:8080/`).
    `server.wireguard.ISCSI_TARGET_IP` should point to the IP
    where the storage server is running without the port number
    (e.g., `127.0.0.1`).
    `WG_LISTEN_PORT_LOCAL` and `WG_LISTEN_PORT` (as well as `run-qemu.sh` and `run-storage-server.sh`)
    might have to be changed if the host machine uses these port numbers for other purposes.
    All the other settings are hardcoded in the provided storage server image,
    so reviewers do not need to modify them (e.g., wireguard subnet IPs).
4. Put `config.toml` at the same directory with `token` program.
5. Flash the hub image to the board or prepare the QEMU image.

### Sledgehammer boot testing

1. Turn on the hub board
    * Connect the board to the ethernet and turn it on.
      The board will boot into the hub manager
      and print a message:
      `Please connect to <your_ip>`.
      Remember this IP address.
    * For QEMU-based testing, use `run-qemu.sh` script.
      The provided script forward internal ports outside,
      so use the host's IP number instead of the printed one
      in the following steps.
          * We used Ubuntu 18.04 server and qemu-system-aarch64 2.11.1 during testing.
2. Run user token program
    * Run user token with the following command:
      `./token <hub_ip> <os_image>`.
    * The local image name and the name on the image server should match.
      Specifically, the hub program looks up `${LOCAL_IMAGE_DIR}/${IMAGE_NAME}`,
      and the hub downloads the image from `${IMAGE_SERVER_URL}/${IMAGE_NAME}.lz4`.
    * The token program will connect to the hub manager
      (through port number 15758),
      sends the location of the image server,
      and chooses a nonce for this communication session.
    * If the communication is successful,
      the hub downloads the image and reboots,
      and the token program will proceed to the next phase.
3. Wait for the authenticated boot
    * When the board reboots,
      the bootloader calculates the hash of the downloaded image
      and generates a certificate based on the measurement result and the nonce.
    * Concurrently, the token program calculates the expected hash of the user image.
      When the hashing is done, the token program waits in a loop
      and prints "Waiting for the authenticator..." message until the hub is ready.
    * When the both parts finish their work,
      the board boots into the user OS image and runs the agent application
      that performs authenticated key exchange with the user token.
      The reference implementation uses TLS client authentication (port number 15759).
    * If the authentication succeeds,
      the user token sends user credentials that are necessary to mount the user layer.
4. User layer mount
    * As the last step, the user layer is mounted with the credential provided from the user token.
    * When everything is done, the Linux-based user OS image will launch.

## Peripheral testing

1. Setup ESP-EYE device based on the instruction at [peripheral setup guide](peripheral.md).
2. Run the sample hub binary
    * `./hub-x86_64 <peripheral_ip>` or `./hub-aarch64 <peripheral_ip>`
    * The hub binary prints CLI menu that can interact with the peripheral.
      Internally, both side use TLS client authentication to ensure their identity.

## Performance testing

Download `eval-scripts/phoronix_install_script.sh` and `eval-scripts/phoronix_run_tests.sh`
and upload them to the board after the board boots up.
Run them in the provisioned board to reproduce the performance evaluation in section 6.1.
