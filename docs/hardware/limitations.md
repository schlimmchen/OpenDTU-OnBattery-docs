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

## Using UART0

In general, avoid using UART0 to connect peripherals.

* On ESP32, GPIO1 and GPIO3 are in use by UART0.
* On ESP32-S3, GPIO43 and GPIO44 are in use by UART0.

### Bootloader Interaction

Connecting a peripheral to UART0 of your ESP32 can break interaction with the
bootloader. The bootloader uses UART0 to communicate with the flash tool. A
peripheral connected to UART0 might therefore interfere in the communication
with the bootloader, preventing writing to the flash memory over USB in
particular.

* On ESP32 boards, UART0 is connected to the USB-UART bridge.
* On ESP32-S3 boards with multiple USB ports, the port connected to the
  USB-UART bridge on the USB side is connected to UART0 on the UART side
  of the bridge.

### Bootloader Output

The ESP32's bootloader will print messages on UART0 on every boot. If a
peripheral is connected to UART0, this peripheral will receive these messages.
If the peripheral is not robust against invalid messages and, depending on the
baud rate, invalid UART chararacters, it may cease to function properly.

### Firmware Messages

OpenDTU-OnBattery uses UART0 to print messages. These are the same messages
appearing in the web console, except that connecting to UART0 allows to read
messages even while the firmware is still booting and not yet connected to the
network.

On ESP32-S3 using firmware variant `generic_esp32s3_usb` (all environments that
define `ARDUINO_USB_MODE=1` and `ARDUINO_USB_CDC_ON_BOOT=1`), the messages are
instead available on the virtual serial interface of the native USB connection.

## SPI Busses

ESP32 and ESP32-S3 chips provide four seperate SPI interfaces. Two of them are
reserved for communicating with the flash and/or PSRAM. The remaining two are
free to use for peripherals. This means only two SPI peripherals can be
connected at a time. The following peripherals need an SPI bus each:

* NRF24 radio module
* CMT2300 radio module
* Huawei CAN interface
* Some diplays
