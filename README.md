# key2blue
Morse code key to bluetooth gateway

## Install esp-idf

Follow [installation directions for esp-idf](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/index.html#installation-step-by-step)

- Remove the noted lines to create a toolchain with support for 64-bit
  time_t.
  
- I chose esp-idf "v4.1".

Might be good to run the "hello_world" example in the installation doc
to make sure you are functionall.

## Install btstack

Directions are cribbed from [ESP32 Bluetooth: Using the BTstack library](https://techtutorialsx.com/2017/07/08/esp32-bluetooth-using-the-btstack-library/).

    cd $(YOUR_ESP_DIR)
    git clone --recurse-submodules git@github.com:bluekitchen/btstack.git
    cd btstack/port/esp32/
    ./create_examples.py

## Build

Env:

    # Setup the shell env once per shell session:
    . $(YOUR_ESP_DIR)/esp-idf/export.sh

Config:

    # Setup the shell env:
    . $(YOUR_ESP_DIR)/esp-idf/export.sh
    
    # Change to match your installation:
    export BTSTACK_ROOT=/usr/local/esp/btstack

    make menuconfig
    # SDK tool configuration -> Toolchain supports time_t wide 64-bits
    # Serial flasher config -> Default baud rate -> 921600
    # Serial flasher config -> Default serial port -> /dev/ttyUSB0

Build and Flash:

    make flash
    
Monitor:

    make monitor


## Other Resources

* [BTstack Repository](https://github.com/bluekitchen/btstack)

* [BTstack dev group](https://groups.google.com/g/btstack-dev/)

