# Installation

## Prerequisites

Before installing Build System, ensure you have:

1. **Unreal Engine 5.7+** installed
2. **Enhanced Input** plugin enabled (comes with UE5)

## Install the Plugin

1. Download the Build System plugin
2. Copy the `BuildSystem` folder into your project's `Plugins/` directory:

```
YourProject/
└── Plugins/
    └── BuildSystem/
        ├── BuildSystem.uplugin
        └── Source/
            └── BuildSystem/
                ├── Public/
                └── Private/
```

3. Restart the Unreal Editor
4. The plugin is **enabled by default**. Verify in **Edit > Plugins** by searching for "Build System"

> **\[Screenshot — Plugins window showing Build System enabled]**

## Verify Installation

Once installed, you should see:

* **Build Mode Component** available when adding components to any actor
* A log message in the Output Log confirming the plugin loaded

> **\[Screenshot — Add Component menu showing Build Mode Component in the BuildSystem category]**

## Plugin Dependencies

Build System automatically enables these required plugins:

| Plugin        | Purpose               |
| ------------- | --------------------- |
| EnhancedInput | Input action handling |
