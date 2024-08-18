# Upgrade from OpenDTU

In general, one can switch seamlessly from OpenDTU to OpenDTU-OnBattery, as the
parts and features inherited from the upstream project are kept compatible.
This is particularly true for the settings.

However, when switching from OpenDTU to OpenDTU-OnBattery, performing an OTA
update will fail, as the OpenDTU-OnBattery firmware images are too large to fit
the upstream's partition layout. This project's partition layout for the ESP32
flash memory is therefore different from the upstream project as of version
2024.08.18. Follow the respective [upgrade guide](upgrade_8mb.md), which is
also applicable when upgrading from OpenDTU to OpenDTU-OnBattery.

In case you want to switch back to OpenDTU (without losing settings), you may
do so by

* performing an OTA update using the respective OpenDTU (non-factory) firmware
  binary (unless you are using an OpenDTU-OnBattery variant without OTA
  support).
* writing the OpenDTU factory image suitable for your board using a USB
  connection.
