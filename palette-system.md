# Palette System

## Overview

The Build Palette is an array of `FBuildableItem` entries that define what the player can place. Each item can be a static mesh or an actor class, with an optional display name and thumbnail for UI.

## FBuildableItem Structure

| Field       | Type                              | Description                          |
| ----------- | --------------------------------- | ------------------------------------ |
| DisplayName | FText                             | Name shown in UI                     |
| Mesh        | TSoftObjectPtr\<UStaticMesh>      | Static mesh to place (Mesh mode)     |
| ActorClass  | TSoftClassPtr\<AActor>            | Actor class to spawn (Actor mode)    |
| Thumbnail   | TSoftObjectPtr\<UTexture2D>       | Optional icon for UI palette display |

> Soft references are used so the palette can be configured in data without forcing assets into memory until needed.

## Setting the Palette

### In the Editor

Add items directly in the **Details** panel under **Build System > Palette > BuildPalette**. Click the **+** button to add entries.

### At Runtime

Call `SetBuildPalette(TArray<FBuildableItem>)` to replace the entire palette at runtime. This resets the selection to index 0.

## Cycling Items

| Function                       | Description                         |
| ------------------------------ | ----------------------------------- |
| `CyclePaletteNext()`          | Select the next item (wraps around) |
| `CyclePalettePrev()`          | Select the previous item (wraps)    |
| `SelectPaletteItem(int32)`    | Select a specific index             |

When the palette item changes:

1. Any selected actor is deselected
2. The preview rotation resets
3. A new ghost preview spawns for the new item
4. `OnPaletteItemChanged` is broadcast with the index and item data

## Querying

| Function                              | Description                                  |
| ------------------------------------- | -------------------------------------------- |
| `GetCurrentPaletteItem(FBuildableItem&)` | Returns the active item (false if empty)  |
