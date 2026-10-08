# Arranging panels in 3D

Removing explicit gaps did not produce a perfectly flat wall. The upper side panels still formed triangular overlaps in the projected view. Their yaw and pitch caused the surfaces to intersect even when the spacing parameters were zero.

That result was retained in the experiment. It was a consequence of the chosen geometry, rather than evidence that a hidden gap setting remained enabled.

## Position and orientation are separate choices

Each panel is a rectangle with a center and an orientation. Yaw turns it toward the viewer from the side. Pitch tilts it vertically. Translation moves the rectangle without changing its orientation.

The recorded layout used left, center, and right yaw angles of −22°, 0°, and +22°. The upper row used −12° pitch, while the middle and added lower rows used 0°. These are the experiment's chosen values, not a comfort recommendation for every headset or viewer.

The physical Mac panel anchored the layout. When the six-panel grid became a nine-panel grid, its former bottom row became the middle row. Keeping that anchor fixed avoided shifting the entire scene simply because another row had been added.

## Rotation order changes the corners

For the upper panels, pitch was applied before yaw. Reversing those operations would produce different corners. A drawing that lists the same angles but uses a different composition order is a different layout.

Specify the coordinate system, rotation order, and pivot before tuning offsets. Compare transformed corners and edges as well as centers. Two panels can have plausible centers and still intersect along their edges.

## Adding the third row

The lower row was built by translating each middle-row panel downward by one panel height. In the experiment's scene coordinates, its center was:

**lower center = middle center + (0, −H, 0)**

Here, H is the scene-space panel height. Orientation and width were preserved. The project had two height profiles, so the translation was checked for both rather than assuming one constant worked everywhere.

This extension preserved the existing six surfaces and made the new middle-to-lower seams straightforward to inspect. It did not remove the upper row's earlier intersections.

## Inspect three different views

A top view helps reveal yaw and horizontal relationships. A side view helps reveal pitch and vertical placement. A projected view shows what the arrangement looks like from one chosen camera position.

A touching edge in world space is different from a clean seam in a projection. Likewise, a projected overlap does not by itself identify whether the cause is geometry, perspective, or source routing. Head movement changes the projection, so one screenshot cannot settle every seam question.

For the next geometry change, I would inspect the transformed corners first, then the projection, and finally the headset. A static preview can establish the intended arrangement; it cannot establish comfort or readability in use.
