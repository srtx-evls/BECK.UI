---
![Obsidian UI Banner](https://github.com/srtx-evls/FJEKQOSIXKSPQOEIDOXKJAKA/blob/main/ObsidianBanner.jpg?raw=true?raw=true)
---
# Obsidian UI Library

## 1. Introduction
Obsidian UI Library is a modified version of LinoriaLib, designed for a modern, mobile-friendly, and customizable UI experience in Roblox scripting.

This documentation covers how to use Obsidian UI Library to build powerful user interfaces with ease.
![Obsidian UI Banner](https://github.com/srtx-evls/FJEKQOSIXKSPQOEIDOXKJAKA/blob/main/UI.jpg?raw=true?raw=true)
---
## 2.3 Example
i lazzy to do all components of ui
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

## Credits
- **LinoriaLib**: Original UI framework
- **Modified by deivid**: Enhanced mobile-friendly features

---
