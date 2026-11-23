# Arcade Manifold

[English](README.md) | [中文](README_CN.md)

![Arcade Manifold in its 32HP wooden box](docs/images/01-finished-module.jpg)

**Arcade Manifold** is a passive 4-channel Eurorack module (32HP) designed by [Meng Qi](https://www.mengqimusic.com). It works as a signal router, momentary switch, passive mixer, multiple, and format jumbler — built around fast, tactile SANWA arcade buttons for live performance.

Because the circuit is completely passive, it requires no power supply and can be mounted in an unpowered controller skiff or a standalone 32HP wooden box.

---

## Features & Controls

The module consists of **4 identical channels** arranged in columns, plus a shared **ground banana jack** at the top center for referencing external banana-format modular systems (Buchla, Serge, Ciat-Lonbarde, etc.).

Each column is labeled top-to-bottom on the faceplate with four Chinese characters:

| Label | Meaning | Control / Jacks |
| :---: | :--- | :--- |
| **出** | Output | 6.35 mm (1/4"), 3.5 mm (1/8"), and 4 mm banana jack |
| **入** | Input | 6.35 mm (1/4"), 3.5 mm (1/8"), and 4 mm banana jack |
| **门** | Gate / Mode | DPDT toggle switch: **Normally Open** (press button to connect) or **Normally Closed** (press button to cut/mute) |
| **力** | Force / Action | **SANWA OBSF-24** 24 mm arcade pushbutton |

### Live Routing & Mixing

Using stackable banana cables, you can reconfigure the signal flow on the fly:

- **Pre-switch mixing (at the inputs):** Stack banana cables across channel inputs to mix signals before the switches, then route or punch that mix out to individual channels with the arcade buttons.
- **Post-switch mixing (at the outputs):** Stack banana cables across channel outputs to sum signals after the switches, using the arcade buttons to choose which voices enter the mix.
- **Format jumbling:** Bridge 3.5 mm Eurorack, 6.35 mm instruments/pedals, and 4 mm banana systems within any channel.
- **Multi-unit chaining:** Link multiple Arcade Manifold modules together across inputs, outputs, and ground — no power rails required.

---

## Circuit Overview

Each channel runs on an identical **Core PCB** mounted perpendicular to the **Faceplate PCB**.

- Every Core PCB holds **three 5.1 kΩ (1206) SMD resistors** (12 total for 4 channels):
  1. Between the input 6.35 mm / 3.5 mm jacks and the input banana pad (`Nana`)
  2. Between the input banana pad (`Nana`) and the toggle/button switch input
  3. Between the switch output and the output bus (`Nana` / 3.5 mm / 6.35 mm)
- In **Normally Open** mode, pressing the arcade button connects the channel input to the output.
- In **Normally Closed** mode, the signal passes through until the button is pressed, which shunts the internal switch node to ground. The series 5.1 kΩ resistors prevent external sources or passively mixed buses from shorting directly to ground.

---

## Repository Structure

```text
Arcade-Manifold/
├── README.md                                 # Project overview (English)
├── README_CN.md                              # Project overview (Chinese)
├── LICENSE                                   # MIT License
├── docs/
│   ├── diy-guide.md                          # Step-by-step assembly guide (English)
│   ├── diy-guide_CN.md                       # Step-by-step assembly guide (Chinese)
│   └── images/                               # Build photos & enclosure drawing preview
└── hardware/
    ├── BOM.csv                               # Complete Bill of Materials
    ├── core/
    │   ├── AM_Core_Gerbers.zip               # Ready-to-fab Gerber package (order 4x)
    │   ├── Arcade Manifold.lay6              # Sprint-Layout 6 source file
    │   └── gerbers/                          # Extracted Gerber & drill files
    ├── faceplate/
    │   ├── AM_Faceplate_Gerbers.zip          # Ready-to-fab Gerber package (order 1x)
    │   ├── AM Faceplate.lay6                 # Sprint-Layout 6 source file
    │   └── gerbers/                          # Extracted Gerber & drill files
    └── enclosure/
        └── AM_Box_32HP.ai                    # 32HP wooden box drawing (Illustrator / PDF)
```

---

## Bill of Materials (BOM)

Machine-readable file: [`hardware/BOM.csv`](hardware/BOM.csv)

| Component | Brand / Model | Qty | Notes |
| :--- | :--- | :---: | :--- |
| Core PCB | Custom (`AM Core`) | 4 | 80.96 × 22.86 mm, 2-layer, 1.6 mm FR4 (1 per channel) |
| Faceplate PCB | Custom (`AM Faceplate`) | 1 | 162.5 × 128.7 mm (32HP × 3U), 2-layer, 1.6 mm FR4 |
| 5.1 kΩ SMD Resistor (1206) | Generic (`5K1 1206`) | 12 | 3 per Core PCB (all 3 resistor pads populated with 5.1 kΩ) |
| 24 mm Arcade Pushbutton | **SANWA** `OBSF-24` | 4 | Snap-in, 1 per channel |
| DPDT ON-ON Toggle Switch | **Dailywell** `2MD1T2B2M7QE` | 4 | Sub-miniature, vertical right-angle PC thru-hole, 1 per channel |
| 6.35 mm (1/4") PCB Jack | **Neutrik** (Yongsheng) `YS-215A` | 8 | 2 per Core PCB (Input & Output) |
| 3.5 mm (1/8") PCB Jack | Generic `PJ-313` | 8 | Right-angle through-hole, 2 per Core PCB (Input & Output) |
| 4 mm Banana Jack | **RCI** `R1-16A` | 9 | Panel-mount; 8 signal (e.g. blue) + 1 ground at top center (e.g. black) |
| Solid-core Bare / Tinned Wire | Generic | as needed | ~0.5–0.8 mm wire for buttons, banana jacks, and top ground jack |
| 32HP Wooden Box *(optional)* | Custom | 1 | Omit if installing into a Eurorack case |

*Optional accessories:* Stackable 4 mm banana patch cables (original builds shipped with 5) and 4× M3 Eurorack mounting screws (or wood screws for the wooden box).

---

## PCB Fabrication Notes

Both PCBs were designed in **Sprint-Layout 6** (`.lay6`). Ready-to-upload Gerber archives are included:

- **Core PCB** — [`hardware/core/AM_Core_Gerbers.zip`](hardware/core/AM_Core_Gerbers.zip)
  - Dimensions: `80.96 × 22.86 mm`, 2-layer, 1.6 mm FR4
  - Quantity needed: **4 per unit** (standard 5-piece fab minimum gives 1 spare)
- **Faceplate PCB** — [`hardware/faceplate/AM_Faceplate_Gerbers.zip`](hardware/faceplate/AM_Faceplate_Gerbers.zip)
  - Dimensions: `162.5 × 128.7 mm` (32HP × 3U), 2-layer, 1.6 mm FR4
  - Quantity needed: **1 per unit**
  - Finish: Front legends (**出 / 入 / 门 / 力** and lotus emblem) and jack rings are exposed copper through solder-mask openings — **blue solder mask** with **HASL or ENIG** matches the original module.
  - Mechanical details: Includes 4 slotted Eurorack mounting holes (`5.2 × 3.2 mm`) and 9 double-D anti-rotation cutouts sized for `RCI R1-16A` banana jacks.

---

## Assembly Guide

See the step-by-step illustrated build instructions in **[`docs/diy-guide.md`](docs/diy-guide.md)**.

---

## Optional 32HP Wooden Enclosure

Source drawing: [`hardware/enclosure/AM_Box_32HP.ai`](hardware/enclosure/AM_Box_32HP.ai) *(Adobe Illustrator file with an embedded PDF stream — can be opened directly in standard PDF viewers)*.

![32HP wooden enclosure drawing](docs/images/05-enclosure-drawing.png)

> **Drawing note:** The file contains two box designs on one sheet. **Use the top drawing (`183 × 149 × 52 mm`)** for Arcade Manifold. The bottom `173 mm` box with side cutouts belongs to a separate 30HP module and should be ignored.

**32HP box dimensions (top drawing):**
- Outer dimensions: `183 × 149 × 52 mm` (open-top 5-sided box)
- Inner opening: `163 × 129 mm`, internal depth `42 mm`
- Wall thickness: `10 mm` charred radiata pine sides + `10 mm` laminated bottom panel (with engraved lotus emblem on the underside)
- Inner mounting rails (green): `8 mm` thick × `40 mm` tall (`2 mm` below the outer rim so the faceplate sits flush)

---

## License

Released under the [MIT License](LICENSE). Build and use these hardware files at your own risk.
