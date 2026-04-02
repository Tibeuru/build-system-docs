# Getting Started

## Quick Start

Follow these steps to get build mode working in your game in under 5 minutes.

### 1. Add the Component

Open your character Blueprint (e.g., `BP_Lucy_Playable`) and add the **Build Mode Component**:

1. Open the Blueprint in the editor
2. Click **Add Component** in the Components panel
3. Search for **Build Mode Component**
4. Add it to your character

> **\[Screenshot — Components panel showing Build Mode Component added to a character Blueprint]**

### 2. Configure the Palette

In the Details panel of the component, expand **Build System > Palette** and add entries to the `BuildPalette` array:

1. Click the **+** button next to Build Palette to add an entry
2. Set the **Display Name** (e.g., "Wall", "Floor", "Pillar")
3. Set either the **Mesh** (for static mesh placement) or **Actor Class** (for spawning actor instances)
4. Optionally set a **Thumbnail** texture for UI display

> **\[Screenshot — Details panel showing BuildPalette array with several configured items]**

### 3. Bind Input Actions

Using Enhanced Input, bind your input actions to the component's functions in your character's Event Graph:

1. Get a reference to the Build Mode Component
2. Bind your desired input actions to the component functions

Here is a recommended input setup:

| Action            | Function                       | Description                         |
| ----------------- | ------------------------------ | ----------------------------------- |
| Toggle Build Mode | `ToggleBuildMode()`            | Enter or exit build mode            |
| Place / Confirm   | `PlaceItem()`                  | Place item at preview location      |
| Select            | `SelectActorUnderCursor()`     | Pick a placed actor under the aim   |
| Delete            | `DeleteSelected()`             | Remove the selected actor           |
| Next Item         | `CyclePaletteNext()`           | Next palette item                   |
| Previous Item     | `CyclePalettePrev()`           | Previous palette item               |
| Rotate Preview    | `RotatePreview(float)`         | Rotate preview yaw (pass degrees)   |
| Transform Delta   | `ApplyTransformDelta(float)`   | Adjust selected actor (mouse wheel) |
| Cycle Transform   | `CycleTransformMode()`         | Switch translate/rotate/scale       |
| Cycle Axis        | `CycleTransformAxis()`         | Switch X/Y/Z axis                   |
| Toggle Grid Snap  | `ToggleGridSnap()`             | Toggle grid snapping on/off         |

> **\[Screenshot — Blueprint Event Graph showing input actions connected to Build Mode Component functions]**

### 4. Test It

1. Press **Play** in the editor
2. Trigger your Toggle Build Mode input
3. A translucent ghost preview should appear at your crosshair
4. Use your Place input to spawn a permanent copy
5. Use your Select input to pick it, then transform or delete it

> **\[Screenshot — In-game view showing build mode active with a placed actor and the ghost preview]**

### 5. (Optional) Bind to Events

For UI integration, bind to the component's event dispatchers:

| Delegate                | Fires When                              |
| ----------------------- | --------------------------------------- |
| `OnBuildModeToggled`    | Build mode is entered or exited         |
| `OnPaletteItemChanged`  | The active palette item changes         |
| `OnActorPlaced`         | An actor is placed in the world         |
| `OnActorSelected`       | A placed actor is selected              |
| `OnActorDeselected`     | A placed actor is deselected or deleted |
| `OnTransformModeChanged`| The transform mode changes              |
| `OnGridSnapToggled`     | Grid snapping is toggled                |

> **\[Screenshot — Blueprint showing OnActorPlaced delegate bound to update a UI widget]**
