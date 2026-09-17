# Firmware (Pico 2)

UF2 images for the **Raspberry Pi Pico 2 (RP2350)** on the single-channel AD9226 + PCM1802 HSDAOH grabber.

Captured data goes **HDMI → MS2130**, not over the Pico USB data path. USB is for **BOOTSEL firmware flashing** only.

## Files

| File                                                                        | Role                                                                      |
|-----------------------------------------------------------------------------|---------------------------------------------------------------------------|
| [`clipping_led_firmware.uf2`](../rp2350_firmware/clipping_led_firmware.uf2) | **Recommended** — HSDAOH + Pico 2 **power LED** as ADC clipping indicator |
| [`stock_firmware.uf2`](../rp2350_firmware/stock_firmware.uf2)               | HSDAOH without the clipping LED behaviour                                 |

UF2 binaries are contained in `rp2350_firmware` folder

## Flashing Pico 2

1. Download a UF2
2. Make sure your Pico 2 is unplugged from any power source
2. Hold **BOOTSEL** button on the Pico 2, **then** connect USB to the PC
5. Release **BOOTSEL**
3. A mass-storage drive will appear (typically `RP2350`)
4. Copy the `.uf2` onto that drive; wait for it to disconnect and reboot (usually takes a few seconds)

MS2130 does **not** need to be connected to flash.

## After flashing

- Install the MS2130 driver and MISRC GUI, then cable up — see [Connect and capture](connect-and-capture.md). **[Under construction 🚧]**

> [!TIP]
> Use the clipping LED in conjunction with MISRC GUI while setting RF levels. Sustained glow usually
> means an input signal is too high (attenuate or lower preamp gain)

## Lineage

- Firmware family: [steve-m/hsdaoh-rp2350](https://github.com/steve-m/hsdaoh-rp2350)
- Carrier PCB: [Sev5000/Pico2_12bitADC_PCMAudio](https://github.com/Sev5000/Pico2_12bitADC_PCMAudio)

[Back](../README.md)
