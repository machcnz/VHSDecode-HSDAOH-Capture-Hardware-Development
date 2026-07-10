# AD9226 Module modification for VHS-Decode - ADC Capture - ~600mVp-p@050 Ohm FS

> [!NOTE]  
> Revision 0.6<br>
> 09-07-2026

<!-- TOC -->
* [Fixing early ADC clipping](#fixing-early-adc-clipping)
* [Gain configuration](#gain-configuration)
* [Configuration notes](#configuration-notes)
  * [Gain table](#gain-table)
* [Modification](#modification)
  * [Gain setup](#gain-setup)
    * [Visual guide](#visual-guide)
  * [LPF and other improvements](#lpf-and-other-improvements)
  * [BOM](#bom)
<!-- TOC -->

## Fixing early ADC clipping

The design flaw is AD8183's _Pin 2_ `VCOM` being incorrectly connected 
to the AD9226 _Pin 37_ `VREF` = 2V.

Instead, the Opamp Pin 2 should be connected to AD9226 _Pin 45_ `CMLEVEL` = 2.5V.

This is a problem which limits the opamp signal swing from a full 2V swing, impacting gain 
and early ADC clipping.

The fix is to:
1. **Cut the track** between Pin 2 of AD8138 and Pin 37 of AD9226
2. **Continuity test** the track has been cut
3. **Add a** short **wire between C11** and **C42** - _This connects AD8138 Pin 2, to Pin 45 of AD9226_

![ADC-clip-fix-steps.jpg](assets/ADC-clip-fix-steps.jpg)

![ADC-clip-fix-done.jpg](assets/ADC-clip-fix-done.jpg)

## Gain configuration

## Configuration notes
* Target ADC input level for 650mVp-p - Gain set to ~4x gain
* R2 / R14 = 2.2kΩ
* R6 & R14 270Ω - **Do not change**

> [!NOTE]  
> SNR ~70dB<br>
> SINAD ~ 98/70dB<br>
> ENOB ~ 11bits

### Gain table

| Gain (times) | R2 & R14 (Ohm) | Vin (Vp-p) |
|--------------|----------------|------------|
| 1            | 560            | 2.5        |
| 1.2          | 680            | 2          |
| 1.7          | 910            | 1.5        |
| 2.5          | 1.2k           | 1          |
| 3            | 1.6k           | 0.9        |
| **4**            | **2.2k**           | **0.65**       |
| 4.1          | 2.4k           | 0.6        |

> [!CAUTION]
> **Values above 2.4k are not recommended** due to lower SNR

> [!TIP]
> Higher value rf/rg resistors lead to higher Johnson noise <br>
> Analogue Devices AD8138 does not recommend rf <= 5k, I suggest rf <= 3k

## Modification

**Stock variant**

![schematic-stock.jpg](assets/schematic-stock.JPG)

**Stock board view**

![ADC9226-stock-board-photo.jpg](assets/ADC9226-stock-board-photo.jpg)

### Gain setup

1. **R3, R5, R8, R17** - **Remove** 
2. **R8 or R17 or R3** — **Add** 56Ω resistor 
3. **R5** — **Add** 0Ω resistor _- Optionally taken from R25_ 
4. **R9 & R11** — **Replace** with 47Ω resistors 
5. **R2 & R14** — **Replace** with 2.2kΩ _- Recommended gain_ 
6. **R6 & R13** — **Replace** with 270Ω resistors 
7. **R16** — **Replace** with 27Ω resistor _- Provides DC offset balance_ 
8. **C3** — **Add** 12nF capacitor lifted at 45 deg in series with **R16**

#### Visual guide
<details>
  <summary>Step by step visual guide</summary
                                     
  ![gain-mod-step-1.jpg](assets/gain_mod_steps/gain-mod-step-1.jpg)
  ![gain-mod-step-2.jpg](assets/gain_mod_steps/gain-mod-step-2.jpg)
  ![gain-mod-step-3.jpg](assets/gain_mod_steps/gain-mod-step-3.jpg)
  ![gain-mod-step-4.jpg](assets/gain_mod_steps/gain-mod-step-4.jpg)
  ![gain-mod-step-5.jpg](assets/gain_mod_steps/gain-mod-step-5.jpg)
  ![gain-mod-step-6.jpg](assets/gain_mod_steps/gain-mod-step-6.jpg)
  ![gain-mod-step-7.jpg](assets/gain_mod_steps/gain-mod-step-7.jpg)
  ![gain-mod-step-8.jpg](assets/gain_mod_steps/gain-mod-step-8.jpg)
  
</details>

### LPF and other improvements

1. **R25** - **Replace** with 12nF capacitor 
2. **C6lpf** — **Add** on the AD9226 side and **across R9/R11** add 160pF _- Provides 1-pole -3db@10MHz LPF & ADC kickback suppression_ 
3. **C2a/b** — **Add** 2.2pF capacitor **in parallel** on top of **R2 & R14** _- Stability and slight LPF roll off_ 

![gain-mod-board-schematic.jpg](assets/schematic-gain-lpf-mod.JPG)

### BOM

| Type       | Value    | Ref        | Quantity |
|------------|----------|------------|----------|
| Resistor   | 27 Ohm   | R16        | 1        |
| Resistor   | 47 Ohm   | R9, R11    | 2        |
| Resistor   | 56 Ohm    | R17/R3-R25 | 1        |
| Resistor   | 270 Ohm    | R6, R13    | 2        |
| _Resistor_ | _2.2k Ohm_ | _R2, R14_  | _2_        |
| Capacitor  | 6.8 nF   | R16        | 1        |
| Capacitor  | 2.2 pF   | R2, R14    | 2        |
| Capacitor  | 160 pF   | R9/R11     | 1        |

> [!NOTE]  
> All SMD, 0805 size<br>
> Resistor tolerance: 5% or less<br>
> Capacitor voltage rating: 10V or more
