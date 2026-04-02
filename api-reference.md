# API Reference

## UBuildModeComponent

The core component. Add to a Pawn or PlayerController.

### Build Mode Control

| Function                   | Returns | Description              |
| -------------------------- | ------- | ------------------------ |
| `ToggleBuildMode()`        | void    | Toggle build mode on/off |
| `SetBuildModeActive(bool)` | void    | Explicitly set state     |
| `IsBuildModeActive()`      | bool    | Query current state      |

### Palette

| Function                     | Returns | Description                |
| ---------------------------- | ------- | -------------------------- |
| `SetBuildPalette(TArray)`    | void    | Replace palette at runtime |
| `SelectPaletteItem(int32)`   | void    | Select by index            |
| `CyclePaletteNext()`        | void    | Next item (wraps)          |
| `CyclePalettePrev()`        | void    | Previous item (wraps)      |
| `GetCurrentPaletteItem(Out)` | bool    | Get active item            |

### Placement

| Function               | Returns  | Description        |
| ---------------------- | -------- | ------------------ |
| `PlaceItem()`          | AActor\* | Place current item |
| `RotatePreview(float)` | void     | Rotate preview yaw |

### Selection

| Function                   | Returns  | Description              |
| -------------------------- | -------- | ------------------------ |
| `SelectActorUnderCursor()` | AActor\* | Select actor under aim   |
| `SelectActor(AActor*)`     | void     | Select specific actor    |
| `DeselectActor()`          | void     | Clear selection          |
| `DeleteSelected()`         | void     | Delete selected actor    |

### Transform

| Function                      | Returns | Description                    |
| ----------------------------- | ------- | ------------------------------ |
| `CycleTransformMode()`       | void    | Cycle translate/rotate/scale   |
| `SetTransformMode(Mode)`     | void    | Set mode directly              |
| `CycleTransformAxis()`       | void    | Cycle X/Y/Z                    |
| `ApplyTransformDelta(float)` | void    | Apply delta to selected actor  |

### Grid

| Function           | Returns | Description          |
| ------------------ | ------- | -------------------- |
| `ToggleGridSnap()` | void    | Toggle grid snapping |

### Queries

| Function               | Returns            | Description                   |
| ---------------------- | ------------------ | ----------------------------- |
| `GetAllPlacedActors()` | TArray\<AActor\*>  | All actors tagged BuildPlaced |

### Configuration Properties

| Property             | Type               | Default         | Description                   |
| -------------------- | ------------------ | --------------- | ----------------------------- |
| `BuildPalette`       | TArray\<FBuildableItem> | Empty      | Items the player can place    |
| `GridSize`           | float              | 50.0            | Grid cell size in UU          |
| `bGridSnapEnabled`   | bool               | true            | Whether snapping is active    |
| `RotationStep`       | float              | 15.0            | Degrees per rotation step     |
| `ScaleStep`          | float              | 0.1             | Scale increment per step      |
| `TranslateStep`      | float              | 10.0            | Translation distance per step |
| `TraceDistance`       | float              | 10,000          | Max trace distance in UU      |
| `TraceChannel`       | ECollisionChannel  | ECC\_Visibility | Collision channel             |
| `bUseCrosshairTrace` | bool               | true            | Crosshair vs mouse cursor     |
| `PreviewColor`       | FLinearColor       | Blue 50% alpha  | Ghost preview tint color      |

### Delegates

| Delegate                | Parameters                        | Fires When                |
| ----------------------- | --------------------------------- | ------------------------- |
| `OnBuildModeToggled`    | bool bIsActive                    | Build mode entered/exited |
| `OnPaletteItemChanged`  | int32 Index, FBuildableItem Item | Palette selection changes |
| `OnActorPlaced`         | AActor\* PlacedActor             | Actor placed in world     |
| `OnActorSelected`       | AActor\* SelectedActor           | Actor selected            |
| `OnActorDeselected`     | AActor\* DeselectedActor         | Actor deselected/deleted  |
| `OnTransformModeChanged`| EBuildTransformMode NewMode      | Transform mode changes    |
| `OnGridSnapToggled`     | bool bEnabled                    | Grid snap toggled         |

## ABuildPreviewActor

Transient ghost actor managed by the component. Not intended to be spawned manually.

| Function                        | Description                           |
| ------------------------------- | ------------------------------------- |
| `SetPreviewMesh(UStaticMesh*)`  | Set the mesh to display               |
| `SetPreviewColor(FLinearColor)` | Change the tint (alpha = opacity)     |

## Actor Tags

| Tag            | Applied To          | Purpose                          |
| -------------- | ------------------- | -------------------------------- |
| `BuildPreview` | Preview ghost actor | Identifies the transient preview |
| `BuildPlaced`  | Placed actors       | Marks build-system-placed actors |
