# SpaceWalker Beyond Three — Exploring 5 to 9 Virtual Displays on macOS

**SpaceWalker originally offered up to three screens. I explored taking it to five, six, and nine.**

A personal macOS experiment: unlock an existing five-screen backend, build a **3 × 2 desktop**, then extend it to **3 × 3**.

## What I Built

### 3 → 5 → 6 → 9 screens

| Stage | Layout | What changed |
| --- | --- | --- |
| **3** | Original selectable layouts | The starting limit in the stock interface |
| **5** | Five-screen arrangement | Exposed an existing backend beyond the visible three-screen options |
| **6** | **3 × 2 grid** | Added a six-panel layout with the physical Mac desktop at bottom-center |
| **9** | **3 × 3 grid** | Added a lower row; kept the six-screen preset selectable |

The nine-screen arrangement:

| Upper left | Upper center | Upper right |
| :---: | :---: | :---: |
| **Middle left** | **Mac desktop** | **Middle right** |
| **Lower left** | **Lower center** | **Lower right** |

Screen counts include the physical Mac display: five, six, and nine panels require **four, five, and eight virtual displays**, respectively.

## How It Works

**Desktop source → capture → texture → 3D panel**

Each desktop feeds its own textured panel. Head tracking changes the view. Extending to nine meant adding three sources and panels while preserving the original six associations.

**Reproduction:** [TECHNICAL.md](TECHNICAL.md#reproducing-the-design) gives the implementation sequence for your own renderer. This repository contains documentation; cloning it does not modify SpaceWalker or unlock screens.

## Technical Challenges

- **Wrong desktop, wrong corner:** the physical display's special capture path needed an explicit render association.
- **Zero spacing, visible overlaps:** yaw and pitch made upper panels intersect. Touching edges needed a geometry check.
- **Frozen head tracking:** a separate app identity was missing its same-device calibration. Restoring it fixed initialization.

## Limitations

Five and six screens received qualitative hardware confirmation. Nine passed implementation checks; headset acceptance and measured performance remain unconfirmed.

Independent project, unaffiliated with VITURE. No vendor code, binaries, patches, or private calibration data are included.
