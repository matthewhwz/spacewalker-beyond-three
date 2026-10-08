# When the right desktop appears on the wrong panel

The first six-screen hardware run created the expected virtual displays, but the physical Mac desktop appeared at the top left. The intended bottom-center panel was empty. Display creation had succeeded; the association between the physical source and its rendered panel was wrong.

## Four identities that looked interchangeable

The investigation had to distinguish an OS display ID, a logical source, a texture slot, and a panel's spatial position.

| Identity | Meaning |
| --- | --- |
| OS display ID | The identifier assigned to a connected display at runtime |
| Logical source | The application's identity for the captured desktop |
| Texture slot | The destination updated by frames from that source |
| Panel position | Where that texture is shown in the scene |

The OS identifier should be treated as a runtime value. A panel's position should be geometry. Neither is a reliable substitute for an explicit source-to-texture association.

The local system also had a special callback value for the physical display. Its resolver selected the first render specification. The initial layout put the top-left specification first, so the physical callback reached the wrong panel. The fix changed the relevant specification order while preserving each specification's complete source association and geometry.

That was a routing fix. Moving the top-left rectangle to the center would have hidden the symptom while changing the spatial arrangement of other content.

## Give every source recognizable content

A useful manual test is to put a different label on every desktop: physical Mac, upper-left, upper-center, and so on. Follow each label from its desktop to its rendered panel. A repeated wallpaper makes a swapped source much harder to notice.

For a new implementation, I would keep one mapping table that records the logical source, texture destination, and intended panel. Any special physical-display path should appear in that table and receive a dedicated test.

The regression check here exercised the actual source resolver and texture writes. A deliberately incorrect physical-to-upper-center association was also tested as a negative control. Detecting that wrong association mattered: a test that accepts every routing table cannot establish that the correct one works.

## An extra monitor changed the symptoms

A later misplaced or black center-panel symptom appeared with an external monitor connected. The user reported normal operation without that monitor. That observation does not identify a universal cause, but it demonstrates that the connected-display configuration belongs in the test record.

Test the physical source with and without an external monitor, then after a preset switch. Record which displays were connected. A result from one configuration should stay attached to that configuration.
