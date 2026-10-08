# SpaceWalker Beyond Three — Exploring 5 to 9 Virtual Displays on macOS

A six-screen desktop can create every display successfully and still put the Mac's desktop on the wrong panel. That happened in this project. Another experimental build displayed the panels but stopped responding to head movement because its separate settings domain was missing device calibration.

These notes explain the engineering work behind a personal multi-screen experiment using VITURE SpaceWalker on macOS. The project progressed from five panels to a six-panel grid (3 × 2), then added a nine-panel grid (3 × 3). They describe the design, failures, and validation in fresh prose.

Throughout the series, five, six, and nine screens mean the total desktop panels, including the physical Mac display. The actual virtual-display counts were:

| Layout | Total desktop panels | Additional virtual displays |
| --- | --- | --- |
| Five-screen arrangement | 5 | 4 |
| Six-screen grid (3 × 2) | 6 | 5 |
| Nine-screen grid (3 × 3) | 9 | 8 |

This is an independent experience report, unaffiliated with VITURE. It is a documentation repository, not an application release or a patch distribution. It contains no application binaries, vendor source, decompiled code, disassembly, binary patches, SDK files, or extracted application resources. Product names identify the software used in the experiment.

## Read the series

| Article | What it covers |
| --- | --- |
| [01 — Building the multi-screen pipeline](01-multi-screen-pipeline.md) | Display creation, capture, textures, panel geometry, and head pose |
| [02 — When the right desktop appears on the wrong panel](02-display-mapping.md) | Separating OS IDs, logical sources, textures, and spatial positions |
| [03 — Arranging panels in 3D](03-panel-geometry.md) | Yaw, pitch, rotation order, touching edges, and extending the grid |
| [04 — A new app identity can lose its calibration](04-identity-and-calibration.md) | Independent experiments, permissions, settings, and frozen tracking |
| [05 — What the tests actually proved](05-validation-and-evidence.md) | Native checks, modeled services, negative controls, and hardware limits |
| [06 — Lessons for the next implementation](06-lessons-for-next-time.md) | An implementation sequence informed by the failures |

## Recorded status

The engineering records covered here end on October 7, 2026.

- The five-screen experiment and an earlier six-screen build received qualitative hardware acceptance on October 5, 2026.
- A later calibration fix received confirmation that left/right head movement and recentering worked.
- The final experimental app retained both six- and nine-screen presets. Native and model checks were recorded for both.
- Explicit hardware acceptance of the nine-screen preset was not recorded. No quantitative performance benchmark or per-frame head-pose measurement is presented here.

The test results belong to particular experimental builds. Earlier hardware feedback does not establish that every later build behaves identically.

For uploading this documentation as a separate repository, see [Publishing these notes](PUBLISHING.md).
