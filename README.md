# Nothing 2 - Modding API Documentation

## How to load assets

The game loads assets from the path specified in the `defaults.json`.

## Assets Layout

How you organize the assets is up to you. The game will search through entire folders and subfolders until it finds what it needs.

## Asset Types

You can load the following types of devices:
- PNG images
- [SDF](https://github.com/BBpezsgo/data-utilities/wiki/Custom-File-Format) data files
- JSON data files
- LUA script files
- WAV audio files

## Data Layouts

### Scene Data Layout

Here is the data layout for a in-game scene:
```meta
script: SCENE_SCRIPT.lua
objects: [
    {
        id: string
        at: { x: number y: number }
    }
    ...
]
```

The `script` field is optional. You can specify a .lua file that will be loaded when the scene loads and starts executing it.

In the `objects` field, you can specify which prefabs should be displayed when the scene is loaded.
The `id` field is the prefab's id, and the `at` is the 2D position where the prefab should be instantiated.

### Prefab Data Layout

Here is the data layout for a in-game prefab:
```meta
Base: string
Tag: string
ID: string
Components: {
  ...
}
```

The `Base` field defines the parent data from which it is inherited. All parent data is loaded and existing fields are replaced by child fields.

The `Tag` field defines the tag of the Unity GameObject. In most cases you should set it to "Entity".

The `ID` field defines the prefab ID. This identifier is used in other files, such as the scene data file. This must be unique.

The `Components` field defines the components that are added to the prefab when loaded.

### LUA Scripting API

Here is a sample of an .api file:
```lua

function Start(this)
    -- ...
end

function FixedUpdate(this)
    -- ...
end

function Update(this)
    -- ...
end

function OnGUI()
    -- ...
end
```

All the functions are optional.

The `Start` function is called when the prefab is instantiated.

The `FixedUpdate` function is called on every Unity fixed update frame.

The `Update` function is called on every Unity update frame.

The `OnGUI` function is called on every Unity OnGUI event. In this function you can draw things on the screen.
