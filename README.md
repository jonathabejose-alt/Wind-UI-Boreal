# WindUI Shiny

**WindUI Shiny** is a refined fork of the original **WindUI** UI library for Roblox, built specifically for Script Hubs and Luau environments.

This fork preserves full compatibility with the original API and overall structure while introducing refinements, fixes, and visual improvements.


## Credits

WindUI was originally created by **[Footagesus](https://github.com/Footagesus)**.

Original repository:
[https://github.com/Footagesus/WindUI](https://github.com/Footagesus/WindUI)

This fork would not exist without the original work and structure provided by **Footagesus**.
Full credit for the base framework, architecture, and core systems belongs to the original author.

# WindUI Shiny Documentation

## Loader

```lua
local WindUI = loadstring(game:HttpGet("https://raw.githubusercontent.com/jonathabejose-alt/Wind-UI-Boreal/refs/heads/main/WindUI%20Boreal"))()
```

## Base Setup

All examples below assume this base setup:

```lua
local WindUI = loadstring(game:HttpGet("https://raw.githubusercontent.com/jonathabejose-alt/Wind-UI-Boreal/refs/heads/main/WindUI%20Boreal"))()

local Window = WindUI:CreateWindow({
    Title = "WindUI Docs Demo",
    Author = "Shiny",
    Folder = "WindUI-Docs",
    Size = UDim2.fromOffset(620, 500),
    Icon = "sparkles",
    ModernLayout = true,
    BottomDragBarEnabled = true,
})

local MainTab = Window:Tab({
    Title = "Main",
    Icon = "home",
})
```

## Multi Section

`MultiSection` is an expandable container with tabbed inner content.

### Create

```lua
local Multi = MainTab:MultiSection({
    Title = "Combat Modes",
    Desc = "Switch between profiles",
    Icon = "crosshair",
    Box = true,
    BoxBorder = true,
    Opened = true,
})
```

### Config

| Key | Type | Default | Notes |
| --- | --- | --- | --- |
| `Title` | `string` | `"Section"` | Header title |
| `Desc` | `string?` | `nil` | Header description |
| `Icon` | `string?` | `nil` | Header icon |
| `TextXAlignment` | `"Left" \| "Center" \| "Right"` | `"Left"` | Header text alignment |
| `TextSize` | `number` | `19` | Header title text size |
| `DescTextSize` | `number` | `16` | Header description text size |
| `Box` | `boolean` | `false` | Enables boxed background |
| `BoxBorder` | `boolean` | `false` | Shows outline when `Box=true` |
| `FontWeight` | `Enum.FontWeight` | `SemiBold` | Header title weight |
| `DescFontWeight` | `Enum.FontWeight` | `Medium` | Header desc weight |
| `TextTransparency` | `number` | `0.05` | Header title transparency |
| `DescTextTransparency` | `number` | `0.4` | Header desc transparency |
| `Hover` | `boolean` | `true` | Hover/press feedback |
| `Opened` | `boolean` | `false` | Starts opened |
| `Locked` | `boolean` | `false` | Starts locked |
| `LockedTitle` | `string?` | `nil` | Stored; no built-in label in this container |
| `HeaderSize` | `number` | `42` | Header base size |
| `IconSize` | `number` | `20` | Header icon size |
| `HeaderGap` | `number` | `10` | Horizontal spacing in header |
| `HeaderPaddingX` | `number` | dynamic | Horizontal header padding |
| `HeaderPaddingY` | `number` | dynamic | Vertical header padding |
| `TabGap` | `number` | `6` | Gap between tab chips |
| `TabPaddingX` | `number` | `12` | Tab chip horizontal padding |
| `TabPaddingY` | `number` | `8` | Tab chip vertical padding |
| `TabTextSize` | `number` | `15` | Tab title size |
| `TabDescTextSize` | `number` | `13` | Tab desc size |

### Multi Section Methods

| Method | Signature | Description |
| --- | --- | --- |
| `SetIcon` | `Multi:SetIcon(iconOrNil)` | Updates/removes header icon |
| `SetTitle` | `Multi:SetTitle(title)` | Updates header title |
| `SetDesc` | `Multi:SetDesc(descOrNil)` | Updates/removes description |
| `Lock` | `Multi:Lock()` | Locks header interaction and tab elements |
| `Unlock` | `Multi:Unlock()` | Unlocks interaction and tab elements |
| `SelectTab` | `Multi:SelectTab(tabValue, isInstant)` | Selects tab by object, index, or title |
| `GetSelectedTab` | `Multi:GetSelectedTab()` | Returns selected tab object |
| `GetTabs` | `Multi:GetTabs()` | Returns all tab objects |
| `Tab` | `Multi:Tab(tabConfig)` | Creates a tab inside this multi section |
| `Open` | `Multi:Open(isNotAnim)` | Opens content area |
| `Close` | `Multi:Close(isNotAnim)` | Closes content area |
| `Destroy` | `Multi:Destroy()` | Destroys container and all tab content |

### Tab Config (`Multi:Tab({...})`)

| Key | Type | Default | Notes |
| --- | --- | --- | --- |
| `Title` | `string` | `"Tab N"` | Tab title |
| `Desc` | `string?` | `nil` | Tab subtitle |
| `Icon` | `string?` | `nil` | Tab icon |
| `IconThemed` | `boolean?` | `nil` | Uses themed icon coloring |
| `Selected` | `boolean` | `false` | Select immediately |
| `Opened` | `boolean` | `false` | Alias for immediate select |

### Multi Section Tab Methods

| Method | Signature | Description |
| --- | --- | --- |
| `Select` | `Tab:Select(isInstant)` | Selects this tab |
| `Destroy` | `Tab:Destroy()` | Removes this tab and its elements |

Each tab also receives element constructors:
`Paragraph`, `Button`, `ButtonKeybind`, `Toggle`, `ToggleKeybind`, `Slider`, `Keybind`, `Input`, `Dropdown`, `Code`, `Colorpicker`, `Section`, `MultiSection`, `Divider`, `Space`, `Image`, `Group`, `Video`.

### Full Example (All Multi Section Methods)

```lua
local Multi = MainTab:MultiSection({
    Title = "Combat Modes",
    Desc = "Select your profile",
    Icon = "crosshair",
    Box = true,
    BoxBorder = true,
    Opened = true,
})

local Rage = Multi:Tab({
    Title = "Rage",
    Desc = "Aggressive settings",
    Icon = "flame",
    Selected = true,
})

local Legit = Multi:Tab({
    Title = "Legit",
    Desc = "Low profile settings",
    Icon = "shield-check",
})

Rage:Toggle({
    Title = "Silent Aim",
    Value = false,
})

Legit:Slider({
    Title = "FOV",
    Value = { Min = 10, Max = 250, Default = 80 },
})

Multi:SetIcon("swords")
Multi:SetTitle("Profiles")
Multi:SetDesc("Switch behavior quickly")

Multi:SelectTab("Legit", true)
Multi:SelectTab(1, false)
Multi:SelectTab(Rage)

local selected = Multi:GetSelectedTab()
print("Selected tab:", selected and selected.Title)

local allTabs = Multi:GetTabs()
print("Tab count:", #allTabs)

local temp = Multi:Tab({ Title = "Temporary" })
temp:Select(true)
temp:Destroy()

Multi:Open(true)
Multi:Close(false)
Multi:Lock()
Multi:Unlock()
```

## Divider

`Divider` creates horizontal or vertical separators, with optional title support for horizontal mode.

### Create

```lua
local Divider = MainTab:Divider({
    Title = "Combat Settings",
    TitleAlignment = "Center",
})
```

### Config

| Key | Type | Default | Notes |
| --- | --- | --- | --- |
| `Orientation` | `"Horizontal" \| "Vertical"` | dynamic | Defaults to `Vertical` in groups, otherwise `Horizontal` |
| `Title` / `Text` | `string` | `""` | Horizontal title |
| `Thickness` | `number` | `1` | Minimum `1` |
| `Inset` | `number` | `7` | Frame inset |
| `TitleSpacing` | `number` | `8` | Space around title |
| `TitleAlignment` | `"Left" \| "Center" \| "Right"` | `"Center"` | Title side/alignment |
| `Height` | `number` | auto | Horizontal frame height |
| `Width` | `number` | auto | Vertical frame width |
| `Size` | `UDim2` | auto | Overrides default size |
| `Color` | `string \| Color3` | theme `"Divider"` | Divider line color |
| `Transparency` | `number` | theme | Divider line transparency |
| `TitleColor` | `string \| Color3` | theme `"DividerLabel"` | Title color |
| `TitleTransparency` | `number` | theme | Title transparency |
| `TitleSize` | `number` | `13` | Title text size |

### Methods

| Method | Signature | Description |
| --- | --- | --- |
| `SetTitle` | `Divider:SetTitle(newTitle)` | Updates title text |
| `SetThickness` | `Divider:SetThickness(px)` | Updates line thickness |
| `SetTitleAlignment` | `Divider:SetTitleAlignment("Left" \| "Center" \| "Right")` | Updates title alignment |
| `SetTitleSpacing` | `Divider:SetTitleSpacing(px)` | Updates title spacing |

### Full Example (All Divider Methods)

```lua
local Divider = MainTab:Divider({
    Title = "Aimbot",
    TitleAlignment = "Center",
    Thickness = 1,
    TitleSpacing = 8,
    Color = "Divider",
    TitleColor = "DividerLabel",
})

Divider:SetTitle("Aimbot Controls")
Divider:SetThickness(2)
Divider:SetTitleAlignment("Left")
Divider:SetTitleSpacing(14)
```

## Sidebar Elements

These APIs create controls in the left sidebar on the `Window` object.

### Label APIs

`Window:SideBarLabel(config)`  
Aliases: `Window.SidebarLabel`, `Window.Label`

Config:

| Key | Type | Default |
| --- | --- | --- |
| `Title` / `Text` | `string` | `"Label"` |
| `Icon` | `string?` | `nil` |
| `Placeholder` | `boolean` | `false` |
| `Radius` | `number?` | `nil` |
| `Height` | `number` | `34` (min `18`) |
| `Size` | `UDim2?` | `UDim2.new(1, -7, 0, Height)` |
| `Visible` | `boolean` | `true` |
| `LayoutOrder` | `number?` | `nil` |

Return object methods:
`SetTitle(newTitle)`, `SetVisible(visible)`, `Destroy()`.

### Button APIs

`Window:SideBarButton(config)`  
Aliases: `Window.SidebarButton`, `Window.Button`

Config:

| Key | Type | Default |
| --- | --- | --- |
| `Title` / `Text` | `string` | `"Button"` |
| `Icon` | `string?` | `nil` |
| `Callback` | `function?` | `nil` |
| `Variant` | `string` | `"Secondary"` |
| `FullRounded` | `boolean?` | `nil` |
| `Radius` | `number?` | `nil` |
| `Height` | `number` | `34` (min `20`) |
| `Size` | `UDim2?` | `UDim2.new(1, -7, 0, Height)` |
| `Visible` | `boolean` | `true` |
| `LayoutOrder` | `number?` | `nil` |

Return object methods:
`SetTitle(newTitle)`, `SetCallback(callback)`, `SetVisible(visible)`, `Destroy()`.

### Space APIs

`Window:SideBarSpace(config)`  
Aliases: `Window.SidebarSpace`, `Window.Space`

Config:

| Key | Type | Default |
| --- | --- | --- |
| `Columns` | `number` | `1` |

Return value: a `Frame` (`Space.ElementFrame`), not a method-rich object.

### Divider APIs

`Window:Divider(config)` creates a sidebar divider.  
Aliases: `Window:SideBarDivider(config)`, `Window.SidebarDivider`.

Config is the same as the `Divider` element config above.

Return value: divider `Frame` only (for runtime method access, use `Tab:Divider(...)` instead).

### Full Example (Sidebar Elements)

```lua
local sbLabel = Window:SideBarLabel({
    Title = "Quick Actions",
    Icon = "sparkles",
})

local sbButton = Window:SideBarButton({
    Title = "Recenter",
    Icon = "locate-fixed",
    Variant = "Secondary",
    Callback = function()
        Window:SetToTheCenter()
    end,
})

local sbSpaceFrame = Window:SideBarSpace({
    Columns = 2,
})

local sbDividerFrame = Window:SideBarDivider({
    Title = "Tools",
    TitleAlignment = "Left",
})

sbLabel:SetTitle("Quick Tools")
sbLabel:SetVisible(true)

sbButton:SetTitle("Center Window")
sbButton:SetCallback(function()
    WindUI:Notify({
        Title = "Window",
        Content = "Centered",
    })
    Window:SetToTheCenter()
end)
sbButton:SetVisible(true)

task.delay(20, function()
    sbLabel:Destroy()
    sbButton:Destroy()
    sbSpaceFrame:Destroy()
    sbDividerFrame:Destroy()
end)
```

## Notify with Buttons

`WindUI:Notify(config)` creates a notification popup and returns a notification object.

### Config

| Key | Type | Default | Notes |
| --- | --- | --- | --- |
| `Title` | `string` | `"Notification"` | Notification title |
| `Content` | `string?` | `nil` | Body text |
| `Icon` | `string?` | `nil` | Optional icon |
| `IconThemed` | `boolean?` | `nil` | Themed icon coloring |
| `Background` | `string?` | `nil` | Image source |
| `BackgroundImageTransparency` | `number?` | `0` | Background image transparency |
| `Duration` | `number` | `5` | Auto-close seconds |
| `CanClose` | `boolean` | `true` | Shows close button |
| `Buttons` | `table[]` | `{}` | Action buttons |

### Button Entry Config (`Buttons = {...}`)

| Key | Type | Default | Notes |
| --- | --- | --- | --- |
| `Title` | `string` | required | Button text |
| `Icon` | `string?` | `nil` | Optional icon |
| `Variant` | `string?` | `nil` | Button variant |
| `Callback` | `function?` | `nil` | Runs on click |
| `CloseOnClick` | `boolean` | `true` | Auto-close behavior |

### Notification Methods

| Method | Signature | Description |
| --- | --- | --- |
| `Close` | `Notification:Close()` | Closes and destroys notification |

### Full Example (Notify + Buttons)

```lua
local n = WindUI:Notify({
    Title = "Configuration Loaded",
    Content = "Choose an action below.",
    Icon = "bell",
    IconThemed = true,
    Background = "rbxassetid://0",
    BackgroundImageTransparency = 0.75,
    Duration = 12,
    CanClose = true,
    Buttons = {
        {
            Title = "Apply",
            Icon = "check",
            Variant = "Primary",
            CloseOnClick = false,
            Callback = function()
                print("Apply clicked")
            end,
        },
        {
            Title = "Dismiss",
            Icon = "x",
            Variant = "Secondary",
            CloseOnClick = true,
            Callback = function()
                print("Dismiss clicked")
            end,
        },
    },
})

task.delay(10, function()
    if n and not n.Closed then
        n:Close()
    end
end)
```

## Video Elements

`Video` embeds a `VideoFrame` as a UI element.

### Create

```lua
local Video = MainTab:Video({
    Video = "1234567890",
    Height = 220,
    Looped = true,
    Playing = false,
    Volume = 0.5,
    Visible = true,
})
```

### Config

| Key | Type | Default | Notes |
| --- | --- | --- | --- |
| `Video` | `string \| number` | `""` | Numeric string/number auto-converts to `rbxassetid://...` |
| `Height` | `number` | `200` | Minimum `24` |
| `Looped` | `boolean` | `false` | Loop playback |
| `Playing` | `boolean` | `false` | Start playback immediately |
| `Volume` | `number` | `0.5` | Clamped `0` to `10` |
| `Visible` | `boolean` | `true` | Element visibility |
| `Radius` | `number` | element radius | Rounded corners |
| `Padding` | `number` | `5` | Inner padding around video |
| `Title` | `string?` | `"Video"` | Stored metadata |
| `Desc` | `string?` | `nil` | Stored metadata |

### Methods

| Method | Signature | Description |
| --- | --- | --- |
| `Play` | `Video:Play()` | Starts playback |
| `Pause` | `Video:Pause()` | Pauses playback |
| `SetPlaying` | `Video:SetPlaying(isPlaying)` | True = play, else pause |
| `SetVideo` | `Video:SetVideo(source)` | Updates video source |
| `SetVolume` | `Video:SetVolume(volume)` | Updates clamped volume |
| `SetLooped` | `Video:SetLooped(looped)` | Enables/disables looping |
| `SetVisible` | `Video:SetVisible(visible)` | Toggles visibility |
| `SetHeight` | `Video:SetHeight(height)` | Updates element height |
| `Destroy` | `Video:Destroy()` | Destroys element |

### Full Example (All Video Methods)

```lua
local Video = MainTab:Video({
    Video = "1234567890",
    Height = 210,
    Looped = true,
    Playing = false,
    Volume = 0.4,
    Visible = true,
    Radius = 16,
    Padding = 6,
})

Video:Play()
task.wait(0.5)
Video:Pause()

Video:SetPlaying(true)
Video:SetVideo("rbxassetid://1234567890")
Video:SetVolume(1.2)
Video:SetLooped(false)
Video:SetVisible(true)
Video:SetHeight(240)
```

## Background Video

Background video is configured on `Window` and can be changed at runtime.

### Create with Video Background

```lua
local Window = WindUI:CreateWindow({
    Title = "Background Media",
    Folder = "WindUI-BG",
    BackgroundVideo = "1234567890",
})
```

Accepted video formats:

1. `number` (converted to `rbxassetid://...`)
2. numeric string (`"1234567890"`)
3. full `rbxassetid://...`
4. `"video:<source>"`
5. URL (`http/https`, with executor file API support recommended)

### Runtime Methods

| Method | Signature | Returns | Description |
| --- | --- | --- | --- |
| `SetBackgroundVideo` | `Window:SetBackgroundVideo(video)` | `boolean` | Switches to video background |
| `SetBackgroundImage` | `Window:SetBackgroundImage(image)` | `boolean` | Switches to image background |
| `SetBackgroundImageTransparency` | `Window:SetBackgroundImageTransparency(v)` | `nil` | Sets image transparency |
| `SetBackgroundTransparency` | `Window:SetBackgroundTransparency(v)` | `nil` | Sets global window transparency state |

### Full Example (Background Video Methods)

```lua
Window:SetBackgroundVideo("1234567890")
Window:SetBackgroundVideo("video:rbxassetid://1234567890")

Window:SetBackgroundImage("rbxassetid://987654321")
Window:SetBackgroundImageTransparency(0.35)

Window:SetBackgroundTransparency(0.2)
```

## Watermark

`Watermark` adds a floating text label over the window background.

### Create with Watermark

```lua
local Window = WindUI:CreateWindow({
    Title = "Watermark Demo",
    Folder = "WindUI-Watermark",
    Watermark = {
        Enabled = true,
        Text = " | v1.0.0",
        Opacity = 0.45,
        Position = "bottom-right",
        Size = 14,
        Padding = 12,
        Offset = Vector2.new(0, 0),
    },
})
```

### Config (`Watermark = {...}` or `Window:Watermark({...})`)

| Key | Type | Default | Notes |
| --- | --- | --- | --- |
| `Enabled` | `boolean` | `true` | Initial visibility |
| `Text` | `string` | `"Watermark"` | Display text |
| `Opacity` | `number` | `0.45` | Clamped `0` to `1` |
| `Position` | `string \| UDim2` | `"bottom-right"` | Preset string or custom `UDim2` |
| `Size` | `number` | `14` | Minimum `8` |
| `Padding` | `number` | `12` | Used by preset positions |
| `Offset` | `Vector2` | `Vector2.new(0, 0)` | Position offset |
| `Color` | `Color3?` | themed text | Optional explicit text color |
| `RichText` | `boolean` | `false` | Enables rich text tags |
| `AnchorPoint` | `Vector2?` | `Vector2.new(0.5, 0.5)` | Used when `Position` is `UDim2` |

Preset `Position` strings:
`top-left`, `top-center`, `top-right`, `center-left`, `center`, `center-right`, `bottom-left`, `bottom-center`, `bottom-right`.

### Runtime Methods

| Method | Signature | Description |
| --- | --- | --- |
| `Watermark` | `Window:Watermark(config)` | Creates/replaces watermark and returns object |
| `CreateWatermark` | `Window:CreateWatermark(config)` | Alias of `Window:Watermark` |
| `SetEnabled` | `Watermark:SetEnabled(v)` | Shows/hides watermark |
| `SetText` | `Watermark:SetText(text)` | Updates watermark text |
| `SetOpacity` | `Watermark:SetOpacity(opacity)` | Updates text opacity |
| `SetPosition` | `Watermark:SetPosition(position)` | Sets preset position or custom `UDim2` |
| `SetOffset` | `Watermark:SetOffset(offset)` | Updates `Vector2` offset |
| `SetPadding` | `Watermark:SetPadding(px)` | Updates preset position padding |
| `SetSize` | `Watermark:SetSize(px)` | Updates text size |
| `Destroy` | `Watermark:Destroy()` | Removes watermark instance |

### Full Example (All Watermark Methods)

```lua
local WM = Window:Watermark({
    Text = "Shiny | Build 240",
    Position = "top-right",
    Opacity = 0.55,
    Size = 15,
    Padding = 14,
    Offset = Vector2.new(-4, 2),
    RichText = true,
})

WM:SetText("Shiny | <font transparency=\"0.2\">Build 241</font>")
WM:SetOpacity(0.7)
WM:SetPosition("bottom-left")
WM:SetPosition(UDim2.new(0.5, 0, 0, 24))
WM:SetOffset(Vector2.new(0, 0))
WM:SetPadding(12)
WM:SetSize(14)

WM:SetEnabled(false)
task.wait(0.25)
WM:SetEnabled(true)
```

## ModernLayout

`ModernLayout` is a window-level style mode enabled at creation time.

### Create

```lua
local ModernWindow = WindUI:CreateWindow({
    Title = "Modern Window",
    Folder = "WindUI-Modern",
    ModernLayout = true,
    ElementsRadius = 24,
})
```

### What It Changes

1. Uses a tighter default element padding (`10` instead of `13`).
2. Uses larger default element corner radius (`23` instead of `12`).
3. Uses compact tab spacing (`1` instead of `6`) for tab content.
4. Uses glass-style outlines for several components (tabs, sections, multi sections, video).
5. Recalculates element shapes for visual consistency.

### Runtime

There is no dedicated runtime `SetModernLayout(...)` method; choose this mode when creating the window.

## BottomDragBarEnabled

Controls the bottom drag handle visibility/behavior on the window.

### CreateWindow Options

| Key | Type | Default | Notes |
| --- | --- | --- | --- |
| `BottomDragBarEnabled` | `boolean` | `true` | Main option |
| `BottomDragEnabled` | `boolean` | `true` | Alias; same behavior |

`BottomDragBarEnabled` is internally treated as:

```lua
not (Config.BottomDragBarEnabled == false or Config.BottomDragEnabled == false)
```

### Runtime Method

| Method | Signature | Description |
| --- | --- | --- |
| `SetBottomDragBarEnabled` | `Window:SetBottomDragBarEnabled(v)` | Enables/disables bottom drag bar at runtime |

### Example

```lua
local Window = WindUI:CreateWindow({
    Title = "Bottom Drag Demo",
    Folder = "WindUI-BottomDrag",
    BottomDragBarEnabled = true,
})

Window:SetBottomDragBarEnabled(false)
task.wait(0.5)
Window:SetBottomDragBarEnabled(true)
```

## Button Keybind

`ButtonKeybind` combines a clickable row + assignable key trigger that runs a callback.

### Create

```lua
local BK = MainTab:ButtonKeybind({
    Title = "Quick Action",
    Desc = "Click row or press key",
    Icon = "mouse-pointer-click",
    IconThemed = true,
    Color = "Accent",
    Justify = "Between",
    IconAlign = "Right",
    Value = Enum.KeyCode.F,
    CanChange = true,
    Locked = false,
    Callback = function(trigger)
        print("Action triggered by:", trigger)
    end,
})
```

### Config

| Key | Type | Default |
| --- | --- | --- |
| `Title` | `string` | `"Button Keybind"` |
| `Desc` | `string?` | `nil` |
| `Icon` | `string` | `"mouse-pointer-click"` |
| `IconThemed` | `boolean` | `false` |
| `Color` | `string \| Color3?` | `nil` |
| `Justify` | `string` | `"Between"` |
| `IconAlign` | `"Left" \| "Right"` | `"Right"` |
| `Locked` | `boolean` | `false` |
| `LockedTitle` | `string?` | `nil` |
| `Callback` | `function` | empty function |
| `Value` | `EnumItem \| string` | `"F"` |
| `CanChange` | `boolean` | `true` |
| `Size` | `"Small" \| "Default" \| "Large"` | `"Default"` |

### Methods

| Method | Signature | Description |
| --- | --- | --- |
| `Lock` | `BK:Lock()` | Locks interaction |
| `Unlock` | `BK:Unlock()` | Unlocks interaction |
| `Set` | `BK:Set(keyOrEnum)` | Sets current trigger key |
| `SetTitle` | `BK:SetTitle(text)` | Updates visible title |
| `SetDesc` | `BK:SetDesc(text)` | Updates visible description |
| `Highlight` | `BK:Highlight()` | Brief highlight animation |

### Full Example (All Button Keybind Methods)

```lua
local BK = MainTab:ButtonKeybind({
    Title = "Quick Action",
    Desc = "Default key: F",
    Value = "F",
    CanChange = true,
    Callback = function(trigger)
        print("ButtonKeybind callback:", trigger or "MouseClick")
    end,
})

BK:Set("MouseRight")
BK:SetTitle("Quick Action Key")
BK:SetDesc("Right mouse now triggers action")
BK:Highlight()

BK:Lock()
task.wait(0.5)
BK:Unlock()
```

## Toggle Keybind

`ToggleKeybind` combines a toggle/checkbox control with an assignable hotkey.

### Create

```lua
local TK = MainTab:ToggleKeybind({
    Title = "Kill Aura",
    Desc = "Toggle with keybind",
    Type = "Toggle",
    Value = false,
    Keybind = Enum.KeyCode.G,
    CanChange = true,
    Callback = function(state)
        print("Kill Aura:", state)
    end,
})
```

### Config

| Key | Type | Default |
| --- | --- | --- |
| `Title` | `string` | `"Toggle Keybind"` |
| `Desc` | `string?` | `nil` |
| `Locked` | `boolean` | `false` |
| `LockedTitle` | `string?` | `nil` |
| `Value` | `boolean` | `false` |
| `Icon` | `string?` | `nil` |
| `IconSize` | `number` | `23` |
| `Type` | `"Toggle" \| "Checkbox"` | `"Toggle"` |
| `Callback` | `function` | empty function |
| `Keybind` / `Bind` / `Key` | `EnumItem \| string` | `"F"` |
| `CanChange` | `boolean` | `true` |

### Methods

| Method | Signature | Description |
| --- | --- | --- |
| `Lock` | `TK:Lock()` | Locks interaction |
| `Unlock` | `TK:Unlock()` | Unlocks interaction |
| `Set` | `TK:Set(value, isCallback, isAnim)` | Sets toggle value |
| `SetKeybind` | `TK:SetKeybind(keyOrEnum)` | Sets activation key |
| `SetTitle` | `TK:SetTitle(text)` | Updates visible title |
| `SetDesc` | `TK:SetDesc(text)` | Updates visible description |
| `Highlight` | `TK:Highlight()` | Brief highlight animation |

### Full Example (All Toggle Keybind Methods)

```lua
local TK = MainTab:ToggleKeybind({
    Title = "Kill Aura",
    Desc = "Press G to toggle",
    Type = "Checkbox",
    Value = false,
    Keybind = "G",
    CanChange = true,
    Callback = function(state)
        print("Toggle state:", state)
    end,
})

TK:Set(true, true, false)
TK:Set(false, false, true)
TK:SetKeybind("MouseLeft")

TK:SetTitle("Kill Aura Key")
TK:SetDesc("Now bound to left mouse")
TK:Highlight()

TK:Lock()
task.wait(0.5)
TK:Unlock()
```

## Multi Section (Locked)

Locking a multi section disables header interaction, prevents tab click switching, and locks lockable child elements in all tabs.

### Lock-Oriented Example

```lua
local LockedMulti = MainTab:MultiSection({
    Title = "Protected Profiles",
    Desc = "Requires unlock",
    Locked = true,
    LockedTitle = "Unlock first",
    Box = true,
    Opened = true,
})

local Basic = LockedMulti:Tab({ Title = "Basic", Selected = true })
Basic:Toggle({ Title = "Enabled", Value = true })

local Advanced = LockedMulti:Tab({ Title = "Advanced" })
Advanced:Slider({ Title = "Power", Value = { Min = 0, Max = 100, Default = 50 } })

LockedMulti:Unlock()
LockedMulti:SelectTab("Advanced")
LockedMulti:Open(true)

LockedMulti:Lock()
LockedMulti:Close()
```

### Lock Notes

1. `LockedTitle` is stored but currently has no built-in visual lock label for this container.
2. Programmatic `SelectTab(...)` still works even when locked; click selection is blocked.

## Section (Locked)

A locked section disables expand/collapse click and locks lockable child elements.

### Section Methods

| Method | Signature | Description |
| --- | --- | --- |
| `SetIcon` | `Section:SetIcon(iconOrNil)` | Updates/removes icon |
| `SetTitle` | `Section:SetTitle(title)` | Updates title |
| `SetDesc` | `Section:SetDesc(descOrNil)` | Updates description |
| `Lock` | `Section:Lock()` | Locks section + lockable children |
| `Unlock` | `Section:Unlock()` | Unlocks section + lockable children |
| `Open` | `Section:Open(isNotAnim)` | Opens (if expandable) |
| `Close` | `Section:Close(isNotAnim)` | Closes (if expandable) |
| `Destroy` | `Section:Destroy()` | Destroys section and child elements |

Like tab containers, section containers also receive element constructors:
`Paragraph`, `Button`, `ButtonKeybind`, `Toggle`, `ToggleKeybind`, `Slider`, `Keybind`, `Input`, `Dropdown`, `Code`, `Colorpicker`, `Section`, `MultiSection`, `Divider`, `Space`, `Image`, `Group`, `Video`.

### Lock-Oriented Example (All Section Methods)

```lua
local Secure = MainTab:Section({
    Title = "Secure Settings",
    Desc = "Locked by default",
    Icon = "lock",
    Box = true,
    BoxBorder = true,
    Opened = true,
    Locked = true,
    LockedTitle = "Unlock to edit",
})

Secure:Toggle({
    Title = "God Mode",
    Value = false,
})

Secure:SetIcon("shield")
Secure:SetTitle("Protected Settings")
Secure:SetDesc("Unlock to change values")

Secure:Unlock()
Secure:Open(true)
Secure:Close(false)

Secure:Lock()
```

### Lock Notes

1. `LockedTitle` is stored but currently has no built-in lock-label renderer in this section container.
2. `Open`/`Close` only affect expandable sections (sections with child elements).
