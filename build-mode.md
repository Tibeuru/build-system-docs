# Build Mode

## Overview

Build Mode is the core placement system of the Build System plugin. When active, a line trace is performed each frame from the player's camera (crosshair) or mouse cursor to find a placement surface. A translucent ghost preview follows the hit point, showing exactly where the item will be placed.

{% hint style="info" %}
**\[Video — Build mode workflow: entering build mode, aiming at surfaces, placing items, cycling the palette]**
{% endhint %}

## Activating Build Mode

Call `ToggleBuildMode()` on the Build Mode Component to enter or exit build mode. You can also use `SetBuildModeActive(true/false)` for explicit control.

When build mode activates:

1. Component tick is enabled (traces begin each frame)
2. The first palette item is selected
3. A ghost preview spawns (for mesh-type items)

When build mode deactivates:

1. Any selected actor is deselected
2. The ghost preview is destroyed
3. Component tick is disabled (zero runtime cost)

## Placement Modes

### Mesh Mode

Set the **Mesh** field on a palette item to a `UStaticMesh`. The system:

1. Spawns an `ABuildPreviewActor` (translucent ghost) that follows the trace
2. On `PlaceItem()`, spawns a generic `AActor` with a `UStaticMeshComponent` attached
3. The placed actor is tagged `BuildPlaced`

### Actor Mode

Set the **Actor Class** field on a palette item to any `AActor` subclass. The system:

1. No preview ghost is shown (the class may have its own visuals)
2. On `PlaceItem()`, spawns an instance of the class at the trace hit point
3. The placed actor is tagged `BuildPlaced`

> Only one of Mesh or Actor Class needs to be set. If both are set, Mesh takes priority.

## Trace Configuration

The line trace can be configured in the component's Details panel:

| Property             | Default        | Description                                 |
| -------------------- | -------------- | ------------------------------------------- |
| `TraceDistance`       | 10,000 UU      | Maximum distance of the placement trace     |
| `TraceChannel`       | ECC\_Visibility | Collision channel for the trace             |
| `bUseCrosshairTrace` | true           | true = camera center, false = mouse cursor  |

## Grid Snapping

Toggle grid snapping with `ToggleGridSnap()`. When enabled, the preview position is rounded to the nearest grid point.

| Property           | Default | Description                    |
| ------------------ | ------- | ------------------------------ |
| `GridSize`         | 50.0 UU | Grid cell size (0 = disabled)  |
| `bGridSnapEnabled` | true    | Whether snapping is active     |

## Rotating the Preview

Call `RotatePreview(float YawDelta)` to rotate the ghost preview around the Z axis before placing. Pass positive values for clockwise, negative for counter-clockwise.

> **\[Screenshot — Ghost preview being rotated with grid snapping visible]**
