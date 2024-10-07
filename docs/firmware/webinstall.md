# Community WebFlasher

Use the [Community WebFlasher](https://solar.metacontrol.eu/opendtu-onbattery-webflasher/)
to install OpenDTU-OnBattery on your ESP32 or ESP32-S3 board with a
user-defined release version of the pre-built firmware binaries (sourced from
the project's GitHub [Releases Page](https://github.com/hoylabs/OpenDTU-OnBattery/releases)).

The WebFlasher is platform-independent, but requires the Chrome or Edge browser.

## Troubleshooting

* It might be required to manually [enter bootloader mode](flash_esp.md#bootloader-mode)
  before attempting to flash the ESP32 using the WebFlasher.
* Try holding the `BOOT` button on your board until you see the WebFlasher is
  erasing the flash memory and actually installing the firmware. This can help
  when a reset is performed in the preparation step, as holding the `BOOT`
  button ensures that the ESP32 restarts into bootloader mode.
* Make sure to [disconnect peripherals from UART0](flash_esp.md#free-uart0).
