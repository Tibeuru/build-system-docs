# Troubleshooting

## Common Issues

### Ghost preview does not appear

* Ensure the Build Palette has at least one item with a valid **Mesh** reference
* Actor Class items do not show a preview ghost — this is by design
* Check that the mesh asset is valid and not null

### Cannot select placed actors

* Only actors tagged `BuildPlaced` can be selected
* Ensure the trace is hitting the actor's collision — check `TraceChannel`
* Increase `TraceDistance` if the actor is far away

### Preview snaps to wrong position

* Check `GridSize` — a large value causes bigger jumps
* Toggle grid snap off with `ToggleGridSnap()` for free placement
* Ensure `bGridSnapEnabled` is set as expected

### Transform has no effect

* Ensure an actor is **selected** before calling `ApplyTransformDelta()`
* Check `CurrentTransformMode` and `CurrentTransformAxis` are set correctly
* Verify the step values (`RotationStep`, `TranslateStep`, `ScaleStep`) are not zero

### Build mode will not activate

* Ensure the component's `BuildPalette` is not empty
* Check that the component is attached to a Pawn or PlayerController with a valid `APlayerController`
* Verify Enhanced Input is enabled in your project

### Mouse cursor trace not working

* Set `bUseCrosshairTrace` to **false** to use mouse cursor instead of camera center
* Ensure the player controller has `bShowMouseCursor` set to true
* Check that `GetMousePosition()` returns valid values

## Performance

Build System has zero runtime cost when build mode is inactive:

* Component tick is only enabled during build mode
* The ghost preview actor is destroyed on exit
* No per-frame traces occur outside of build mode

When active, the cost is a single line trace per frame plus the preview actor update.
