# Technical Notes

The project extended a local SpaceWalker experiment from five to six and nine desktop panels. These notes retain the implementation lessons without distributing the modified app or its patch machinery.

## Display mapping

The initial six-screen version created the expected displays, but the physical Mac desktop appeared at the top left and the intended bottom-center panel was empty. The physical-source callback followed a special resolver path that selected the first render specification. That specification belonged to the wrong panel.

Changing the relevant specification order fixed the association. Moving the rectangle would have moved the symptom around without correcting the routing.

Keep these identities separate:

| Identity | Purpose |
| --- | --- |
| Runtime OS display ID | Identifies the currently connected desktop surface |
| Logical source | Identifies the desktop within the application |
| Texture destination | Receives that source's frames |
| Spatial panel | Places the textured rectangle in the scene |

A geometry edit should retain the source and texture associations. A runtime OS display ID should be resolved when a display connects, rather than treated as a permanent panel index.

For an independent implementation, a simple association table can follow the spatial grid:

| Logical source | Six-panel position | Nine-panel position |
| --- | --- | --- |
| Virtual A | Upper left | Upper left |
| Virtual B | Upper center | Upper center |
| Virtual C | Upper right | Upper right |
| Virtual D | Bottom left | Middle left |
| Physical Mac | Bottom center | Middle center |
| Virtual E | Bottom right | Middle right |
| Virtual F | — | Lower left |
| Virtual G | — | Lower center |
| Virtual H | — | Lower right |

These letters describe an independent design, not the proprietary application's internal indices. Give every source its own texture, including the physical source. Preserve the first six associations when adding the lower row.

Use different desktop labels to check routing visually. The local regression checks also exercised the actual resolver and texture writes, and rejected a deliberately incorrect physical-to-upper-center association.

An external monitor changed the symptoms in a later experiment, so record the connected-display configuration when testing the physical-source path.

## Panel geometry

The experiment used the following orientations:

| Column or row | Orientation |
| --- | --- |
| Left / center / right | Yaw −22° / 0° / +22° |
| Upper row | Pitch −12° |
| Middle and lower rows | Pitch 0° |

For upper panels, apply pitch before yaw. The rotation order and pivot affect the transformed corners even when the angle values are identical.

The six-panel layout anchored its bottom-center panel to the physical Mac desktop. Extending it to nine kept that anchor fixed: the old bottom row became the middle row, and each new lower panel was a rigid translation of the corresponding middle panel.

**lower center = middle center + (0, −H, 0)**

H is the panel's scene-space height. In the recorded coordinate system, width was 1.152 and the two height profiles were 0.720 and 0.648. The physical anchor was at (0, 0, −0.5). These are local scene units, not a physical-distance or comfort recommendation.

Zero explicit spacing did not eliminate intersections between the upper surfaces. Side yaw combined with upper pitch produced triangular projected overlaps. The lower row added touching seams while retaining that earlier geometry.

Check transformed corners and shared edges, then inspect the scene from more than one view. Center coordinates alone cannot establish whether panels touch or intersect.

## Calibration and app identity

Independent experimental app identities avoided conflicts between the installed app and modified copies in permission and launch registration. They also created separate settings domains.

One new domain lacked the working same-device calibration cache, causing tracking initialization to fail. Restoring the missing cache resolved the incident without changing the binary or signature. Left/right head movement and recentering were then confirmed by the user.

For a renderer you own, distinguish permission readiness from device readiness. Grant permissions through normal macOS UI, check calibration before initializing tracking, and inspect pose updates before changing panel geometry to diagnose a frozen view. Another user's private calibration is not a reusable fixture.

## Reproducing the design

There is no public build command for the local SpaceWalker modification in this repository. The sequence below reproduces the design in an implementation you own; it is not a recipe that modifies the stock app.

1. **Establish one complete source path.** Capture one desktop, update one texture, and show it on one panel. Confirm that new frames arrive.
2. **Add distinct desktops.** Create virtual displays through a display backend available to your implementation. Resolve their runtime IDs and bind each captured source to its own texture. Check two visibly different desktops before increasing the count.
3. **Handle the physical desktop explicitly.** Define its logical source and texture destination. Test any special callback path rather than relying on creation order.
4. **Build the six-panel grid.** Use five virtual desktops plus the physical one. Define the panel centers, pivots, and rotation order; verify labels at all six positions.
5. **Extend to nine.** Append three virtual desktops and three panel records. Translate the middle row down by H to create the lower row. Keep the earlier associations intact.
6. **Integrate pose and lifecycle.** Check calibration, head movement, and recentering. Switch six → nine → six in one process; stop obsolete capture streams and release their display and texture resources.

You will need your own virtual-display backend, desktop-capture integration, textured-panel renderer, and compatible tracking integration. A different backend may impose different display-count or permission requirements.

Validate unique sources and textures, physical-source routing, both height profiles, and preset transitions. The local project's native/model checks covered those concerns; real display creation, live capture, headset behavior, and performance still require actual hardware testing.
