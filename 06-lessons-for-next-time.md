# Lessons for the next implementation

The most expensive confusion came from treating display count, content placement, and head tracking as one result. They failed independently. The six-screen mapping bug passed display creation, while the calibration incident left the scene visible but stopped its response to head movement.

If I were building a new multi-screen renderer that I owned, I would establish one complete source path before designing the full grid.

## Start with distinguishable sources

Get one desktop into one texture and one panel. Add a second desktop with visibly different content. Verify that updating one leaves the other's content intact, then add the physical-display source and any special callback handling.

Write down the source-to-texture associations before arranging panels. A stable logical identity should survive a change in spatial position or a different runtime OS display ID.

## Add the grid without rewriting the working path

Build the six-panel arrangement with explicit centers, orientations, and transformed corners. Record rotation order. Check every desktop label in its intended position before spending time on touching seams.

For nine panels, preserve the existing associations and append the lower row. Exercise six → nine → six in one session. Inspect counts and ownership during the transition as well as the final picture.

I would keep a known working preset until the larger one had hardware acceptance. For a throwaway static mockup, preserving multiple presets may be unnecessary; for this project it provided a practical regression reference.

## Capture the configuration with the result

An external monitor changed the observed symptoms in one experiment. Missing same-device calibration changed tracking in another. A useful test record therefore needs more than a screenshot.

Record the experimental version, connected displays, selected profile, calibration readiness, and whether the test used real services or substitutes. Include the behavior that was actually observed: source placement, head response, recentering, and preset switching.

## Keep references durable

Older experimental apps were later removed to reduce clutter. Some retained build and verification scripts still depended on those apps, making their historical commands unsuitable for immediate reuse.

A reference used by a test should have an explicit retention plan. In an implementation you own, preserve permitted fixtures or expected outputs independently of disposable builds. These public notes publish the lessons rather than the proprietary artifacts used locally.

## Keep the public repository focused

The shareable result is the explanation of the pipeline, the mapping failure, the geometry decisions, and the limits of the evidence. Raw app bundles, extracted resources, patch machinery, calibration files, and private logs are unnecessary for understanding those lessons.

Publish the documentation directory as its own repository. Keep the local experimental workspace separate so that a broad upload cannot accidentally include those artifacts.
