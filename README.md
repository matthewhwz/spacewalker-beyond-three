# SpaceWalker Beyond Three

### SpaceWalker supports 3 screens. I wanted 9.

SpaceWalker officially offers up to three screens on macOS.

But while experimenting with the app, I discovered something interesting: **a five-screen backend was already there.**

So I started pushing the limits.

**3 → 5 → 6 → 9 screens.**

And eventually, I built a 3 × 3 virtual desktop layout.

## The Experiment

It started with a simple question:

*What if three screens aren't enough?*

First, I explored the existing five-screen functionality.

Then I built a six-screen layout.

Then I added another row.

Nine screens. One Mac. One pair of XR glasses.

## What Went Wrong

Getting more screens to appear was only half the challenge.

- The Mac desktop appeared in the wrong corner
- Some panels overlapped even with zero spacing
- Head tracking stopped working after changing the app identity

Each problem had a different cause.

## The Result

I built selectable six-screen and nine-screen configurations, with the earlier six-screen setup preserved.

Six screens were confirmed on hardware. The nine-screen build passed implementation checks, but its final headset validation and performance measurements have not been documented.

Screen counts include the physical Mac display: the nine-screen layout uses eight virtual displays plus the Mac desktop.

This repository shares the experiment and technical lessons, not modified application binaries.

For mapping, geometry, calibration, and reproduction notes, see [TECHNICAL.md](TECHNICAL.md).
