# Victron Charge Controllers

Victron SmartSolar and BlueSolar charge controllers can be connected to
OpenDTU-OnBattery using the [VE.Direct](vedirect.md) interface.

This allows OpenDTU-OnBattery to

* read data from the charge controller
* display the data in the web UI
* publish the data to the MQTT broker
* and make the data auto-discoverable in HomeAssistent.

Additionally, knowing the amount of solar power currently being produced, can
be leveraged by the Dynamic Power Limiter to implement (Full)
Solar-Passthrough. This feature allows to set the limit of the inverter such
that it uses the available solar power to generate AC power directly, i.e.,
without storing it in the battery just so that it can be discharged later.

## Retrieve Data

Each charge controller whose data shall be processed must be connected to
OpenDTU-OnBattery using the [VE.Direct](vedirect.md) interface, i.e., one wired
connection each.

For every connected charge controller, the ESP32 currently must use a hardware
UART. This limits the amount of charge controllers that can be connected to one
ESP32 with OpenDTU-OnBattery to either two or three, see
[limitations](limitations.md).

To start processing messages from a charge controller, enable the VE.Direct
interface in the web UI. Additionally, define up to three charge controllers in
the [device profile](../firmware/device_profiles.md).

## VE.Smart Network

In case only one or only a subset of all available charge controllers in the
system can be connected to OpenDTU-OnBattery, you may want to determine the
total solar production so that the Dynamic Power Limiter (Full)
Solar-Passthrough feature works as expected.

To do so,

* configure all charge controllers to be part of the same VE.Smart Bluetooth network.
* connect the receive pin of the charge controller with a transmit (TX) pin on the ESP32.
* configure the transmit pin in the [device profile](../firmware/device_profiles.md).

This setup allows OpenDTU-OnBattery to query the "VE.Smart network total power"
using a HEX-Mode message. This value, if available, is then preferred to
determine the available solar power.
