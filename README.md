# Build System

Welcome to the official documentation for **Build System** — an Unreal Engine runtime plugin by [Tibeuru](https://tibeuru.com) that gives players an in-game build mode for placing, selecting, transforming, and deleting actors at runtime.

> **\[Hero Image — Plugin banner or logo]**

{% hint style="info" %}
**\[Video — Overview trailer showing Build System in action: entering build mode, browsing the palette, placing items, selecting and transforming placed actors]**
{% endhint %}

## What is Build System?

Build System provides a single component (`UBuildModeComponent`) that can be added to any character or player controller to enable a full in-game construction mode. Players can browse a palette of buildable items, aim to place them in the world with a ghost preview, and then select, move, rotate, scale, or delete placed actors — all at runtime.

## Key Features

* **Build Mode Toggle** — Enter and exit build mode at any time during gameplay
* **Build Palette** — Define buildable items as static meshes or actor classes with display names and thumbnails
* **Ghost Preview** — Translucent preview actor follows the player's aim with real-time positioning
* **Grid Snapping** — Configurable grid snap for precise placement (default 50 UU)
* **Transform Tools** — Translate, rotate, and scale placed actors along any axis (X, Y, Z)
* **Selection System** — Select placed actors under the crosshair or cursor for modification
* **Deletion** — Remove placed actors from the world
* **Full Event System** — Blueprint-assignable delegates for all build events (placement, selection, transforms, etc.)
* **Zero Cost When Inactive** — Component tick is disabled outside of build mode

> **\[Screenshot — Build mode active in-game with a ghost preview following the crosshair and placed actors visible in the scene]**

## Requirements

* Unreal Engine 5.7+
* Enhanced Input plugin (included with UE5)
* Windows 64-bit or macOS
