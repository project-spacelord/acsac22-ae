# Spacelord peripheral devices

A prototype implementation of Spacelord peripheral device that targets ESP-EYE board
can be downloaded at `peripheral` directory.

- `peripheral/secure-hub-peripheral.elf`
- `peripheral/bootloader.bin`
- `peripheral/partition-table.bin`

Please check "Build the Project" section in Esperiff documentation
to see how to flash these files to the board.

- [Linux and macOS](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/linux-macos-setup.html#build-the-project)
- [Windows](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/windows-setup.html#build-the-project)

The board communicates with the board through Wi-Fi,
and the prototype used hardcoded Wi-Fi SSID and password.
Please test in the environment where a Wi-Fi with SSID "myssid" and password "mypassword" (without quote, WPA2).
Alternatively, we can provide a binary with alternative SSID/PW upon a reviewer's request.

TODO: check if this is correct SSID/PW

## Minimal hub implementation

The above camera implementation is intended to communicate with OpenHAB hub software through HTTPS protocol (REST).
Both side (the hub and the peripheral) must use TLS client authentication to verify the identity of each other.
To reduce the hassle of setting up a patched OpenHAB,
we provide a CLI program written in Rust that performs the Sledgehammer TLS authentication.

- Use `peripheral/hub-x86` to perform peripheral test on a laptop
- Use `peripheral/hub-aarch64` to perform peripheral test with a Spacelord board
