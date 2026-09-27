# GitHub Actions for Godot

This repo provides a collection of forgejo actions related to the Godot game engine, including:

- [`install-godot`](#install-godot)
- [`build-godot`](#build-godot)

See below for more details on usage of each action.

**Note: all actions in this repo are currently designed to run inside of git.gays docker container, assume builds use GDScript, a released binary engine version, and do not require compilation and linking of source plugins.**

## `install-godot`

This action installs Godot to the applications directory (`~/.local/share/bin`) for a specific Godot version within the docker runner. If the installation is to be used for building, the `install-templates` flag should be set to `true` in order to install with Godot's export templates.

### Inputs

#### `godot-version`

**Required** The version of Godot to build with. Default `0.0` (invalid).

#### `install-templates`

Whether or not to install the Godot export templates. Default `false`.

### Outputs

#### `godot-executable`

The path to the installed Godot executable.

### Example usage

```yaml
- name: Install Godot
        uses: https://git.ourserver.fun/GR3YH4TT3R93/godot-actions/install-godot@v2.5
        with:
          godot-version: 4.5.1-stable
          install-templates: true
        id: install-godot
```

## `build-godot`

This action builds Windows, and Linux executables for the Godot project within the current directory, uploading all exports as GitHub Actions workflow artifacts where they can be later accessed either manually or via another workflow.

### Inputs

#### `build-dir`

**Required** The chosen build directory. Default `'build'`.

#### `godot-executable`

The path to the Godot executable. Default `~/.local/share/bin/godot`.

#### `platform`

What platform should be built. Should be the same string as the export template. Default `Linux`

#### `version-string`

What the version string should be of the export. Default `dev`

#### `game_name`

The name the game identifies as. Default `game`

#### `path_to_project`

Where in the repository the project is. Default ``

### Example usage

```yaml
- uses: https://git.ourserver.fun/GR3YH4TT3R93/godot-actions/install-godot@v2.5
  with:
    build-dir: './build'
    game-name: 'My awesome game'
```
