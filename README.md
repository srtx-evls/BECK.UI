---
![Obsidian UI Banner](https://github.com/srtx-evls/FJEKQOSIXKSPQOEIDOXKJAKA/blob/main/ObsidianBanner.jpg?raw=true?raw=true)
---
# Obsidian UI Library - Full Documentation

## Table of Contents
1. Introduction
2. Library Initialization
   - 2.3 Example
4. Library Configuration
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
## 2.3 Example
For Newbies 
```lua
local repo = "https://raw.githubusercontent.com/deividcomsono/Obsidian/main/"
local Library = loadstring(game:HttpGet(repo .. "Library.lua"))()
local ThemeManager = loadstring(game:HttpGet(repo .. "addons/ThemeManager.lua"))()
local SaveManager = loadstring(game:HttpGet(repo .. "addons/SaveManager.lua"))()

local Options = Library.Options
local Toggles = Library.Toggles

Library.ForceCheckbox = false
Library.ShowToggleFrameInKeybinds = true

local Window = Library:CreateWindow({
    Title = "mspaint",
    Footer = "version: example",
    Icon = 95816097006870,
    NotifySide = "Right",
    ShowCustomCursor = true,
})

local Tabs = {
    Main = Window:AddTab("Main", "user"),
    Key = Window:AddKeyTab("Key System"),
    ["UI Settings"] = Window:AddTab("UI Settings", "settings"),
}

local LeftGroupBox = Tabs.Main:AddLeftGroupbox("Groupbox")

LeftGroupBox:AddToggle("MyToggle", {
    Text = "This is a toggle",
    Tooltip = "This is a tooltip",
    DisabledTooltip = "I am disabled!",
    Default = true,
    Disabled = false,
    Visible = true,
    Risky = true,
    Callback = function(Value)
        print("[cb] MyToggle changed to:", Value)
    end,
}):AddColorPicker("ColorPicker1", {
    Default = Color3.new(1, 0, 0),
    Title = "Some color1",
    Transparency = 0,
    Callback = function(Value)
        print("[cb] Color changed!", Value)
    end,
}):AddColorPicker("ColorPicker2", {
    Default = Color3.new(0, 1, 0),
    Title = "Some color2",
    Callback = function(Value)
        print("[cb] Color changed!", Value)
    end,
})

Toggles.MyToggle:OnChanged(function()
    print("MyToggle changed to:", Toggles.MyToggle.Value)
end)

Toggles.MyToggle:SetValue(false)

LeftGroupBox:AddCheckbox("MyCheckbox", {
    Text = "This is a checkbox",
    Tooltip = "This is a tooltip",
    DisabledTooltip = "I am disabled!",
    Default = true,
    Disabled = false,
    Visible = true,
    Risky = false,
    Callback = function(Value)
        print("[cb] MyCheckbox changed to:", Value)
    end,
})

Toggles.MyCheckbox:OnChanged(function()
    print("MyCheckbox changed to:", Toggles.MyCheckbox.Value)
end)

local MyButton = LeftGroupBox:AddButton({
    Text = "Button",
    Func = function()
        print("You clicked a button!")
    end,
    DoubleClick = false,
    Tooltip = "This is the main button",
    DisabledTooltip = "I am disabled!",
    Disabled = false,
    Visible = true,
    Risky = false,
})

local MyButton2 = MyButton:AddButton({
    Text = "Sub button",
    Func = function()
        print("You clicked a sub button!")
    end,
    DoubleClick = true,
    Tooltip = "This is the sub button",
    DisabledTooltip = "I am disabled!",
})

local MyDisabledButton = LeftGroupBox:AddButton({
    Text = "Disabled Button",
    Func = function()
        print("You somehow clicked a disabled button!")
    end,
    DoubleClick = false,
    Tooltip = "This is a disabled button",
    DisabledTooltip = "I am disabled!",
    Disabled = true,
})

LeftGroupBox:AddLabel("This is a label")
LeftGroupBox:AddLabel("This is a label\n\nwhich wraps its text!", true)
LeftGroupBox:AddDivider()

LeftGroupBox:AddSlider("MySlider", {
    Text = "This is my slider!",
    Default = 0,
    Min = 0,
    Max = 5,
    Rounding = 1,
    Compact = false,
    Callback = function(Value)
        print("[cb] MySlider was changed! New value:", Value)
    end,
    Tooltip = "I am a slider!",
    DisabledTooltip = "I am disabled!",
    Disabled = false,
    Visible = true,
})

Options.MySlider:SetValue(3)

LeftGroupBox:AddInput("MyTextbox", {
    Default = "My textbox!",
    Numeric = false,
    Finished = false,
    ClearTextOnFocus = true,
    Text = "This is a textbox",
    Tooltip = "This is a tooltip",
    Placeholder = "Placeholder text",
    Callback = function(Value)
        print("[cb] Text updated. New text:", Value)
    end,
})

Options.MyTextbox:OnChanged(function()
    print("Text updated. New text:", Options.MyTextbox.Value)
end)

local DropdownGroupBox = Tabs.Main:AddRightGroupbox("Dropdowns")

DropdownGroupBox:AddDropdown("MyDropdown", {
    Values = { "This", "is", "a", "dropdown" },
    Default = 1,
    Multi = false,
    Text = "A dropdown",
    Tooltip = "This is a tooltip",
    DisabledTooltip = "I am disabled!",
    Callback = function(Value)
        print("[cb] Dropdown got changed. New value:", Value)
    end,
    Disabled = false,
    Visible = true,
})

Options.MyDropdown:SetValue("This")

local MenuGroup = Tabs["UI Settings"]:AddLeftGroupbox("Menu")

MenuGroup:AddToggle("KeybindMenuOpen", {
    Default = Library.KeybindFrame.Visible,
    Text = "Open Keybind Menu",
    Callback = function(value)
        Library.KeybindFrame.Visible = value
    end,
})

MenuGroup:AddToggle("ShowCustomCursor", {
    Text = "Custom Cursor",
    Default = true,
    Callback = function(Value)
        Library.ShowCustomCursor = Value
    end,
})

MenuGroup:AddDropdown("NotificationSide", {
    Values = { "Left", "Right" },
    Default = "Right",
    Text = "Notification Side",
    Callback = function(Value)
        Library:SetNotifySide(Value)
    end,
})

MenuGroup:AddDropdown("DPIDropdown", {
    Values = { "50%", "75%", "100%", "125%", "150%", "175%", "200%" },
    Default = "100%",
    Text = "DPI Scale",
    Callback = function(Value)
        Value = Value:gsub("%%", "")
        local DPI = tonumber(Value)
        Library:SetDPIScale(DPI)
    end,
})

MenuGroup:AddDivider()

MenuGroup:AddLabel("Menu bind"):AddKeyPicker("MenuKeybind", {
    Default = "RightShift",
    NoUI = true,
    Text = "Menu keybind"
})

MenuGroup:AddButton("Unload", function()
    Library:Unload()
end)

Library.ToggleKeybind = Options.MenuKeybind
ThemeManager:SetLibrary(Library)
SaveManager:SetLibrary(Library)
SaveManager:IgnoreThemeSettings()
SaveManager:SetIgnoreIndexes({ "MenuKeybind" })

ThemeManager:SetFolder("MyScriptHub")
SaveManager:SetFolder("MyScriptHub/specific-game")
SaveManager:SetSubFolder("specific-place")

SaveManager:BuildConfigSection(Tabs["UI Settings"])
ThemeManager:ApplyToTab(Tabs["UI Settings"])
SaveManager:LoadAutoloadConfig()
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
