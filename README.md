# VHS-Decode HSDAOH capture hardware

Low-cost **HSDAOH** capture hardware notes for **[VHS-Decode](https://github.com/oyvindln/vhs-decode)**: standardising
the common **AD9226** ADC module, **Pico 2** firmware, and a single-channel build (1× RF video + PCM1802 2 channel
audio) via an **MS2130/MS2130S** USB3 HDMI capture dongle.

---

## Start here

| I want to…                     | Go to                                                                          |
|--------------------------------|--------------------------------------------------------------------------------|
| See the full path end-to-end   | [Getting started](docs/getting-started.md) **[Under construction 🚧]**         |
| Order/build the capture device | [BOM and build](docs/bom-and-build.md) **[Under construction 🚧]**                                        |
| Fix my PCM1802 defects         | [PCM1802 fixes](docs/pcm1802-fixes.md)                                         |
| Modify the AD9226              | [AD9226 guide](docs/ad9226/index.md)                                           |
| Flash the Pico 2               | [Firmware](docs/firmware.md)                                                   |
| Print the case                 | [Case](docs/case.md)                                                           |
| Cable up and capture           | [Connect and capture](docs/connect-and-capture.md) **[Under construction 🚧]** |
| Fix problems                   | [Troubleshooting](docs/troubleshooting.md) **[Under construction 🚧]**         |
| Look up terms                  | [Glossary](docs/glossary.md) **[Under construction 🚧]**                       |


New to VHS-Decode? Read the [upstream wiki](https://github.com/oyvindln/vhs-decode/wiki) first, then return here for the
hardware deeper dive

---

## Quick path

1. Build / order single channel Pico 2 capture device
2. Fix known PCM1802 defects
3. Mod AD9226 module to fix clipping & setup gain (full mod recommended)
4. Flash Pico 2 UF2 (clipping LED firmware preferred)
5. Install MS2130 driver + MISRC GUI
6. Connect RF (and audio), set levels, capture

---

## Repository layout

| Path                                                                 | Contents                                                  |
|----------------------------------------------------------------------|-----------------------------------------------------------|
| [`README.md`](README.md)                                             | Overview and links (this file)                            |
| [`docs/`](docs/index.md)                                             | All guides (Markdown wiki)                                |
| [`case/`](case/)                                                     | STL files (`HSDAOH_case_base.stl`, `HSDAOH_case_lid.stl`) |
| [`rp2350_firmware/`](rp2350_firmware/)                               | UF2 binaries (stock + clipping LED)                       |
| [`initial_setup_and_modification/`](initial_setup_and_modification/) | Redirect to [`docs/ad9226/`](docs/ad9226/README.md)       |

---

## Design targets (AD9226)

| Item         | Typical target                                |
|--------------|-----------------------------------------------|
| Input level  | ~**650 mVpp** @ 50Ω-oriented setup            |
| Gain example | **~4x**                                       |
| Optional LPF | **82 pF** ≈ **10 MHz**, VHS / Video8 oriented |

Full procedure: [docs/ad9226/](docs/ad9226/README.md).

---

## External projects

- [oyvindln/vhs-decode](https://github.com/oyvindln/vhs-decode) — the entire decode stack and wiki
- [Sev5000/Pico2_12bitADC_PCMAudio](https://github.com/Sev5000/Pico2_12bitADC_PCMAudio) — main PCB, Gerbers, parts
- [Wren6991/Pico-DVI-Sock](https://github.com/Wren6991/Pico-DVI-Sock) — DVI/HDMI sock
- [harrypm/MISRC-GUI](https://github.com/harrypm/MISRC-GUI/releases) · [machcnz/HSDAOH-MISRC-GUI](https://github.com/machcnz/HSDAOH-MISRC-GUI) —
  capture UI