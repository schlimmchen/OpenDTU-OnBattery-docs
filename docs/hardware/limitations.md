# ESP32 Hardware Limitations

## Hardware UARTs

### Amount

Depending on the ESP32 you use and depending on the firmware variant, either
two or three hardware UARTs are available.

| MCU      | Firmware              | UARTs |
| -------- | --------------------- | ----- |
| ESP32    | any                   | 2     |
| ESP32-S3 | `generic_esp32s3`     | 2     |
| ESP32-S3 | `generic_esp32s3_usb` | 3     |

The ESP32 has three hardware UART controllers. On ESP32, the first controller
is always reserved for the serial console. This is also the case for ESP32-S3
chips, if the firmware variant uses the first port for the serial console. Only
on ESP32-S3, which has a native USB port, and only if that USB port is used to
transport the serial console messages instead (determined by a compile-time
switch), three hardware UARTs are available.

### Users

The following features/peripherals currently require a hardware UART:

1. Victron charge controllers
2. Victron SmartShunts
3. JK BMS

### Serial Port Manager

All features that need a hardware UART request access to one from the serial
port manager. Requests are made in the same order as the hardware UART users
are listed above. The serial port manager allows to use the available hardware
UARTs freely, without risking conflicts due to hard-coded controllers. However,
once all hardware UARTs are occupied, features/peripherals requiring a hardware
UART will fail to initialize. Have a look at the output on the [serial
console](../firmware/howto/serial_console.md) when booting to know how hardware
UARTs are assigned.
