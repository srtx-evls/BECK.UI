---
![Obsidian UI Banner](https://github.com/srtx-evls/FJEKQOSIXKSPQOEIDOXKJAKA/blob/main/ObsidianBanner.jpg?raw=true?raw=true)
---
# Obsidian UI Library - Full Documentation

## Table of Contents
1. Introduction
2. Library Initialization
3. Library Configuration
- Variables
5. Creating a Window
6. Tabs & Groupboxes
7. UI Elements
   - Toggles
   - Checkboxes
   - Buttons
   - Labels
   - Sliders
   - Text Inputs
   - Dropdowns
   - Color Pickers
   - Keybinds
8. Notifications
9. Save & Load System
10. Themes & DPI Settings
11. Event Handling & Best Practices
12. Unloading the Library
13. Credits

---

## 1. Introduction
Obsidian UI Library is a modified version of LinoriaLib, designed for a modern, mobile-friendly, and customizable UI experience in Roblox scripting.

This documentation covers how to use Obsidian UI Library to build powerful user interfaces with ease.
![Obsidian UI Banner](https://github.com/srtx-evls/FJEKQOSIXKSPQOEIDOXKJAKA/blob/main/UI.jpg?raw=true?raw=true)
---

## 2. Library Initialization
To use the library, load it along with ThemeManager and SaveManager.

```lua
local repo = "https://raw.githubusercontent.com/deividcomsono/Obsidian/main/"
local Library = loadstring(game:HttpGet(repo .. "Library.lua"))()
local ThemeManager = loadstring(game:HttpGet(repo .. "addons/ThemeManager.lua"))()
local SaveManager = loadstring(game:HttpGet(repo .. "addons/SaveManager.lua"))()
```

---

## 3. Library Configuration
Modify library settings before creating the UI.

```lua
Library.ForceCheckbox = false -- Forces toggles to use checkboxes
Library.ShowToggleFrameInKeybinds = true -- Shows toggle frame inside keybinds UI
```

---
## 3.1 Variables 
Options: Configures settings / Toggles: Controls features (on/off).
```lua
local Options = Library.Options
local Toggles = Library.Toggles
```

---

## 4. Creating a Window
The Window is the main UI container.

```lua
local Window = Library:CreateWindow({
	Title = "Obsidian UI",
	Footer = "Version 1.0",
	Icon = 95816097006870, -- (Optional)
	NotifySide = "Right", -- Notification position ("Left" or "Right")
	ShowCustomCursor = true, -- Enables custom cursor
})
```

---

## 5. Tabs & Groupboxes
### Creating Tabs
Tabs help organize UI elements.

```lua
local Tabs = {
	Main = Window:AddTab("Main", "user"),
	Key = Window:AddKeyTab("Key System"),
	["UI Settings"] = Window:AddTab("UI Settings", "settings"),
}
```

### Adding Groupboxes
Groupboxes organize UI elements inside a tab.

```lua
local LeftGroupBox = Tabs.Main:AddLeftGroupbox("Main Features")
local RightGroupBox = Tabs.Main:AddRightGroupbox("Settings")
```

---

## 6. UI Elements
### 6.1 Toggles
Toggles are on/off switches.

```lua
LeftGroupBox:AddToggle("ExampleToggle", {
	Text = "Enable Feature",
	Default = true,
	Tooltip = "Enables a feature",
	Callback = function(Value)
		print("Toggle changed:", Value)
	end
})
```

---

### 6.2 Checkboxes
Similar to toggles but styled as checkboxes.

```lua
LeftGroupBox:AddCheckbox("ExampleCheckbox", {
	Text = "Enable Option",
	Default = false,
	Callback = function(Value)
		print("Checkbox changed:", Value)
	end
})
```

---

### 6.3 Buttons
Executes an action when clicked.

```lua
LeftGroupBox:AddButton({
	Text = "Click Me",
	Func = function()
		print("Button clicked!")
	end,
	Tooltip = "Press to trigger an action"
})
```

---

### 6.4 Labels
Displays text in the UI.

```lua
LeftGroupBox:AddLabel("This is a normal label")
```

---

### 6.5 Sliders
Allows users to select numeric values.

```lua
LeftGroupBox:AddSlider("SpeedSlider", {
	Text = "Speed",
	Default = 10,
	Min = 0,
	Max = 100,
	Rounding = 1,
	Callback = function(Value)
		print("Speed changed:", Value)
	end
})
```

---

### 6.6 Text Inputs
Allows user text input.

```lua
LeftGroupBox:AddInput("NameInput", {
	Default = "Enter text...",
	Text = "Player Name",
	Placeholder = "Type here...",
	Callback = function(Value)
		print("Input changed:", Value)
	end
})
```

---

### 6.7 Dropdowns
Creates a dropdown menu.

```lua
LeftGroupBox:AddDropdown("WeaponSelect", {
	Values = { "Pistol", "Rifle", "Sniper" },
	Default = 1,
	Multi = false,
	Text = "Select a weapon",
	Searchable = true,
	Callback = function(Value)
		print("Weapon selected:", Value)
	end
})
```
---

### 6.8 ColorPicker  
Allows users pick a color

```lua
LeftGroupBox:AddColorPicker("ColorPicker1", {
    Default = Color3.new(1, 0, 0), -- Default color (Red)
    Title = "Some Color1",         -- Color picker title
    Transparency = 0,              -- Transparency value (0 is fully opaque)
    Callback = function(Value)
        print("[cb] Color changed!", Value)
    end
})
```


---

## 7. Notifications
Displays in-game notifications.

```lua
Library:Notify("Message", 5) -- Displays for 5 seconds
```

---

## 8. Save & Load System
Saves UI settings between sessions.

```lua
SaveManager:SetLibrary(Library)
SaveManager:BuildConfigSection(Tabs["UI Settings"])
SaveManager:LoadAutoloadConfig()
```

---

## 9. Themes & DPI Settings
Customize UI appearance.

```lua
ThemeManager:SetLibrary(Library)
ThemeManager:ApplyToTab(Tabs["UI Settings"])

Library:SetDPIScale(100) -- DPI scaling
```

---

## 10. Event Handling & Best Practices
- Use `OnChanged` to detect UI changes.
- Separate UI logic from game logic.
- Optimize script execution for performance.

---

## 11. Unloading the Library
Removes the UI when no longer needed.

```lua
Library:OnUnload(function()
	print("UI unloaded!")
end)
```

---

## 12. Credits
- **LinoriaLib**: Original UI framework
- **Modified by deivid**: Enhanced mobile-friendly features

---
