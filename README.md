# Raspberry Pi Pico SDK Examples

## Getting started

See [Getting started with Raspberry Pi Pico-series](https://rptl.io/pico-get-started) and the README in the [pico-sdk](https://github.com/raspberrypi/pico-sdk) for information
on getting up and running.

##### Notes on different boards and platforms (RP2040 / RP2350) 

The majority of examples are applicable to both RP2040 and RP2350 based boards,
however certain examples that use chip-specific functionality will only build on that platform.
Similarly, Wi-Fi and Bluetooth examples will only build on a board that includes Wi-Fi and Bluetooth support.

Platform and board information are passed to the CMake build via the `PICO_PLATFORM` and `PICO_BOARD` variables.

By default, the Pico SDK targets builds for RP2040 (`PICO_PLATFORM=rp2040`). To build for RP2350 instead, pass
`-DPICO_PLATFORM=rp2350` to CMake (or `-DPICO_PLATFORM=rp2350-riscv` for RISC-V). Alternatively, in many cases, you can rely
on the board configuration to set the platform for you. For example, passing `-DPICO_BOARD=pico2` will automatically select `PICO_PLATFORM=rp2350`.

For more information see the "Platform and Board Configuration" chapter of 
the [Raspberry Pi Pico-series C/C++ SDK](https://rptl.io/pico-c-sdk) book.

Information on which examples are not being built is displayed during the CMake configuration step.

### First Examples

App| Description | Link to prebuilt UF2
---|---|---
[hello_serial](hello_world/serial) | The obligatory Hello World program for Pico (output over serial version). |
[hello_usb](hello_world/usb) | The obligatory Hello World program for Pico (output over USB version). | https://rptl.io/pico-hello-usb
[blink](blink) | Blink a LED on and off. Works on both boards with regular LEDs and boards like Pico W where the LED is connected via the Wi-Fi chip. | https://rptl.io/pico-blink
[blink_simple](blink_simple) | Blink a LED on and off. Does not work on boards like Pico W where the LED is connected via the Wi-Fi chip. |
[picow_blink](pico_w/wifi/blink) | Blinks the on-board LED on boards like Pico W where the LED is connected via the Wi-Fi chip. | http://rptl.io/pico-w-blink

### ADC

App|Description
---|---
[hello_adc](adc/hello_adc) | Display the voltage from an ADC input.
[joystick_display](adc/joystick_display) | Display a Joystick X/Y input based on two ADC inputs.
[adc_console](adc/adc_console) | An interactive shell for playing with the ADC. Includes example of free-running capture mode.
[onboard_temperature](adc/onboard_temperature) | Display the value of the onboard temperature sensor.
[microphone_adc](adc/microphone_adc) | Read analog values from a microphone and plot the measured sound amplitude.
[dma_capture](adc/dma_capture) | Use the DMA to capture many samples from the ADC.
[read_vsys](adc/read_vsys) | Demonstrates how to read VSYS to get the voltage of the power supply.

### Binary Info

App|Description
---|---
[blink_any](binary_info/blink_any) | Uses `bi_ptr` variables to create a configurable blink binary - see the separate [README](binary_info/README.md) for more details.
[hello_anything](binary_info/hello_anything) | Uses `bi_ptr` variables to create a configurable hello_world binary - see the separate [README](binary_info/README.md) for more details.

### Bootloaders (RP235x Only)

These examples all produce multiple UF2s - a bootloader UF2, and then a separate UF2 of the program that the bootloader will load and boot. To load them onto a device with empty flash, first load the bootloader UF2, then reset to BOOTSEL mode and load the program UF2. This ordering is required because the bootloaders contain embedded partition tables - see section 5.10.6 in the RP2350 datasheet for more details on those.

App|Description
---|---
[enc_bootloader](bootloaders/encrypted) | A bootloader which decrypts binaries from flash into SRAM. See the separate [README](bootloaders/encrypted/README.md) for more information.
[uart_boot](bootloaders/uart) | A bootloader which boots a separate RP2350 using the UART boot interface. See section 5.8 in the datasheet for more details, including the wiring requirements.

### Clocks

App|Description
---|---
[hello_48MHz](clocks/hello_48MHz) | Change the system clock frequency to 48 MHz while running.
[hello_gpout](clocks/hello_gpout) | Use the general purpose clock outputs (GPOUT) to drive divisions of internal clocks onto GPIO outputs.
[hello_resus](clocks/hello_resus) | Enable the clock resuscitate feature, "accidentally" stop the system clock, and show how we recover.
[detached_clk_peri](clocks/detached_clk_peri) | Detach peripheral clock and vary system clock.

### CMake

App|Description
---|---
[build_variants](cmake/build_variants) | Builds two versions of the same app with different configurations.

### DCP (RP235x Only)

App|Description
---|---
[hello_dcp](dcp/hello_dcp) | Use the double-precision coprocessor directly in assembler.

### DMA

App|Description
---|---
[hello_dma](dma/hello_dma) | Use the DMA to copy data in memory.
[control_blocks](dma/control_blocks) | Build a control block list, to program a longer sequence of DMA transfers to the UART.
[channel_irq](dma/channel_irq) | Use an IRQ handler to reconfigure a DMA channel, in order to continuously drive data through a PIO state machine.
[sniff_crc](dma/sniff_crc) | Use the DMA engine's 'sniff' capability to calculate a CRC32 on a data buffer.

### Encrypted (RP235x Only)

App|Description
---|---
[hello_encrypted](encrypted/hello_encrypted) | Create a self-decrypting binary, using the hardened decryption stage. This should be secure against side channel attacks.
[hello_encrypted_mbedtls](encrypted/hello_encrypted) | Create a self-decrypting binary, using the MbedTLS decryption stage. This is not secure against side channel attacks, so is fast but provides limited protection.

### HSTX (RP235x Only)

App|Description
---|---
[dvi_out_hstx_encoder](hstx/dvi_out_hstx_encoder) | Use the HSTX to output a DVI signal with 3:3:2 RGB.

### Flash

App|Description
---|---
[cache_perfctr](flash/cache_perfctr) | Read and clear the cache performance counters. Show how they are affected by different types of flash reads.
[nuke](flash/nuke) | Obliterate the contents of flash. An example of a NO_FLASH binary (UF2 loaded directly into SRAM and runs in-place there). A useful utility to drag and drop onto your Pico if the need arises.
[program](flash/program) | Erase a flash sector, program one flash page, and read back the data.
[xip_stream](flash/xip_stream) | Stream data using the XIP stream hardware, which allows data to be DMA'd in the background whilst executing code from flash.
[ssi_dma](flash/ssi_dma) | DMA directly from the flash interface (continuous SCK clocking) for maximum bulk read performance.
[runtime_flash_permissions](flash/runtime_flash_permissions) | Demonstrates adding partitions at runtime to change the flash permissions.
[partition_info](flash/partition_info) | Extract and enumerate partition information (address ranges, permissions, IDs, and names) from the partition table.

### FreeRTOS

These examples require you to set the `FREERTOS_KERNEL_PATH` to point to the FreeRTOS Kernel. See https://github.com/FreeRTOS/FreeRTOS-Kernel

App|Description
---|---
[hello_freertos_one_core](freertos/hello_freertos) | Demonstrates how to run FreeRTOS and tasks on one core.
[hello_freertos_two_cores](freertos/hello_freertos) | Demonstrates how to run FreeRTOS and tasks on two cores.
[hello_freertos_static_allocation](freertos/hello_freertos) | Demonstrates how to run FreeRTOS on two cores with static RAM allocation.

### GPIO

App|Description
---|---
[hello_7segment](gpio/hello_7segment) | Use the GPIOs to drive a seven segment LED display.
[hello_gpio_irq](gpio/hello_gpio_irq) | Register an interrupt handler to run when a GPIO is toggled.
[dht_sensor](gpio/dht_sensor) | Use GPIO to bitbang the serial protocol for a DHT temperature/humidity sensor.

See also: [blink](blink), blinking an LED attached to a GPIO.

### HW divider

App|Description
---|---
[hello_divider](divider) | Show how to directly access the hardware integer dividers, in case AEABI injection is disabled.

### I2C

App|Description
---|---
[bus_scan](i2c/bus_scan) | Scan the I2C bus for devices and display results.
[bmp280_i2c](i2c/bmp280_i2c) | Read and convert temperature and pressure data from a BMP280 sensor, attached to an I2C bus.
[lcd_1602_i2c](i2c/lcd_1602_i2c) | Display some text on a generic 16x2 character LCD display, via I2C.
[lis3dh_i2c](i2c/lis3dh_i2c) | Read acceleration and temperature value from a LIS3DH sensor via I2C
[mcp9808_i2c](i2c/mcp9808_i2c) | Read temperature from a MCP9808 sensor, set limits and raise alerts when limits are surpassed.
[mma8451_i2c](i2c/mma8451_i2c) | Read acceleration from a MMA8451 accelerometer and set range and precision for the data.
[mpl3115a2_i2c](i2c/mpl3115a2_i2c) | Interface with an MPL3115A2 altimeter, exploring interrupts and advanced board features, via I2C.
[mpu6050_i2c](i2c/mpu6050_i2c) | Read acceleration and angular rate values from a MPU6050 accelerometer/gyro, attached to an I2C bus.
[ssd1306_i2c](i2c/ssd1306_i2c) | Convert and display a bitmap on a 128x32 or 128x64 SSD1306-driven OLED display.
[pa1010d_i2c](i2c/pa1010d_i2c) | Read GPS location data, parse and display data via I2C.
[pcf8523_i2c](i2c/pcf8523_i2c) | Read time and date values from a PCF8523 real time clock. Set current time and alarms on it.
[ht16k33_i2c](i2c/ht16k33_i2c) | Drive a 4 digit 14 segment LED with an HT16K33.
[slave_mem_i2c](i2c/slave_mem_i2c) | i2c slave example where the slave implements a 256 byte memory.
[slave_mem_i2c_burst](i2c/slave_mem_i2c) | i2c slave example where the slave implements a 256 byte memory. This version inefficiently writes each byte in a separate call to demonstrate read and write burst mode.

### Interpolator

App|Description
---|---
[hello_interp](interp/hello_interp) | A bundle of small examples, showing how to access the core-local interpolator hardware, and use most of its features.

### Multicore

App|Description
---|---
[hello_multicore](multicore/hello_multicore) | Launch a function on the second core, printf some messages on each core, and pass data back and forth through the mailbox FIFOs.
[multicore_fifo_irqs](multicore/multicore_fifo_irqs) | On each core, register an interrupt handler for the mailbox FIFOs. Show how the interrupt fires when that core receives a message.
[multicore_runner](multicore/multicore_runner) | Set up the second core to accept, and run, any function pointer pushed into its mailbox FIFO. Push in a few pieces of code and get answers back.
[multicore_doorbell](multicore/multicore_doorbell) | Claims two doorbells for signaling between the cores. Counts how many doorbell IRQs occur on the second core and uses doorbells to coordinate exit.

### OTP (RP235x Only)

App|Description
---|---
[hello_otp](otp/hello_otp) | Demonstrate reading and writing from the OTP on RP235x, along with some of the features of OTP (error correction and page locking).

### Pico Board

App|Description
---|---
[blinky](picoboard/blinky) | Blink "hello, world" in Morse code on Pico's LED.
[button](picoboard/button) | Use Pico's BOOTSEL button as a regular button input, by temporarily suspending flash access.

### Pico Networking

These networking examples are only available if Wi-Fi is supported by the board.

App|Description
---|---
[picow_access_point](pico_w/wifi/access_point) | Starts a WiFi access point, and fields DHCP requests.
[picow_blink](pico_w/wifi/blink) | Blinks the on-board LED (which is connected via the WiFi chip).
[picow_blink_slow_clock](pico_w/wifi/blink) | Blinks the on-board LED (which is connected via the WiFi chip) with a slower system clock to show how to reconfigure communication with the WiFi chip at run time under those circumstances.
[picow_blink_fast_clock](pico_w/wifi/blink) | Blinks the on-board LED (which is connected via the WiFi chip) with a faster system clock to show how to reconfigure communication with the WiFi chip at build time under those circumstances.
[picow_iperf_server](pico_w/wifi/iperf) | Runs an "iperf" server for WiFi speed testing.
[picow_ntp_client](pico_w/wifi/ntp_client) | Connects to an NTP server to fetch and display the current time.
[picow_tcp_client](pico_w/wifi/tcp_client) | A simple TCP client. You can run [python_test_tcp_server.py](pico_w/wifi/python_test_tcp/python_test_tcp_server.py) for it to connect to.
[picow_tcp_server](pico_w/wifi/tcp_server) | A simple TCP server. You can use [python_test_tcp_client.py](pico_w//wifi/python_test_tcp/python_test_tcp_client.py) to connect to it.
[picow_tls_client](pico_w/wifi/tls_client) | Demonstrates how to make a HTTPS request using TLS.
[picow_tls_verify](pico_w/wifi/tls_client) | Demonstrates how to make a HTTPS request using TLS with certificate verification.
[picow_wifi_scan](pico_w/wifi/wifi_scan) | Scans for WiFi networks and prints the results.
[picow_udp_beacon](pico_w/wifi/udp_beacon) | A simple UDP transmitter.
[picow_httpd](pico_w/wifi/httpd) | Runs a LWIP HTTP server test app.
[picow_http_client](pico_w/wifi/http_client) | Demonstrates how to make http and https requests.
[picow_http_client_verify](pico_w/wifi/http_client) | Demonstrates how to make a https request with server authentication.
[picow_mqtt_client](pico_w/wifi/mqtt) | Demonstrates how to implement a MQTT client application.
[picow_ota_update](pico_w/wifi/ota_update) | A minimal OTA update server (RP235x only). See the separate [README](pico_w/wifi/ota_update/README.md) for more details.

#### FreeRTOS Networking

These are examples of integrating Wi-Fi networking under FreeRTOS, and require you to set the `FREERTOS_KERNEL_PATH`
to point to the FreeRTOS Kernel. See https://github.com/FreeRTOS/FreeRTOS-Kernel

App|Description
---|---
[picow_freertos_iperf_server_nosys](pico_w/wifi/freertos/iperf) | Runs an "iperf" server for WiFi speed testing under FreeRTOS in NO_SYS=1 mode. The LED is blinked in another task.
[picow_freertos_iperf_server_sys](pico_w/wifi/freertos/iperf) | Runs an "iperf" server for WiFi speed testing under FreeRTOS in NO_SYS=0 (i.e. full FreeRTOS integration) mode. The LED is blinked in another task.
[picow_freertos_ping_nosys](pico_w/wifi/freertos/ping) | Runs the lwip-contrib/apps/ping test app under FreeRTOS in NO_SYS=1 mode.
[picow_freertos_ping_sys](pico_w/wifi/freertos/ping) | Runs the lwip-contrib/apps/ping test app under FreeRTOS in NO_SYS=0 (i.e. full FreeRTOS integration) mode. The test app uses the lwIP _socket_ API in this case.
[picow_freertos_ntp_client_socket](pico_w/wifi/freertos/ntp_client_socket) | Connects to an NTP server using the LwIP Socket API with FreeRTOS in NO_SYS=0 (i.e. full FreeRTOS integration) mode.
[pico_freertos_httpd_nosys](pico_w/wifi/freertos/httpd) | Runs a LWIP HTTP server test app under FreeRTOS in NO_SYS=1 mode.
[pico_freertos_httpd_sys](pico_w/wifi/freertos/httpd) | Runs a LWIP HTTP server test app under FreeRTOS in NO_SYS=0 (i.e. full FreeRTOS integration) mode.
[picow_freertos_http_client_sys](pico_w/wifi/freertos/http_client) | Demonstrates how to make a https request in NO_SYS=0 (i.e. full FreeRTOS integration) mode.

### Pico Bluetooth

These Bluetooth examples are only available for boards that support Bluetooth.
They are examples from the Blue Kitchen Bluetooth stack, see [here](https://bluekitchen-gmbh.com/btstack/#examples/examples/index.html) for a full description.

By default, the Bluetooth examples are only built in one "mode" only (*background*, *poll*, or *freertos*), with the 
default being *background*. This can be changed by passing `-DBTSTACK_EXAMPLE_TYPE=poll` etc. to `CMake`, or all 
examples can be built (which may be slow) by passing `-DBTSTACK_EXAMPLE_TYPE=all`
Freertos versions can only be built if `FREERTOS_KERNEL_PATH` is defined.

The Bluetooth examples that use audio require code in [pico-extras](https://github.com/raspberrypi/pico-extras). Pass `-DPICO_EXTRAS_PATH=${HOME}/pico-extras` on the cmake command line or define `PICO_EXTRAS_PATH=${HOME}/pico-extras` in your environment and re-run cmake to include them in the build.

App|Description
---|---
[picow_bt_example_a2dp_sink_demo](https://github.com/bluekitchen/btstack/tree/master/example/a2dp_sink_demo.c) | A2DP Sink - Receive Audio Stream and Control Playback.
[picow_bt_example_a2dp_source_demo](https://github.com/bluekitchen/btstack/tree/master/example/a2dp_source_demo.c) | A2DP Source - Stream Audio and Control Volume.
[picow_bt_example_ancs_client_demo](https://github.com/bluekitchen/btstack/tree/master/example/ancs_client_demo.c) | LE ANCS Client - Apple Notification Service.
[picow_bt_example_att_delayed_response](https://github.com/bluekitchen/btstack/tree/master/example/att_delayed_response.c) | LE Peripheral - Delayed Response.
[picow_bt_example_audio_duplex](https://github.com/bluekitchen/btstack/tree/master/example/audio_duplex.c) | Audio Driver - Forward Audio from Source to Sink.
[picow_bt_example_avrcp_browsing_client](https://github.com/bluekitchen/btstack/tree/master/example/avrcp_browsing_client.c) | AVRCP Browsing - Browse Media Players and Media Information.
[picow_bt_example_dut_mode_classic](https://github.com/bluekitchen/btstack/tree/master/example/dut_mode_classic.c) | Testing - Enable Device Under Test (DUT.c) Mode for Classic.
[picow_bt_example_gap_dedicated_bonding](https://github.com/bluekitchen/btstack/tree/master/example/gap_dedicated_bonding.c) | GAP bonding.
[picow_bt_example_gap_inquiry](https://github.com/bluekitchen/btstack/tree/master/example/gap_inquiry.c) | GAP Classic Inquiry.
[picow_bt_example_gap_le_advertisements](https://github.com/bluekitchen/btstack/tree/master/example/gap_le_advertisements.c) | GAP LE Advertisements Scanner.
[picow_bt_example_gap_link_keys](https://github.com/bluekitchen/btstack/tree/master/example/gap_link_keys.c) | GAP Link Key Management (Classic.c).
[picow_bt_example_gatt_battery_query](https://github.com/bluekitchen/btstack/tree/master/example/gatt_battery_query.c) | GATT Battery Service Client.
[picow_bt_example_gatt_browser](https://github.com/bluekitchen/btstack/tree/master/example/gatt_browser.c) | GATT Client - Discover Primary Services.
[picow_bt_example_gatt_counter](https://github.com/bluekitchen/btstack/tree/master/example/gatt_counter.c) | GATT Server - Heartbeat Counter over GATT.
[picow_bt_example_gatt_device_information_query](https://github.com/bluekitchen/btstack/tree/master/example/gatt_device_information_query.c) | GATT Device Information Service Client.
[picow_bt_example_gatt_heart_rate_client](https://github.com/bluekitchen/btstack/tree/master/example/gatt_heart_rate_client.c) | GATT Heart Rate Sensor Client.
[picow_bt_example_gatt_streamer_server](https://github.com/bluekitchen/btstack/tree/master/example/gatt_streamer_server.c) | Performance - Stream Data over GATT (Server.c).
[picow_bt_example_hfp_ag_demo](https://github.com/bluekitchen/btstack/tree/master/example/hfp_ag_demo.c) | HFP AG - Audio Gateway.
[picow_bt_example_hfp_hf_demo](https://github.com/bluekitchen/btstack/tree/master/example/hfp_hf_demo.c) | HFP HF - Hands-Free.
[picow_bt_example_hid_host_demo](https://github.com/bluekitchen/btstack/tree/master/example/hid_host_demo.c) | HID Host Classic.
[picow_bt_example_hid_keyboard_demo](https://github.com/bluekitchen/btstack/tree/master/example/hid_keyboard_demo.c) | HID Keyboard Classic.
[picow_bt_example_hid_mouse_demo](https://github.com/bluekitchen/btstack/tree/master/example/hid_mouse_demo.c) | HID Mouse Classic.
[picow_bt_example_hog_boot_host_demo](https://github.com/bluekitchen/btstack/tree/master/example/hog_boot_host_demo.c) | HID Boot Host LE.
[picow_bt_example_hog_host_demo](https://github.com/bluekitchen/btstack/tree/master/example/hog_host_demo.c) | HID Host LE.
[picow_bt_example_hog_keyboard_demo](https://github.com/bluekitchen/btstack/tree/master/example/hog_keyboard_demo.c) | HID Keyboard LE.
[picow_bt_example_hog_mouse_demo](https://github.com/bluekitchen/btstack/tree/master/example/hog_mouse_demo.c) | HID Mouse LE.
[picow_bt_example_hsp_ag_demo](https://github.com/bluekitchen/btstack/tree/master/example/hsp_ag_demo.c) | HSP AG - Audio Gateway.
[picow_bt_example_hsp_hs_demo](https://github.com/bluekitchen/btstack/tree/master/example/hsp_hs_demo.c) | HSP HS - Headset.
[picow_bt_example_le_credit_based_flow_control_mode_client](https://github.com/bluekitchen/btstack/tree/master/example/le_credit_based_flow_control_mode_client.c) | LE Credit-Based Flow-Control Mode Client - Send Data over L2CAP.
[picow_bt_example_le_credit_based_flow_control_mode_server](https://github.com/bluekitchen/btstack/tree/master/example/le_credit_based_flow_control_mode_server.c) | LE Credit-Based Flow-Control Mode Server - Receive data over L2CAP.
[picow_bt_example_led_counter](https://github.com/bluekitchen/btstack/tree/master/example/led_counter.c) | Hello World - Blinking a LED without Bluetooth.
[picow_bt_example_le_mitm](https://github.com/bluekitchen/btstack/tree/master/example/le_mitm.c) | LE Man-in-the-Middle Tool.
[picow_bt_example_le_streamer_client](https://github.com/bluekitchen/btstack/tree/master/example/le_streamer_client.c) | Performance - Stream Data over GATT (Client.c).
[picow_bt_example_mod_player](https://github.com/bluekitchen/btstack/tree/master/example/mod_player.c) | Audio Driver - Play 80's MOD Song.
[picow_bt_example_nordic_spp_le_counter](https://github.com/bluekitchen/btstack/tree/master/example/nordic_spp_le_counter.c) | LE Nordic SPP-like Heartbeat Server.
[picow_bt_example_nordic_spp_le_streamer](https://github.com/bluekitchen/btstack/tree/master/example/nordic_spp_le_streamer.c) | LE Nordic SPP-like Streamer Server.
[picow_bt_example_sdp_general_query](https://github.com/bluekitchen/btstack/tree/master/example/sdp_general_query.c) | SDP Client - Query Remote SDP Records.
[picow_bt_example_sdp_rfcomm_query](https://github.com/bluekitchen/btstack/tree/master/example/sdp_rfcomm_query.c) | SDP Client - Query RFCOMM SDP record.
[picow_bt_example_sine_player](https://github.com/bluekitchen/btstack/tree/master/example/sine_player.c) | Audio Driver - Play Sine.
[picow_bt_example_sm_pairing_central](https://github.com/bluekitchen/btstack/tree/master/example/sm_pairing_central.c) | LE Central - Test Pairing Methods.
[picow_bt_example_sm_pairing_peripheral](https://github.com/bluekitchen/btstack/tree/master/example/sm_pairing_peripheral.c) | LE Peripheral - Test Pairing Methods.
[picow_bt_example_spp_and_gatt_counter](https://github.com/bluekitchen/btstack/tree/master/example/spp_and_gatt_counter.c) | Dual Mode - SPP and LE Counter.
[picow_bt_example_spp_and_gatt_streamer](https://github.com/bluekitchen/btstack/tree/master/example/spp_and_gatt_streamer.c) | Dual Mode - SPP and LE streamer.
[picow_bt_example_spp_counter](https://github.com/bluekitchen/btstack/tree/master/example/spp_counter.c) | SPP Server - Heartbeat Counter over RFCOMM.
[picow_bt_example_spp_flowcontrol](https://github.com/bluekitchen/btstack/tree/master/example/spp_flowcontrol.c) | SPP Server - RFCOMM Flow Control.
[picow_bt_example_spp_streamer_client](https://github.com/bluekitchen/btstack/tree/master/example/spp_streamer_client.c) | Performance - Stream Data over SPP (Client.c).
[picow_bt_example_spp_streamer](https://github.com/bluekitchen/btstack/tree/master/example/spp_streamer.c) | Performance - Stream Data over SPP (Server.c).
[picow_bt_example_ublox_spp_le_counter](https://github.com/bluekitchen/btstack/blob/master/example/ublox_spp_le_counter.c) | LE u-blox SPP-like Heartbeat Server.

Some standalone Bluetooth examples (without all the common example build infrastructure) are also available:

App|Description
---|---
[picow_ble_temp_sensor](pico_w/bt/standalone) | Reads from the on board temperature sensor and sends notifications via BLE.
[picow_ble_temp_sensor_with_wifi](pico_w/bt/standalone) | Same as above but also connects to Wi-Fi and starts an "iperf" server.
[picow_ble_temp_reader](pico_w/bt/standalone) | Connects to one of the above "sensors" and reads the temperature.

### PIO

App|Description
---|---
[hello_pio](pio/hello_pio) | Absolutely minimal example showing how to control an LED by pushing values into a PIO FIFO.
[pio_apa102](pio/apa102) | Rainbow pattern on a string of APA102 addressable RGB LEDs.
[pio_clocked_input](pio/clocked_input) | Shift in serial data, sampling with an external clock.
[pio_differential_manchester](pio/differential_manchester) | Send and receive differential Manchester-encoded serial (BMC).
[pio_hub75](pio/hub75) | Display an image on a 128x64 HUB75 RGB LED matrix.
[pio_i2c_bus_scan](pio/i2c) | Scan an I2C bus.
[pio_ir_loopback](pio/ir_nec) | Sending and receiving IR (infra-red) codes using the PIO.
[pio_logic_analyser](pio/logic_analyser) | Use PIO and DMA to capture a logic trace of some GPIOs, whilst a PWM unit is driving them.
[pio_manchester_encoding](pio/manchester_encoding) | Send and receive Manchester-encoded serial.
[pio_onewire](pio/onewire)| A library for interfacing to 1-Wire devices, with an example for the DS18B20 temperature sensor.
[pio_blink](pio/pio_blink) | Set up some PIO state machines to blink LEDs at different frequencies, according to delay counts pushed into their FIFOs.
[pio_pwm](pio/pwm) | Pulse width modulation on PIO. Use it to gradually fade the brightness of an LED.
[pio_quadrature_encoder](pio/quadrature_encoder) | A quadrature encoder using PIO to maintain counts independent of the CPU. 
[pio_quadrature_encoder_substep](pio/quadrature_encoder_substep) | High resolution speed measurement using a standard quadrature encoder.
[pio_spi_flash](pio/spi) | Use PIO to erase, program and read an external SPI flash chip.
[pio_spi_loopback](pio/spi) | Use PIO to run a loopback test with all four CPHA/CPOL combinations.
[pio_squarewave](pio/squarewave) | Drive a fast square wave onto a GPIO. This example accesses low-level PIO registers directly, instead of using the SDK functions.
[pio_squarewave_div_sync](pio/squarewave) | Generates a square wave on three GPIOs and synchronises the divider on all the state machines.
[pio_st7789_lcd](pio/st7789_lcd) | Set up PIO for 62.5 Mbps serial output, and use this to display a spinning image on a ST7789 serial LCD.
[pio_uart_dma](pio/uart_dma) | Send and receive data from a UART implemented using the PIO and DMA.
[pio_uart_rx](pio/uart_rx) | Implement the receive component of a UART serial port. Attach it to the spare Arm UART to see it receive characters.
[pio_uart_rx_intr](pio/uart_rx) | Implement the receive component of a UART serial port with an interrupt for received characters. Attach it to the spare Arm UART to see it receive characters.
[pio_uart_tx](pio/uart_tx) | Implement the transmit component of a UART serial port, and print hello world.
[pio_ws2812](pio/ws2812) | Example of driving a string of WS2812 addressable RGB LEDs.
[pio_ws2812_parallel](pio/ws2812) | Examples of driving multiple strings of WS2812 addressable RGB LEDs efficiently.
[pio_addition](pio/addition) | Add two integers together using PIO. Only around 8 billion times slower than Cortex-M0+.

### PWM

App|Description
---|---
[hello_pwm](pwm/hello_pwm) | Minimal example of driving PWM output on GPIOs.
[led_fade](pwm/led_fade) | Fade an LED between low and high brightness. An interrupt handler updates the PWM slice's output level each time the counter wraps.
[measure_duty_cycle](pwm/measure_duty_cycle) | Drives a PWM output at a range of duty cycles, and uses another PWM slice in input mode to measure the duty cycle.

### Reset

App|Description
---|---
[hello_reset](reset/hello_reset) | Perform a hard reset on some peripherals, then bring them back up.

### RTC (RP2040 Only)

App|Description
---|---
[hello_rtc](rtc/hello_rtc) | Set a date/time on the RTC, then repeatedly print the current time, 10 times per second, to show it updating.
[rtc_alarm](rtc/rtc_alarm) | Set an alarm on the RTC to trigger an interrupt at a date/time 5 seconds into the future.
[rtc_alarm_repeat](rtc/rtc_alarm_repeat) | Trigger an RTC interrupt once per minute.

### SHA-256 (RP235x Only)

App|Description
---|---
[hello_sha256](sha/sha256) | Demonstrates how to use the pico_sha256 library to calculate a checksum using the hardware in RP2350.
[mbedtls_sha256](sha/mbedtls_sha256) | Demonstrates using the SHA-256 hardware acceleration in MbedTLS.

### SPI

App|Description
---|---
[bme280_spi](spi/bme280_spi) | Attach a BME280 temperature/humidity/pressure sensor via SPI.
[mpu9250_spi](spi/mpu9250_spi) | Attach a MPU9250 accelerometer/gyroscope via SPI.
[spi_dma](spi/spi_dma) | Use DMA to transfer data both to and from the SPI simultaneously. The SPI is configured for loopback.
[spi_flash](spi/spi_flash) | Erase, program and read a serial flash device attached to one of the SPI controllers.
[spi_master_slave](spi/spi_master_slave) | Demonstrate SPI communication as master and slave.
[max7219_8x7seg_spi](spi/max7219_8x7seg_spi) | Attaching a Max7219 driving an 8 digit 7 segment display via SPI.
[max7219_32x8_spi](spi/max7219_32x8_spi) | Attaching a Max7219 driving an 32x8 LED display via SPI.

### Status LED

App|Description
---|---
[status_blink](status_led/status_blink) | Blink the onboard LED using the status_led API.
[color_blink](status_led/color_blink) | Blink the onboard colored (WS2812) LED using the colored_status_led API if supported by the board.

### System

App|Description
---|---
[boot_info](system/boot_info) | Demonstrate how to read and interpret sys info boot info (RP235x only).
[hello_double_tap](system/hello_double_tap) | An LED blink with the `pico_bootsel_via_double_reset` library linked. This enters the USB bootloader when it detects the system being reset twice in quick succession, which is useful for boards with a reset button but no BOOTSEL button.
[rand](system/rand) | Demonstrate how to use the pico random number functions.
[narrow_io_write](system/narrow_io_write) | Demonstrate the effects of 8-bit and 16-bit writes on a 32-bit IO register.
[unique_board_id](system/unique_board_id) | Read the 64 bit unique ID from external flash (RP2040) or OTP (RP235x), which serves as a unique identifier for the board.

### Timer

App|Description
---|---
[hello_timer](timer/hello_timer) | Set callbacks on the system timer, which repeat at regular intervals. Cancel the timer when we're done.
[periodic_sampler](timer/periodic_sampler) | Sample GPIOs in a timer callback, and push the samples into a concurrency-safe queue. Pop data from the queue in code running in the foreground.
[timer_lowlevel](timer/timer_lowlevel) | Example of direct access to the timer hardware. Not generally recommended, as the SDK may use the timer for IO timeouts.

### UART

App|Description
---|---
[hello_uart](uart/hello_uart) | Print some text from one of the UART serial ports, without going through `stdio`.
[lcd_uart](uart/lcd_uart) | Display text and symbols on a 16x02 RGB LCD display via UART.
[uart_advanced](uart/uart_advanced) | Use some other UART features like RX interrupts, hardware control flow, and data formats other than 8n1.

### Universal

These are examples of how to build universal binaries which run on RP2040, and RP2350 Arm & RISC-V.
These require you to set `PICO_ARM_TOOLCHAIN_PATH` and `PICO_RISCV_TOOLCHAIN_PATH` to appropriate paths, to ensure you have compilers for both architectures.

App|Description
---|---
[blink_universal](universal/CMakeLists.txt#L126) | Same as the [blink](blink) example, but universal.
[hello_universal](universal/hello_universal) | The obligatory Hello World program for Pico (USB and serial output). On RP2350 it will reboot to the other architecture after every 10 prints.
[nuke_universal](universal/CMakeLists.txt#L132) | Same as the [nuke](flash/nuke) example, but universal. On RP2350 runs as a packaged SRAM binary, so it is written to flash and copied to SRAM by the bootloader.

### USB Device

#### TinyUSB Examples 

Most of the USB device examples come directly from the TinyUSB device examples directory [here](https://github.com/hathach/tinyusb/tree/master/examples/device).
Those that are supported on RP2040 and RP2350 devices are automatically included as part of the pico-examples
build as targets named `tinyusb_dev_<example_name>`, e.g. https://github.com/hathach/tinyusb/tree/master/examples/device/hid_composite
is built as `tinyusb_dev_hid_composite`.

At the time of writing, these examples are available:

- tinyusb_dev_audio_4_channel_mic
- tinyusb_dev_audio_test
- tinyusb_dev_board_test
- tinyusb_dev_cdc_dual_ports
- tinyusb_dev_cdc_msc
- tinyusb_dev_dfu
- tinyusb_dev_dfu_runtime
- tinyusb_dev_dynamic_configuration
- tinyusb_dev_hid_composite
- tinyusb_dev_hid_generic_inout
- tinyusb_dev_hid_multiple_interface
- tinyusb_dev_midi_test
- tinyusb_dev_msc_dual_lun
- tinyusb_dev_net_lwip_webserver
- tinyusb_dev_uac2_headset
- tinyusb_dev_usbtmc
- tinyusb_dev_video_capture
- tinyusb_dev_webusb_serial

Whilst these examples ably demonstrate how to use TinyUSB in device mode, their `CMakeLists.txt` is set up in a way
tailored to how TinyUSB builds their examples within their source tree.

For a better example of how to configure `CMakeLists.txt` for using TinyUSB in device mode with the Raspberry Pi Pico SDK
see below:

#### SDK build example 
App|Description
---|---
[dev_hid_composite](usb/device/dev_hid_composite) | A copy of the TinyUSB device example with the same name, but with a CMakeLists.txt which demonstrates how to add a dependency on the TinyUSB device libraries with the Raspberry Pi Pico SDK.

#### Low Level example
App|Description
---|---
[dev_lowlevel](usb/device/dev_lowlevel) | A USB Bulk loopback implemented with direct access to the USB hardware (no TinyUSB).

#### Custom CDC with SDK stdio

This example demonstrates how to use the TinyUSB CDC device library to create two USB serial ports, and assign one of them to the SDK for stdio.

App|Description
---|---
[dev_multi_cdc](usb/device/dev_multi_cdc) | A USB CDC device example with two serial ports, one of which is used for stdio. The example exposes two serial ports over USB to the host. The first port is used for stdio, and the second port is used for a simple echo loopback. You can connect to the second port and send some characters, and they will be echoed back on the first port while you will receive a "OK\r\n" message on the second port indicating that the data was received.

### USB Host

All the USB host examples come directly from the TinyUSB host examples directory [here](https://github.com/hathach/tinyusb/tree/master/examples/host).
Those that are supported on RP2040 and RP2350 devices are automatically included as part of the pico-examples
build as targets named `tinyusb_host_<example_name>`, e.g. https://github.com/hathach/tinyusb/tree/master/examples/host/cdc_msc_hid
is built as `tinyusb_host_cdc_msc_hid`.

At the time of writing, there is only one host example available:

- tinyusb_host_cdc_msc_hid

### USB Dual Mode

USB Dual Mode uses PIO as a USB host controller and the RP2040/RP2350 USB controller as a device controller. All the USB dual examples come directly from the TinyUSB dual examples directory [here](https://github.com/hathach/tinyusb/tree/master/examples/dual).
Those that are supported on RP2040 and RP2350 devices are automatically included as part of the pico-examples
build as targets named `tinyusb_dual_<example_name>`, e.g. https://github.com/hathach/tinyusb/tree/master/examples/dual/host_hid_to_device_cdc
is built as `tinyusb_dual_host_hid_to_device_cdc`.

At the time of writing, there is only one dual mode example available:

- tinyusb_dual_host_hid_to_device_cdc

### Watchdog

App|Description
---|---
[hello_watchdog](watchdog/hello_watchdog) | Set the watchdog timer, and let it expire. Detect the reboot, and halt.
