# T-DSP XLR 2×2 — Balanced XLR I/O Board

**Part of the [T-DSP](https://t-dsp.com) open modular audio platform.**

A simple balanced-audio I/O board: **two XLR inputs and two XLR outputs** for pro line-level signals. It hosts a [T-DSP TAC5212 pro audio module](https://github.com/t-dsp/t-dsp_tac5212_pro_audio_module), which handles the entire analog signal path. Audio and control (I2S + I2C) are carried over a ribbon cable to a separate [T-DSP](https://t-dsp.com) controller module — this board has no microcontroller of its own.

[![T-DSP XLR 2x2 - Top Isometric](https://t-dsp.github.io/t-dsp_XLR_2x2/renders/t-dsp_XLR_2x2-3D_blender_th_top_iso.png)](https://t-dsp.github.io/t-dsp_XLR_2x2/gallery.html)

| | |
|:---:|:---:|
| [![Top](https://t-dsp.github.io/t-dsp_XLR_2x2/renders/t-dsp_XLR_2x2-3D_blender_th_top.png)](https://t-dsp.github.io/t-dsp_XLR_2x2/gallery.html) | [![Bottom](https://t-dsp.github.io/t-dsp_XLR_2x2/renders/t-dsp_XLR_2x2-3D_blender_th_bottom.png)](https://t-dsp.github.io/t-dsp_XLR_2x2/gallery.html) |
| [![Front](https://t-dsp.github.io/t-dsp_XLR_2x2/renders/t-dsp_XLR_2x2-3D_blender_th_front.png)](https://t-dsp.github.io/t-dsp_XLR_2x2/gallery.html) | [![Rear](https://t-dsp.github.io/t-dsp_XLR_2x2/renders/t-dsp_XLR_2x2-3D_blender_th_rear.png)](https://t-dsp.github.io/t-dsp_XLR_2x2/gallery.html) |

**[View 3D Render Gallery](https://t-dsp.github.io/t-dsp_XLR_2x2/gallery.html)** -- interactive slideshow of all board views

## What It Is

This is a **balanced I/O carrier** for the T-DSP ecosystem. It exposes four panel-mount Neutrik XLR connectors and gives a [TAC5212 pro audio module](https://github.com/t-dsp/t-dsp_tac5212_pro_audio_module) a home:

- **2× XLR inputs** — balanced, pro line level, into the TAC5212 ADC
- **2× XLR outputs** — balanced, pro line level, from the TAC5212 DAC
- **TAC5212 module socket** — the codec daughter board mounts here and does all the analog work
- **Ribbon link** — I2S audio, I2C control, and power travel over a single 2×10 ribbon cable to the host controller

There is no microcontroller, DSP, or power supply on this board. It is purely the analog front panel: connectors, the codec module, and the cable to the brains.

## How It Fits Together

```
  XLR in  ─┐                                  ┌─ I2S (audio)
  XLR in  ─┼─►  TAC5212 module  ◄────ribbon───┼─ I2C (control)   ►  T-DSP controller
  XLR out ─┤      (this board)                └─ power              (Teensy-based)
  XLR out ─┘
```

The controller module runs the firmware and clocks; this board provides the balanced analog I/O and the codec that converts it.

## Features

### Audio I/O
- **2× balanced XLR input** — female XLR (Neutrik NC3FAH2), into the TAC5212 ADC
- **2× balanced XLR output** — male XLR (Neutrik NC3MAH), from the TAC5212 DAC
- Pro line-level signal path, handled entirely by the TAC5212 module

### Connectivity
- **TAC5212 module socket** — hosts the [T-DSP TAC5212 pro audio module](https://github.com/t-dsp/t-dsp_tac5212_pro_audio_module)
- **2×10 ribbon header** — carries I2S, I2C, and power to/from a T-DSP controller module

### Power
- Supplied from the host controller over the ribbon cable — no power input on this board

## Board Design

- **100 mm × 44 mm** PCB
- Built around the T-DSP audio module board-outline standard (50 × 34.5 mm module footprint)
- The TAC5212 module handles the entire analog signal path
- KiCad source files, full BOM, and CI-generated manufacturing outputs included
- Open source under CC BY-NC-SA 4.0

## Getting Started

### Hardware

1. Mount the **TAC5212 pro audio module** onto this board's module socket
2. Wire the four panel-mount **XLR connectors** (2 in, 2 out)
3. Connect the **2×10 ribbon cable** between this board and your T-DSP controller module
4. Power and clocks are provided by the controller over the ribbon — no separate supply needed

### Firmware

The TAC5212 codec is configured and clocked by the **host controller module**, not by this board. See [t-dsp_software](https://github.com/t-dsp/t-dsp_software) for the firmware that drives the codec over I2C and streams audio over I2S.

View the design files in your browser with KiCanvas: [Schematic](https://kicanvas.org/?github=https://github.com/t-dsp/t-dsp_XLR_2x2/blob/main/t-dsp_XLR_2x2.kicad_sch) | [PCB](https://kicanvas.org/?github=https://github.com/t-dsp/t-dsp_XLR_2x2/blob/main/t-dsp_XLR_2x2.kicad_pcb)

## Project Files

| Directory | Contents |
|-----------|----------|
| `/3d_models/` | 3D models for PCB components |
| `/lib_fp/` | Custom KiCad footprint libraries |
| `/lib_sch/` | Custom KiCad schematic symbol libraries |
| `/manufacturing/` | CI-generated manufacturing outputs (gerbers, BOM, pick & place, PDFs) |
| `/pages/` | [3D Render Gallery](https://t-dsp.github.io/t-dsp_XLR_2x2/gallery.html), [Interactive BOM](https://t-dsp.github.io/t-dsp_XLR_2x2/ibom.html) |

## Manufacturing

Manufacturing files are generated automatically by [KiBot](https://github.com/INTI-CMNB/KiBot) on every push to `main` and on tagged releases via GitHub Actions.

To order:
1. Download the latest `t-dsp_XLR_2x2-manufacturing-vX.X.zip` from [Releases](https://github.com/t-dsp/t-dsp_XLR_2x2/releases)
2. Upload gerbers and drill files to your PCB fab (JLCPCB, PCBWay, etc.)
3. Use the BOM and CPL files for JLCPCB SMT assembly

## About T-DSP

T-DSP is an open modular audio platform built around the Teensy microcontroller and the [Teensy Audio Library](https://www.pjrc.com/teensy/td_libs_Audio.html). This board is the balanced-I/O front end — a clean 2-in/2-out XLR interface that pairs a TAC5212 codec module with a T-DSP controller over a ribbon cable.

For a full desktop audio development platform with ESP32 UI, MIDI I/O, S/PDIF, RCA I/O, and multi-module TDM expansion, see the [T-DSP Desktop Pro](https://github.com/t-dsp/t-dsp_desktop_pro).

Learn more at [t-dsp.com](https://t-dsp.com).

## Status

Active development. If you build one, please open an issue or reach out.

## Contact

For consulting, custom audio hardware design, or commercial licensing, reach out via [LinkedIn](https://linkedin.com/in/jayshoe).

## License

[Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International (CC BY-NC-SA 4.0)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

Free to share and adapt for non-commercial purposes with attribution and same license on derivatives.
