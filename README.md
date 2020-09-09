# Key2Blue

Morse code key to bluetooth gateway

## Install esp-idf

Follow [installation directions for esp-idf](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/get-started/index.html#installation-step-by-step)

- Remove the noted lines to create a toolchain with support for 64-bit
  time_t.
  
- I chose esp-idf tag "v4.1". (`git checkout v4.1`)

Might be good to run the "hello_world" example in the installation doc
to make sure you are functional.

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

Debugging coredumps:

Put the base64 encoded coredump (w/o the text header/footer) in a
file named `CORE`:

    cat > CORE

Print stack traces:

    espcoredump.py info_corefile \
      --core CORE --core-format b64 \
      build/key2blue.elf

Use GDB:

    espcoredump.py dbg_corefile \
      --core CORE --core-format b64 \
      build/key2blue.elf

See Also:

[Launching GDB with GDBStub](https://docs.espressif.com/projects/esp-idf/en/latest/esp32/api-guides/tools/idf-monitor.html#launching-gdb-with-gdbstub)

## Related Issues

* [hsp_hs_demo: not receiving HCI_EVENT_SCO_CAN_SEND_NOW?](https://groups.google.com/u/1/g/btstack-dev/c/HIE4FOeEkZc)

* [Trouble Sending SCO Audio](https://github.com/espressif/esp-idf/issues/1118)

## Other Resources

* [BTstack Repository](https://github.com/bluekitchen/btstack)

* [BTstack dev group](https://groups.google.com/g/btstack-dev/)

