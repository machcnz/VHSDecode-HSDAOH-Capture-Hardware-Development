# VHS-LD-Capture-Hardware-Development
Sharing of VHS-Decode hardware development with a focus standardizing the low cost [HSDAOH](https://github.com/steve-m/hsdaoh) AD9226 ADC module.

[ADC gain setup and module modification](initial_setup_and_modification/README.md) - a complete guide for gain setup and other improvements of AD9226  module

[Pico 2 firmware](rp2350_firmware/stock_firmware.uf2) - ready to flash .uf2 firmware

[Pico 2 clipping LED firmware](rp2350_firmware/clipping_led_firmware.uf2) - ready to flash .uf2 firmware with Power LED ADC Clipping indicator

[Case](case/README.md) - .stl files for printable case

[MISRC-GUI for HSDAOH](https://github.com/harrypm/MISRC/releases) - download and install the Windows release here.

## The high level steps to get up and running.
This guide assumes a basic understand of the concepts, hardware & software options and usage of the VHS decode's capture method.

[Otherwise, its best to start here first](https://github.com/oyvindln/vhs-decode/wiki)

### 1. Build a single AD9226 + Single PCM1802 - for RF Video capture and Analogue (Stereo) Audio
Credits to [Sev5000](https://github.com/Sev5000) - [Detailed board build, PCB Gerber files for manufacturer and components needed](https://github.com/Sev5000/Pico2_12bitADC_PCMAudio)
<br>
This Capture devce uses a USB 3.0 HDMI capture stick based on the MacroSilicon MS2130/MS2130S as an interface to tranfer and capture 
the Analogue-to-digital converter stream to PC or MAC.

I recommended following Sev's excellent parts list and approach - choose build your own or JCLPCB do all of the work.

**Bill of material:**
- 1x [This](https://github.com/Sev5000/Pico2_12bitADC_PCMAudio/blob/main/Gerber_Pico2_12bitADC.zip) PCB (Send the Gerber .zip to JLC, PCBWay, ..)
- 1x Raspberry Pi Pico 2
- 1x [AD9226](https://aliexpress.com/item/1005003038271519.html)
- 1x [PCM1802](https://aliexpress.com/item/1005006412873984.html) - take note below - important!
- 2x [RCA-105 or RCA-106](https://aliexpress.com/item/1005006152724809.html)
- 1x [PJ-324M 5P](https://aliexpress.com/item/1005006146950431.html)
- 1x 3pin 2.54mm pin header horizontal for the headswitch/overflow selection jumper
- 1x 9pin 2.54mm pin-socket header 
- 1x 2x10pin 2.54mm pin-socket header
- 1x 3pin 2.54mm pin header (remove the center pin for connecting R/L of the PCM1802)
- 1x 3pin 2.54mm pin-socket header (remove the center pin for connecting R/L of the PCM1802)


**No surface mount component variant**
- 1x DVI-Sock - This ready to use HDMI board, no component soldering is necessary.
                To obtain, order the adafruit DVI sock or Aliexpress have these
- 2x 15pin 2.54mm pin-socket header

 **or build-your-own HDMI Surface Mount Variant - Component difficulty warning)**:
- 1× Stewart SS-53000-001 connector (See [BOM](https://github.com/Wren6991/Pico-DVI-Sock#bill-of-materials) for details)
- 8× 0402 270 ohm resistors
- 5x 0805 100nF ceramic capacitors
- 2x 20pin 2.54mm pin-socket header (For socketed Pi Pico 2 only)


Additional Items needed:
- HDMI cable
- MS2130/MS2130S USB 3 capture device
- VCR w/head tap mod
- VCR Head tap
- SMA or BNC 50ohm Coax cable (for connection to VCR head tap amplifier and this capture board
- RCA-to-RCA Stereo audio cable, of  at least 0.5m length
- Optional: 10MHz Low pass filter and for less hassle with Amp gain setting & adjustment - one (Digital) attenuator with attenuation steps
            of atleast -5db, -15db, -20db

> [!CAUTION]
> The PCM1802 board needs MODE0 bridged *and* connected to 3.3V with a wire (Those boards have a design error)

![pcm-module-mode.jpg](assets/pcm-module-mode.jpg)

- 1x [DVI-Sock](https://github.com/Wren6991/Pico-DVI-Sock) for a flush fit with the pcb edge, otherwise the adafruit DVI sock works fine too
- 2x 15pin 2.54mm pin-socket header


### 2. Modify the AD9226/AD8138 Module

Refer to the [guide](initial_setup_and_modification/README.md) in this repo.

Recommend full modification - or - modify for gain & VHS-Decode ready, is your choice.


### 2. Flash the RPI PICO 3

- [Pico 2 HSDAOH firmware with clipping indicator](rp2350_firmware/clipping_led_firmware.uf2) (uses the built in PI PICO 2 Power LED)


### 3. Software install - misrc GUI & driver

- Use the [ready to install release](https://github.com/machcnz/HSDAOH-MISRC-GUI) of HSDAOH or build and install
- Install MS2130 Driver - zadig included in release with instruction readme.


### 4. Connect, test & capture



