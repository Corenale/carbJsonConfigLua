# CarboneumJsonConfig Library

CarboneumJsonConfig is a Lua library for handling JSON configuration files, with special support for FFI cdata structures.

## Features

- Save and load configuration data to/from JSON files
- Support for complex data structures including nested tables and FFI cdata
- Automatic handling of cdata serialization and deserialization
- Reset configurations to default values
- Path fixing for cross-platform compatibility

## Built-in dependencies

- dkjson
- lbase64
- ffi-reflect

## Usage

```lua
local carboneum = require("carbJsonConfig")

-- Define your configuration table
local config = {
    someValue = 123,
    someString = "hello",
    someStruct = ffi.new("struct { int x; float y; }")
}

-- Load configuration (creates file if it doesn't exist)
carboneum.load("config/myconfig.json", config)

-- Save configuration
config()

-- Reset configuration to default values
config("reset")
```

## API

### `carboneum.load(path, table)`

Loads configuration from a JSON file. If the file doesn't exist, it creates one with the provided table.

- `path`: Path to the JSON file
- `table`: Table to load the configuration into

### `config()`

Saves the configuration table to a JSON file.

### `config("reset")`

Resets the configuration to its original values. Methods is added to the config table after calling `carboneum.load()`.

## Notes

- The library handles cdata structures by either saving them as tables (when possible) or as base64-encoded strings.
- Unnamed cdata structs are saved as bytes.
- Unsupported types (userdata, threads, functions) are skipped during serialization.
