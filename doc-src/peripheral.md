# Spacelord peripheral devices

A prototype implementation of a Spacelord peripheral device that targets the [ESP-EYE](https://www.espressif.com/en/products/devkits/esp-eye/overview) board
can be downloaded from the `peripheral` directory.

- `peripheral/secure-hub-peripheral.elf`
- `peripheral/bootloader.bin`
- `peripheral/partition-table.bin`

Please install the Espressif ESP-IDF and tools following the instructions from these links.

- [Linux and macOS](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/linux-macos-setup.html#build-the-project)
- [Windows](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/windows-setup.html#build-the-project)

Connect the ESP32 board to the test computer via USB cable. This should produce a serial port on the test machine. Find out the name of the serial port based on your operating system. For example, on Windows, the ESP32 board should appear in Device Manager under `Ports (COM & LPT)' as a COM port. On Linux, it should appear under /dev/ttyUSB*. With the three .bin files from the OneDrive peripheral directory in the same directory as the command line, run 

> python <Espressif-path>\frameworks\esp-idf-v5.0\components\esptool_py\esptool\esptool.py -p <ESP32 serial port> -b 460800 --before default_reset --after hard_reset --chip esp32  write_flash --flash_mode dio --flash_size 2MB --flash_freq 80m 0x1000 bootloader.bin 0x8000 partition-table.bin 0x10000 secure-hub-peripheral.bin

For example, on my Windows test machine, I used the following line:
> python C:\Espressif\frameworks\esp-idf-v5.0\components\esptool_py\esptool\esptool.py -p COM8 -b 460800 --before default_reset --after hard_reset --chip esp32  write_flash --flash_mode dio --flash_size 2MB --flash_freq 80m 0x1000 bootloader.bin 0x8000 partition-table.bin 0x10000 secure-hub-peripheral.bin

This should produce screen output indicating that a new image is being flashed to the ESP32.


The hub communicates with the board through Wi-Fi, and the prototype uses hardcoded Wi-Fi SSID and password. You will need to set up a Wi-Fi router or other acceess point with SSID "myssid" and WPA2 password "mypassword" (without quotes). The ESP32 board should automatically connect after being powered on. Alternatively, we can provide a binary with alternative SSID/PW upon request.

Next, you need to look up the ESP32 board's IP address. This can be done throught the control menu of your Wi-Fi router (or other access point) or by plugging the ESP32 board into a computer and running a serial port console on the bord's serial port with baud rate 115200. After resetting the device, it should produce a considerable amount of debugging output through the serial port. The IP address should appear toward the end.


## Minimal hub implementation

The above camera implementation is intended to communicate with OpenHAB hub software through HTTPS (REST).
Both sides (the hub and the ESP32 board) must use TLS client authentication to verify the identity of each other.
To reduce the hassle of setting up a patched OpenHAB,
we provide a Linux CLI program written in Rust that performs the Spacelord TLS authentication.

- Use `peripheral/hub-x86_64` to perform peripheral tests on a laptop
- Use `peripheral/hub-aarch64` to perform peripheral tests with a Spacelord board

With the ESP32 board powered up, run this hub program as follows:

> hub-x86_64 `IP address of ESP32 board'

Next, a command-line menu should appear that allows you to control the sensor (i.e., camera) and actuator (i.e., LED) of the ESP32 board.
