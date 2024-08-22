# Compile on CLI

## Step by Step

1. Install [PlatformIO Core](https://platformio.org/install/cli){target=_blank} (PIO).
2. Clone the [code repository](https://github.com/helgeerbe/OpenDTU-OnBattery).
   You really have to clone it, do not download and extract a source ZIP file.
   During the build process the GIT hash gets embedded into the firmware. If you
   download and extract the source ZIP file a build error will occur.
3. Adjust the COM port in file `platformio_override.ini`. It occurs twice:
    * `upload_port`
    * `monitor_port`
4. Mandatory: [Build the WebApp](compile_webapp.md) **before** compiling the firmware.
5. Build the firmware: `platformio run -e generic_esp32s3` (chose a suitable PIO environment)
6. Upload to ESP32 module: `platformio run -e generic_esp32s3 -t upload`

## Other Popular PlatformIO Tasks

* Clean the sources:  `platformio run -e generic_esp32s3 -t clean`
* Erase flash: `platformio run -e generic_esp32s3 -t erase`