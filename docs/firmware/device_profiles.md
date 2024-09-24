# Device Profiles

!!! note "Sample Profiles"
    Ready-to-use device profiles can be found [in the code
    repository](https://github.com/hoylabs/OpenDTU-OnBattery/tree/master/docs/DeviceProfiles){target=_blank}.

## Summary

Perform these steps to configure pin assignments for your board:

1. Upload an appropriate device profile (JSON file).
2. Afterwards, select a profile in the Web UI Device-Manager.

## Details

It is required to setup hardware settings like pin assignments or Ethernet
support using a JSON file. This tells OpenDTU-OnBattery what peripherals are
connected and how they are connected. The JSON file is uploaded using the
configuration management (**Settings** --> **Config Management**) in the web
interface. Select "Pin Mapping (pin_mapping.json)" in the dropdown menu of the
"Restore" section and choose the file to upload, then click the "Restore" button.

After the file was uploaded, the ESP performs a reboot. This is required as the
pin settings could have changed within the file and pin assignments are
initialized when booting.

To initially select or to change a device profile, navigate to **Settings** -->
**Device-Manager** and select the appropriate profile. When changing the device
profile, the ESP reboots. You can see the current (Active) and the new
(Selected) pin assignment in the table below the combobox.

The JSON file can contain multiple profiles. Each profile requires a unique
name and the respective parameters. If any parameter is not set, the default
value `-1` ("not in use") will be effective. The default value may actually be
something else if you compile the firmware yourself, in which case it is
assumed that you know what you are doing.

## Structure of the JSON file

!!!note "GPIO Numbers"
    Please be aware that the numerical values used in the device profile JSON
    file are **ESP32 chip GPIO numbers** (NOT physical pin numbers). Refer to
    the documentation of your respective ESP32 board to learn at what physical
    pin header a particular ESP32 GPIO is available.

!!!warning "GPIO Numbering on different chips"
    Some GPIO numbers available on one particular chip may be unavailable on
    another. Keep this in mind when upgrading, e.g., from an ESP32 to an
    ESP32-S3. Also, different boards may expose different GPIOs on their
    respective pin headers. Always check which GPIOs are actually available on
    your board before choosing which GPIOs to use.

!!!note "Examples"
    These profiles are partially incomplete and merely serve as example snippets.

```json
[
    {
        "name": "Generic NodeMCU 38 pin with SSD1306 display",
        "nrf24": {
            "miso": 19,
            "mosi": 23,
            "clk": 18,
            "irq": 16,
            "en": 4,
            "cs": 5
        },
        "victron": {
            "rx": 22,
            "tx": -1
        },
        "battery": {
            "rx": 27,
            "tx": 14
        },
        "huawei": {
            "miso": 12,
            "mosi": 13,
            "clk": 26,
            "irq": 25,
            "power": 33,
            "cs": 15
        },
        "display": {
            "type": 2,
            "data": 21,
            "clk": 22
        },
        "eth": {
            "enabled": false,
            "phy_addr": -1,
            "power": -1,
            "mdc": -1,
            "mdio": -1,
            "type": -1,
            "clk_mode": -1
        }
    },
    {
        "name": "Generic NodeMCU 38 pin with SSD1306",
        "nrf24": {
            "miso": 19,
            "mosi": 23,
            "clk": 18,
            "irq": 16,
            "en": 4,
            "cs": 5
        },
        "eth": {
            "enabled": false,
            "phy_addr": -1,
            "power": -1,
            "mdc": -1,
            "mdio": -1,
            "type": -1,
            "clk_mode": -1
        },
        "display": {
            "type": 2,
            "data": 21,
            "clk": 22
        },
        "powermeter": {
            "rx": 25,
            "tx": 26,
            "dere": 27
        }
    },
    {
        "name": "Olimex ESP32-POE",
        "nrf24": {
            "miso": 15,
            "mosi": 2,
            "clk": 14,
            "irq": 13,
            "en": 16,
            "cs": 5
        },
        "eth": {
            "enabled": true,
            "phy_addr": 0,
            "power": 12,
            "mdc": 23,
            "mdio": 18,
            "type": 0,
            "clk_mode": 3
        }
    },
    {
        "name": "OpenDTU FUSION v2 + JK BMS on RS485 Transceiver",
        "battery": {
            "rx": 16,
            "rxen": 15,
            "tx": 45,
            "txen": 46
        }
    },
    {
        "name": "OpenDTU FUSION v2 + 2xVictron MPPT + Victron SmartShunt",
        "nrf24": {
            "miso": 48,
            "mosi": 35,
            "clk": 36,
            "irq": 47,
            "en": 38,
            "cs": 37
        },
        "cmt": {
            "clk": 6,
            "cs": 4,
            "fcs": 21,
            "sdio": 5,
            "gpio2": 3,
            "gpio3": 8
        },
        "led": {
            "led0": 17,
            "led1": 18
        },
        "battery": {
            "rx": 16,
            "tx": -1
        },
        "victron": {
            "rx": 22,
            "tx": -1,
            "rx2": 23,
            "tx2": -1
        }
    },
    {
        "name": "OpenDTU Fusion v2 with NRF24, MPPT, SDM72",
        "nrf24": {
            "miso": 48,
            "mosi": 35,
            "clk": 36,
            "irq": 47,
            "en": 38,
            "cs": 37
        },
        "victron": {
            "rx": 22,
            "tx": -1,
        },
        "powermeter": {
            "rx": 16,
            "tx": 45,
            "rxen": 15,
            "txen": 46
        }
    }
]
```

## Implemented configuration values

| Parameter       | Data Type | Description |
| --------------- | --------- | ----------- |
| name            | string    | Unique name of the profile (max 63 characters) |
| links           | array     | Must contain a object with the properties **name** and **url**. For each object a button is shown in the Device-Manager
| nrf24.miso      | number    | MISO Pin |
| nrf24.mosi      | number    | MOSI Pin |
| nrf24.clk       | number    | Clock Pin |
| nrf24.irq       | number    | Interrupt Pin |
| nrf24.en        | number    | Enable Pin |
| nrf24.cs        | number    | Chip Select Pin |
| cmt.sdio        | number    | SDIO Pin |
| cmt.clk         | number    | CLK Pin |
| cmt.cs          | number    | CS Pin |
| cmt.fcs         | number    | FCS Pin |
| cmt.gpio2       | number    | GPIO2 Pin (optional) |
| cmt.gpio3       | number    | GPIO3 Pin (optional) |
| eth.enabled     | boolean   | Enable/Disable the ethernet stack |
| eth.phy_addr    | number    | Unique PHY addr |
| eth.power       | number    | Power Pin (if available). Use -1 for not assigned pins. |
| eth.mdc         | number    | Serial Management Interface MDC Pin. Use -1 for not assigned pins. |
| eth.mdio        | number    | Serial Management Interface MDIO Pin. Use -1 for not assigned pins. |
| eth.type        | number    | Possible values:<ul><li>0 = ETH_PHY_LAN8720</li><li>1 = ETH_PHY_TLK110</li><li>2 = ETH_PHY_RTL8201</li><li>3 = ETH_PHY_DP83848</li><li>4 = ETH_PHY_DM9051</li><li>5 = ETH_PHY_KSZ8041</li><li>6 = ETH_PHY_KSZ8081</li></ul> |
| eth.clk_mode    | number    | Possible values:<ul><li>0 = ETH_CLOCK_GPIO0_IN</li><li>1 = ETH_CLOCK_GPIO0_OUT</li><li>2 = ETH_CLOCK_GPIO16_OUT</li><li>3 = ETH_CLOCK_GPIO17_OUT</li></ul> |
| w5500.sclk      | number    | W5500 SPI Clock Pin |
| w5500.mosi      | number    | W5500 MOSI Pin |
| w5500.miso      | number    | W5500 MISO Pin |
| w5500.cs        | number    | W5500 Chip Select Pin |
| w5500.int       | number    | W5500 Interrupt Pin |
| w5500.rst       | number    | W5500 Reset Pin |
| display.type    | number    | Specify type of display. Possible values:<ul><li>0 = None (default)</li><li>1 = PCD8544</li><li>2 = SSD1306</li><li>3 = SH1106</li><li>4 = SSD1309</li><li>5 = ST7567S GM12864-59N</li></ul> |
| display.data    | number    | Data Pin (e.g. SDA for i2c displays) required for all displays. Use 255 for not assigned pins. |
| display.clk     | number    | Clock Pin (e.g. SCL for i2c displays) required for SSD1306 and SH1106. Use 255 for not assigned pins. |
| display.cs      | number    | Chip Select Pin required for PCD8544. Use 255 for not assigned pins. |
| display.reset   | number    | Reset Pin required for PCD8544, optional for all other displays. Use 255 for not assigned pins. |
| led.led0        | number    | LED pin for network indication. <ul><li>Blinking = WLAN connected but NTP & MQTT (if enabled) disconnected.</li><li>On = WLAN, NTP, MQTT connected.</li><li>Off = Network not connected</li></ul> |
| led.led1        | number    | LED pin for inverter indication. <ul><li>On = All inverters reachable & producing.</li><li>Blinking = All inverters reachable but not producing.</li><li>Off = At least one inverter is not reachable.</li></ul> Only inverters with polling enabled are considered. |
| victron.rx      | number    | Victron MPPT Charger VE.Direct receive pin  |
| victron.tx      | number    | Victron MPPT Charger VE.Direct transmit pin, can be set to -1 |
| victron.rx2     | number    | Second Victron MPPT Charger VE.Direct receive pin  |
| victron.tx2     | number    | Second Victron MPPT Charger VE.Direct transmit pin, can be set to -1 |
| victron.rx3     | number    | Third Victron MPPT Charger VE.Direct receive pin  |
| victron.tx3     | number    | Third Victron MPPT Charger VE.Direct transmit pin, can be set to -1 |
| battery.rx      | number    | Pylontech battery CAN bus receive pin,<br/> JK BMS receive pin or<br/> Victron SmartShunt VE.Direct receive pin |
| battery.tx      | number    | Pylontech battery CAN bus transmit pin,<br/> JK BMS transmit pin or<br/> Victron SmartShunt VE.Direct  transmit pin |
| battery.rxen    | number    | JK BMS receive enable pin for RS485 transceiver mode |
| battery.txen    | number    | JK BMS transmit enable pin for RS485 transceiver mode |
| huawei.miso     | number    | MISO Pin for Huawei CAN bus interface |
| huawei.mosi     | number    | MOSI Pin for Huawei CAN bus interface |
| huawei.clk      | number    | CLK Pin for Huawei CAN bus interface |
| huawei.cs       | number    | CS Pin for Huawei CAN bus interface |
| huawei.irq      | number    | IRQ Pin for Huawei CAN bus interface |
| huawei.power    | number    | Power Pin for Huawei power control (e.g. using slot detect) |
| powermeter.rx   | number    | Serial power meter receive pin |
| powermeter.tx   | number    | Serial power meter transmit pin (required for SDM, invalid for SML) |
| powermeter.dere | number    | Serial power meter "driver/receiver enable" pin (only for SDM, optional, can't be combined with rxen+txen) |
| powermeter.rxen | number    | Serial power meter "receiver enable" pin (only for SDM, optional, requires txen, can't be combined with dere) |
| powermeter.txen | number    | Serial power meter "driver enable" pin (only for SDM, optional, requires rxen, can't be combined with dere) |
