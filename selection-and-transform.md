# Selection & Transform

## Selecting Actors

Only actors tagged `BuildPlaced` can be selected. There are two ways to select:

### Under Cursor / Crosshair

Call `SelectActorUnderCursor()`. This performs a line trace and selects the first `BuildPlaced` actor hit. The ghost preview is hidden while an actor is selected.

### Direct Selection

Call `SelectActor(AActor*)` to select a specific actor programmatically. The actor must have the `BuildPlaced` tag.

## Deselecting

Call `DeselectActor()` to clear the selection. The ghost preview reappears if build mode is still active.

## Deleting

Call `DeleteSelected()` to destroy the currently selected actor. This broadcasts `OnActorDeselected` and then removes the actor from the world. The ghost preview reappears afterward.

## Transform Modes

When an actor is selected, you can transform it using `ApplyTransformDelta(float Delta)`. The effect depends on the current mode and axis:

| Mode      | Effect per Delta Unit | Step Property   | Default |
| --------- | --------------------- | --------------- | ------- |
| Translate | Move along axis       | `TranslateStep` | 10 UU   |
| Rotate    | Rotate around axis    | `RotationStep`  | 15 deg  |
| Scale     | Scale along axis      | `ScaleStep`     | 0.1     |

### Cycling Modes

| Function               | Description                            |
| ---------------------- | -------------------------------------- |
| `CycleTransformMode()` | Translate > Rotate > Scale (cycles)    |
| `SetTransformMode()`   | Set directly to a specific mode        |

### Cycling Axes

| Function               | Description                            |
| ---------------------- | -------------------------------------- |
| `CycleTransformAxis()` | X > Y > Z (cycles)                    |

### Typical Usage

Bind mouse wheel scroll to `ApplyTransformDelta()`:

* Scroll up: `ApplyTransformDelta(1.0)` — moves/rotates/scales in the positive direction
* Scroll down: `ApplyTransformDelta(-1.0)` — moves/rotates/scales in the negative direction

> **\[Screenshot — Selected actor being rotated with the transform mode indicator visible in the UI]**
