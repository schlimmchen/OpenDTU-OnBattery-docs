# Migrate 'generic' to 'generic_esp32'

!!!note "Applicability"
    This information only applies to older releases. Neither the `generic` nor
    the `generic_esp32` firmware variants are released any more.

## Differences

The only difference between `opendtu-onbattery-generic.bin` (deprecated) and `opendtu-onbattery-generic_esp32.bin` is, that `opendtu-onbattery-generic.bin` contains hard-coded pins for the nRF24 Module (and only for that module). The `opendtu-onbattery-generic_esp32.bin` comes with no pre-configured pins and can be set-up by uploading a [device profile](../device_profiles.md).

## Migration process

* Make a backup of your configuration! (**Settings** --> **Config Management** --> **Backup** --> Select **config.json** --> Press **Backup**)
* Download the latest `opendtu-onbattery-generic_esp32.bin` file from the GitHub [Release Page](https://github.com/helgeerbe/OpenDTU-OnBattery/releases){target=_blank}
* Download [a compatible device profile](https://raw.githubusercontent.com/helgeerbe/OpenDTU-OnBattery/master/docs/DeviceProfiles/nodemcu_esp32.json){target=_blank}. It contains the same pin assignments as the hard-coded ones in `opendtu-onbattery-generic.bin`.
* Upload the device profile. (**Settings** --> **Config Management** --> **Restore** --> Select **Pin Mapping (pin_mapping.json)** --> Select `nodemcu_esp32.json` --> Press **Restore**)
* The ESP reboots but does nothing different at the moment.
* Select the new uploaded device profile. This can already be done using the `opendtu-onbattery-generic.bin` firmware. (**Settings** --> **Device-Manager** --> **Selected profile** --> Select `NRF24` --> Press **Save**)
* The ESP reboots and uses the pin assignment from the device profile. (Which makes no difference because they are equal to the old one)
* Upload the new firmware (**Settings** --> **Firmware Upgrade**)
* The ESP reboots
* All done!
