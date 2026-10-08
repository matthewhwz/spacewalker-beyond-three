# Building the multi-screen pipeline

The first milestone was a five-panel arrangement. The next target was six desktop panels arranged in two rows, followed by an optional third row. In this experiment, the physical Mac display counted as one panel. Six total panels therefore required five virtual displays; nine required eight.

The local implementation extended an existing installed application in an isolated experimental copy. Its original implementation and modification machinery are excluded from this series. The useful part to share is how the display, capture, geometry, and tracking responsibilities fit together.

## The five-screen starting point

The earlier experiment exposed an existing five-screen backend in the local application. It created four virtual displays plus the physical Mac display. The user reported five visible screens with usable capture, rendering, and tracking; performance and clarity were described qualitatively as normal. Those observations were not an instrumented benchmark.

That milestone showed that the local pipeline could handle more than three panels. It did not establish that a new six- or nine-panel layout would work automatically. Extending the layout still required checking the storage, source associations, and geometry used by the downstream stages.

## Follow one desktop through the system

Each virtual display gives macOS a desktop surface. Capture produces frames for that surface. Those frames update a texture, and a panel in the AR scene displays that texture. Head pose changes the view of the scene.

| Stage | Responsibility | A failure that can survive a display-count check |
| --- | --- | --- |
| Display creation | Establish each desktop surface | Duplicate or missing display identity |
| Capture | Obtain frames from the intended desktop | Capturing the wrong source |
| Texture routing | Update the texture belonging to that source | Two panels sharing content |
| Panel geometry | Place and orient the textured rectangle | Correct content at the wrong location |
| View and tracking | Respond to head pose and recentering | A static view despite live desktop frames |

Counting displays only checks the first stage. A six-panel scene can contain six valid rectangles while its center panel is empty and its physical desktop appears somewhere else.

## Keep geometry separate from source identity

A panel needs both an identity and a pose. Moving it upward should change its position. It should retain its desktop source, capture association, and texture association.

I would make that separation explicit in a new implementation before working on visual spacing. It makes a geometry change easier to inspect and prevents a layout reorder from silently becoming a capture reorder. A disposable visualization with one static image can use a simpler model; a desktop system with independently changing sources benefits from explicit associations.

The nine-panel extension followed this principle: preserve the existing six associations and append three sources for the lower row. The six-panel preset remained available, so the extension could be checked against a working baseline.

## More panels bring more lifecycle work

The larger layout required storage for additional display objects, capture specifications, corner data, and textures. Capacity alone was insufficient. Each display needed its own object, and the storage needed consistent ownership during copying, switching presets, and destruction.

Creating nine panels once is a weaker test than switching from six to nine and back to six within the same process. The latter can expose stale captures, leftover textures, or objects that outlive the preset that created them.

Panel resolution and quality settings were preserved during the extension. That kept the experiment focused on layout and routing, but it also left the cost of the additional displays unresolved. The records do not establish a measured performance result for nine screens.
