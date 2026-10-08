# What the tests actually proved

The nine-screen implementation passed checks that ran native instruction paths and checks that modeled parts of the environment. The project record still does not contain explicit nine-screen hardware acceptance.

Those two statements belong together. A passing allocation or routing test cannot establish that the real OS creates eight virtual displays or that the headset remains responsive under that load.

## The recorded checks

The final evidence recorded 14 nine-screen cases and 14 cases for the preserved six-screen behavior. Four native callback, resolver, and texture cases checked routing. A separate negative control checked an incorrect physical-display destination. Four transitions exercised six → nine → six in a shared virtual machine across height profiles and address relocation scenarios.

The numbers describe that project's verification runs. They are not frame-rate measurements, repeated hardware trials, or a standard coverage target.

Native allocation paths, ownership-envelope operations, callbacks, source resolution, and writes were exercised. Some OS services, array-runtime behavior, and graphics operations were modeled. Consequently, the results supported specific storage, lifecycle, and mapping claims under those conditions.

| Evidence | Supported conclusion | Remaining question |
| --- | --- | --- |
| Allocation and ownership checks | Expected objects and storage follow checked paths | Behavior of real system services |
| Resolver and texture-write checks | Checked sources reach their intended destinations | Live capture and actual graphics output |
| Geometry comparisons | Existing surfaces are preserved and new coordinates agree | Headset readability and comfort |
| Preset transitions | Checked transitions restore the expected counts and associations | Long-running real-device stability |
| Selector checks | The intended option routes to the intended preset | Complete hardware behavior after selection |

## Preserve a working reference

The nine-screen extension kept the six-screen preset available and preserved its implementation payload. That gave the regression checks a specific baseline: the older surfaces and associations should survive the extension.

A stable baseline makes failures easier to localize. If both the old and new layout fail after an extension, investigate shared setup and lifecycle paths before adjusting only the added panels.

## Make an incorrect result fail

The physical-display negative control intentionally used the wrong destination. Its rejection showed that the mapping check could distinguish a known routing error from the expected result.

The same idea is useful for counts and transitions. A check should reject a missing panel or a leftover texture after switching back. Returning success from the test process is only useful if the assertions can detect the defect being investigated.

## What hardware feedback covered

An earlier six-screen build received qualitative hardware acceptance. A later calibration repair received confirmation of left/right head movement and recentering. These observations were valuable, but they were attached to particular versions and configurations.

The next evidence needed for nine screens is a real-device session confirming nine distinct desktop sources, head movement, recentering, and switching back to six. Quantitative performance claims would additionally need recorded machine and device conditions, capture modes, measurement methods, and duration.
