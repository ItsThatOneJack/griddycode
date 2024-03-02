# GriddyCode
Coding has never been more lit!

# Table of Contents
1. [GriddyCode](#griddycode)
   - [Lua modding](#lua-modding)
	  - [Where?](#where)
	  - [How?](#how)
	  - [Docs?](#docs)
		 - [Langs](#langs)
			- [Introduction](#introduction)
			- [Methods](#methods)
		 - [Themes](#themes)
			- [Introduction](#introduction-1)
			- [Methods](#methods-1)
2. [Known issues](#known-issues)
   - [Visual bugs](#visual-bugs)
3. [Contributions](#contributions)
   - [Current bugs/needed features](#current-bugsneeded-features)
	  - [HIGH PRIORITY](#high-priority)
	  - [MEDIUM PRIORITY](#medium-priority)
	  - [LOW PRIORITY](#low-priority)


# Lua modding
GriddyCode allows you to extend its functionality via **Lua**.

## Where?
To open the folder with Lua scripts, go to:
- Windows: `%APPDATA%\Bussin GriddyCode`
- macOS: `~/Library/Application Support/Bussin GriddyCode`
- Linux: `~/.local/share/Bussin GriddyCode`

*Note: since the paths might change, we recommend you manually search for GriddyCode in the AppData of your OS.*

## How?
You may see the folders **"langs"** and **"themes"**.
- **"langs"** holds a bunch of `.lua` files that power GriddyCode's syntax highlighting & autocomplete.
- **"themes"** holds a bunch of `.lua` files that change GriddyCode's appearance.

*Note: the Lua scripts are reloaded only if you switch from a different file extension (i.e. "README.md" -> "main.ts"), or if GriddyCode is restarted.*

## Docs?
### Langs
#### Introduction
To extend the functionality of GriddyCode for a specific **file extension**, create a file with its name. (i.e. `toml.lua`)

#### Methods
#### Methods

| Method | Example | Description | Notes |
| -------- | -------- | -------- | -------- |
| `highlight(keyword: String, color: String)` | `highlight("const", "reserved")` | Tells GriddyCode to highlight a certain keyword with a preset of colors. | Available colors: `reserved`, `string`, `binary`, `symbol`, `variable`, `operator`, `comments`, `error`, `function`, `member` |
| `highlight_region(start: String, end: String, color: String, line_only: bool = false)` | `highlight("/*", "*/", "comments", false)` | Tells GriddyCode to highlight a region with a preset of colors. | The `start` must be a symbol. Due to Godot's limited functionality, you can't use RegEx. |
| `detect_functions(content: String) -> Array[String]` | `detect_functions("const test = 3; function main() {}; async init() => { main() }")` | Called by GriddyCode upon input. Results are showed in the autocomplete feature. | This must be provided by the Lua script. It must return an array of strings (i.e. ["main", "init"]). |
| `detect_variables(content: String) -> Array[String]` | `detect_variables("const test = 3;")` | Called by GriddyCode upon input. Results are showed in the autocomplete feature. | This must be provided by the Lua script. It must return an array of strings (i.e. ["test"]). |

*Note: to provide reserved variables/functions (i.e. `Math`/`parseInt()` in JS) you can have them as preset values in the array you return. GriddyCode will handle the rest!*
### Themes
#### Introduction
To add a theme, create a file in the **"themes"** folder with any name. (i.e. "dracula.lua"). You will be able to choose it within GriddyCode.

#### Methods
| Method | Example | Description | Notes |
| -------- | -------- | -------- | -------- |
| `set_keywords(property: String, new_color: String)` | `set_keywords("reserved", "#ff00ff")` | Set the color of syntax highlighting. | The second argument must be a hex, `#` being optional. Available colors/properties listed above at `langs`. |
| `set_gui(property: String, new_color: String)` | `set_gui("background_color", "#ff00ff")` | This method is dedicated to the overall GUI aspect of GriddyCode. | Available properties: `background_color`, `current_line_color`, `selection_color`, `font_color`, `word_highlighted_color`, `selection_background_color`. Properties except `background_color`, if not provided, will be set to a slightly modified version of `background_color`. Although possible, we don't recommend you rely on those & instead set all the values. |

*Note: if the HEX you input is invalid, it will default to #ff0000 (red)*

# Known issues
## Visual bugs
- The `CheckButton` node for each `setting` scene doesn't change with the theme. This affects light themes specifically.

# Contributions
Contributions are heavily appreciated, whether it's for adding Lua plugins, themes, safely exposing more features to Lua, or adding features directly to GriddyCode!

## Current bugs/needed features:
### HIGH PRIORITY
- To apply changes to the settings (i.e. adding a new setting), it's required to delete your save data;
- The `VHS & CRT` shader, on certain themes (One Dark Pro, etc.), becomes completely white. Works good on GitHub Dark;
- Light modes get affected by *glow*, while dark modes seem fine.

### MEDIUM PRIORITY
- An option in the settings menu (`CTRL` + `,`) to change the font;
- The current limit for lines is ~1600. If the cursor moves past that amount, the `CodeEdit` node will activate its scrolling, making the camera bug & go out of view. A limit should be implemented so that the camera won't go out of screen.

### LOW PRIORITY
- Making the cat jumping video in the settings menu fade in/out along the actual menu. Currently it ignores the transition;
- `CTRL` + `P` to open a **quick file picker**, similar to [VSCode](https://code.visualstudio.com/docs/editor/editingevolved#:~:text=Quick%20file%20navigation,-Tip%3A%20You%20can&text=VS%20Code%20provides%20two%20powerful,release%20Ctrl%20to%20open%20it.).
- Selecting a setting with the property "shader" *should* disable previously-enabled settings with "shader".
