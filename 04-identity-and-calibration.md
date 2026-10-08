# A new app identity can lose its calibration

One experimental version stopped responding to head movement after it was given a separate application identity. The display layout was present, but the new settings domain was missing the working device calibration cache. Tracking initialization failed.

Restoring the missing same-device cache resolved that incident without changing the app binary or its signature. The user then confirmed normal left/right movement and recentering, and the logs showed SDK initialization. No per-frame pose measurements were collected.

## Isolation has two sides

Separate experimental identities were useful because the installed app and locally modified copies could otherwise compete for permission and launch registration. The earlier shared-identity arrangement produced permission confusion and launches of an unintended copy.

A separate identity also meant separate settings. A settings domain existing on disk did not prove that it contained the device data needed for tracking.

| State | What needed attention |
| --- | --- |
| App identity and path | Which experimental copy was actually running |
| Permission grants | Whether that identity had permission through normal macOS UI |
| Device calibration | Whether the same device's known working calibration was present |
| Layout preferences | Whether the experiment selected its intended preset |
| Logs | Whether capture and tracking initialized independently |

Permissions and calibration solve different problems. A successful permission prompt does not establish tracking readiness.

## Diagnose initialization before changing geometry

Frozen head movement initially looks like a rendering defect. Before changing panel transforms, check whether pose updates are arriving and whether the device initialized successfully. In this incident, missing calibration explained the failure more directly than the layout did.

The later experimental identities were populated with the working same-device calibration before first launch. The public notes omit those files and their contents because readers need the lesson, not another user's device data.

For an implementation you own, I would include an explicit calibration readiness check and make the initialization result visible. A minimal display-only prototype can defer this; a headset workflow needs it before meaningful tracking tests.

## Keep the user workflow simple

The final local workflow was to open the experimental app directly, choose a preset, and launch the desktop. Development scripts were optional tools for building and collecting evidence. They were not prerequisites for daily use.

That distinction matters when documenting a project. A troubleshooting command can be useful to a developer without becoming another step every user must perform.
