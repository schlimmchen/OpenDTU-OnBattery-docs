# Getting Started

OpenDTU-OnBattery supports the ESP32 family of microcontrollers. ESP32-S3
chips are preferred.

!!! note "Flash Memory"
    Due to the growing size of the firmware images, ESP32(-S3) boards with a
    minimum of 8 MB of flash memory are required in order to utilize
    over-the-air firmware updates. Most ESP32 boards provide only 4 MB of
    flash memory.

Depending on the inverter to be addressed, different RF modules are required.

- The HM series requires the NRF24L01+ module
- The HMS/HMT series requires the CMT2300A module

Please see the [inverter overview](inverter_overview.md) to see if your inverter is supported and to determine the required RF module.

For an easy start, acquire an [OpenDTU Fusion](../3rd_party/opendtu_fusion.md) board.

## Steps to build your own DTU

1. Determine the [RF module(s)](inverter_overview.md) you need.
2. Get an ESP32-S3 board.
3. Use a power suppy with 5 V and 1 A. The USB cable connected to your
   PC/Notebook may be powerful enough or may be not. Also the quality of the
   used USB cable might have an impact.
4. Wire the ESP32-S3 to the RF module(s).
5. Wire a [display](display.md) (optional).
6. [Flash the firmware](../firmware/flash_esp.md) via USB.
7. Upload a [device profile](../firmware/device_profiles.md) which describes
   your hardware (or look at the profile first and connect your pins
   accordingly) using the [Config
   Managment](../firmware/configuration/config_settings.md).
