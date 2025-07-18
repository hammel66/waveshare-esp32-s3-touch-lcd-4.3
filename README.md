# Solar Display with Waveshare ESP32-S3-Touch-LCD-4.3

# DRAFT: This is only a copy and must be edited

| Supported ESP SoCs |  ESP32-S3 | Waveshare ESP32-S3-Touch-LCD-4.3 |
| ------------------ | --------- | - |

# Example

## Overview

This example implements a simple Wi-Fi clock demo, which UI is created by Squareline Studio. And for `RGB/MIPI-DSI` interface LCDs, it can enable the avoid tearing and rotation function.

This example can run on various LCD resolutions, but since the UI itself is designed based on a `320 x 240` resolution, it will look very uncoordinated if the actual resolution is too large.

## How to Use

### Step 1. Install SDK and dependencies

- Install the following SDK and library dependencies:

  - See [SDK & Dependencies](../../../../../docs/envs/use_with_arduino.md#sdk--dependencies) and [Installing Libraries](../../../../../docs/envs/use_with_arduino.md#installing-libraries) sections for more information

- Install the following example dependencies:

  - `lvgl`: v8.4.0
  - `NTPClient`: v3.2.1
  - `ArduinoJson`: v6.21.3
  - `ui`: Please copy the [ui](./ui) folder from project directory to [Arduino library directory](../../../../../docs/envs/use_with_arduino.md#where-is-the-arduino-library-directory). See [Porting SquareLine Projects](../../../../../docs/envs/use_with_arduino.md#porting-squareline-projects) for more information

### Step 2. Configure the libraries

- [Mandatory] `ESP32_Display_Panel`:

  - This example already has the [esp_panel_board_supported_conf.h](./esp_panel_board_supported_conf.h) and [esp_panel_board_custom_conf.h](./esp_panel_board_custom_conf.h) configuration files in the project directory. But no board configuration enabled by default, before compiling, please edit the configuration file according to your target board:

    - **If using a [supported board](../../../../../README.md#supported-boards)**, edit the *esp_panel_board_supported_conf.h* file and set `ESP_PANEL_BOARD_DEFAULT_USE_SUPPORTED` to `1`. Then uncomment the target board definition in the file
    - **If using a custom board**, edit the *esp_panel_board_custom_conf.h* file and set `ESP_PANEL_BOARD_DEFAULT_USE_CUSTOM` to `1`. Then change other configurations as needed in the file

  - This example already has the [esp_panel_drivers_conf.h](./esp_panel_drivers_conf.h) configuration file in the project directory. Edit this file as needed.
  - see [Board Configuration Guide](../../../../../docs/envs/use_with_arduino.md#configuration-guide) for more information

- [Optional] `esp-lib-utils` :

  - This example already has the [esp_utils_conf.h](./esp_utils_conf.h) configuration file in the project directory. Edit this file as needed
  - See [Configuring esp-lib-utils](../../../../../docs/envs/use_with_arduino.md#configuring-esp-lib-utils) section for more information

- [Optional] `lvgl` :

  - This example already has the [lv_conf.h](./lv_conf.h) configuration file which been modified with the recommended configurations in the project directory
  - Change the `LV_COLOR_16_SWAP` macro definition to `1` if using `SPI/QSPI` interface, or `0` if using other interfaces
  - Change other configurations in the file as needed
  - See [Configuring LVGL](../../../../../docs/envs/use_with_arduino.md#configuring-lvgl) section for more information

### Step 3. Configure the example

- [Mandatory] Edit the macro definitions in the [squareline_wifi_clock.ino](./squareline_wifi_clock.ino) file

  - To obtain and calibrate time information after connecting to Wi-Fi, please correctly fill in your time zone within the macro `TIMEZONE_OFFSET` (such as `CST-8`).
  - To obtain weather information after connecting to Wi-Fi, please follow the steps:

    - Register an account on [OpenWeather](https://openweathermap.org/) and obtain an **API KEY** in the personal profile.
    - Fill the obtained API KEY in the macro definition `WEATHER_API_KEY`.
    - Fill the name of the city for which need to obtain weather information (such as `Shanghai`) in the macro definition `WEATHER_CITY`.

- [Optional] Edit the macro definitions in the [lvgl_v8_port.h](./lvgl_v8_port.h) file

  - **If using `RGB/MIPI-DSI` interface**, change the `LVGL_PORT_AVOID_TEARING_MODE` macro definition to `1`/`2`/`3` to enable the avoid tearing function. After that, change the `LVGL_PORT_ROTATION_DEGREE` macro definition to the target rotation degree
  - **If using other interfaces**, please don't modify the `LVGL_PORT_AVOID_TEARING_MODE` and `LVGL_PORT_ROTATION_DEGREE` macro definitions

### Step 4. Configure Arduino IDE

- Navigate to the `Tools` menu
- Select the target board in the `Board` menu
- Change the `Partition Scheme` and `Flash Size` to make the flash size enough for the project (like `Huge App` + `4MB`)
- Change the `PSRAM` option to `OPI PSRAM` if using `ESP32S3R8 + RGB LCD`, or `Enabled` if using `ESP32P4 + MIPI-DSI LCD`
- Change the `USB CDC On Boot` option to `Enabled` if using `USB` port, or `Disabled` if using `UART` port. If this configuration differs from previous flashing, first enable `Erase All Flash Before Sketch Upload`, then it can be disabled after flashing.
- Change other configurations as needed
- see [Configuring Arduino IDE](../../../../../docs/envs/use_with_arduino.md#configuring-arduino-ide) for more information

### Step 5. Compile and upload the project

- Connect the board to your computer
- Select the correct serial port
- Click the `upload` button

### Step 6. Check the serial output

- Open the serial monitor and select the correct baud rate (like `115200`)
- Check the output logs

## Serial Output

The following are the logs output when using the `Espressif:ESP32_S3_LCD_EV_BOARD_2_V1_5` development board. The logs content may vary with different development boards or different configurations, and it is provided for reference only.

```bash
...
Initializing board
[I][Panel][esp_panel_board.cpp:0066](init): Initializing board (Espressif:ESP32_S3_LCD_EV_BOARD_2_V1_5)
[I][Panel][esp_panel_board.cpp:0235](init): Board initialize success
[I][Panel][esp_panel_board.cpp:0253](begin): Beginning board (Espressif:ESP32_S3_LCD_EV_BOARD_2_V1_5)
[I][Panel][esp_lcd_touch_gt1151.c:0050](esp_lcd_touch_new_i2c_gt1151): version: 1.0.5
[I][Panel][esp_lcd_touch_gt1151.c:0234](read_product_id): IC version: GT1158_000101(Patch)_0102(Mask)_00(SensorID)
[I][Panel][esp_panel_board.cpp:0459](begin): Board begin success
Initializing LVGL
[I][LvPort][lvgl_v8_port.cpp:0769](lvgl_port_init): Initializing LVGL display driver
Creating UI
NVS: selected_wifi_name: xxxxxxxx
NVS: wifi_password: xxxxxxxx
Wifi connecting...
NVS: selected_wifi_name: xxxxxxxx
NVS: wifi_password: xxxxxxxx
NVS Wifi Connecting Success
wifi_connected_flag: true
lat_lon_url: http://api.openweathermap.org/geo/1.0/direct?q=Shanghai&limit=1&appid=xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
lat: 31.2322758
lon: 121.4692071
Weather: Rain
temperature: 7
...
```

## Troubleshooting

Please check the [FAQ](../../../../../docs/envs/use_with_arduino.md#faq) first to see if the same question exists. If not, please create a [Github Issue](https://github.com/esp-arduino-libs/ESP32_Display_Panel/issues). We will get back to you as soon as possible.
