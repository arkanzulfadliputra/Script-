## Open Ui
```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("Kavo UI", "DarkTheme")

-- Create UI Tabs
local Tab = Window:NewTab("Main")
local Section = Tab:NewSection("Control UI")

-- Function to toggle UI
local function ToggleUI(state)
    local ScreenGui = game.CoreGui:FindFirstChild("ScreenGui")
    if ScreenGui then
        ScreenGui.Enabled = state
    end
end

-- Close Button inside UI
Section:NewButton("Close UI", "Hides the UI", function()
    ToggleUI(false)
end)

-- Create an Open Button (Outside UI)
local OpenButton = Instance.new("TextButton")
OpenButton.Parent = game.CoreGui
OpenButton.Size = UDim2.new(0, 100, 0, 50) -- Button size
OpenButton.Position = UDim2.new(0, 10, 0, 10) -- Button position
OpenButton.Text = "Open UI"
OpenButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0) -- Green color
OpenButton.TextScaled = true

-- Open Button Functionality
OpenButton.MouseButton1Click:Connect(function()
    ToggleUI(true)
end)
```

## Close Ui
```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("Kavo UI with Close Button", "DarkTheme")

-- Create a tab
local Tab = Window:NewTab("Main")
local Section = Tab:NewSection("Close UI")

-- Close button
Section:NewButton("Close UI", "Click to close", function()
    for _, v in pairs(game.CoreGui:GetChildren()) do
        if v.Name == "ScreenGui" then -- Adjust if necessary
            v:Destroy()
        end
    end
end)
```
## Hide Ui
```lua
Section:NewButton("Hide UI", "Click to hide", function()
    local ScreenGui = game.CoreGui:FindFirstChild("ScreenGui")
    if ScreenGui then
        ScreenGui.Enabled = not ScreenGui.Enabled -- Toggles visibility
    end
end)
```
## Icon Ui
```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("🔥 Kavo UI with Icon", "DarkTheme") -- Fire emoji as an icon


task.spawn(function()
    wait(1) -- Wait for UI to load
    local ScreenGui = game.CoreGui:FindFirstChild("ScreenGui") -- Change if needed
    if ScreenGui then
        local MainFrame = ScreenGui:FindFirstChild("Main") -- Locate UI main frame
        if MainFrame then
            -- Create an ImageLabel
            local Icon = Instance.new("ImageLabel")
            Icon.Parent = MainFrame
            Icon.Size = UDim2.new(0, 50, 0, 50) -- Adjust size
            Icon.Position = UDim2.new(0, 10, 0, 10) -- Adjust position
            Icon.Image = "rbxassetid://1234567890" -- Replace with your icon ID
            Icon.BackgroundTransparency = 1 -- Remove background
        end
    end
end)
```
## Notify Ui
```lua

local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("Kavo UI Notifications", "DarkTheme")

-- Create a tab for notifications
local Tab = Window:NewTab("Notifications")
local Section = Tab:NewSection("Notification System")

-- Function to send notifications
Section:NewButton("Show Notification", "Click to notify", function()
    Library:Notify("Notification Title", "This is a test notification!")
end)
```
## 2 Adding Notify
```lua
function NotifyCustom(title, message, duration)
    Library:Notify(title, message)
    task.wait(duration or 3) -- Wait for the given duration
end

Section:NewButton("Custom Notify", "Shows for 5 seconds", function()
    NotifyCustom("Alert!", "This notification lasts 5 seconds.", 5)
end)
```
## Movable Ui
```lua
-- Load Kavo UI
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("Movable Kavo UI", "DarkTheme")

-- Make the UI draggable
local function MakeDraggable(frame)
    local UserInputService = game:GetService("UserInputService")
    local dragging, dragInput, startPos, startMousePos

    local function update(input)
        local delta = input.Position - startMousePos
        frame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end

    frame.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragging = true
            startPos = frame.Position
            startMousePos = input.Position

            input.Changed:Connect(function()
                if input.UserInputState == Enum.UserInputState.End then
                    dragging = false
                end
            end)
        end
    end)

    frame.InputChanged:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseMovement then
            dragInput = input
        end
    end)

    UserInputService.InputChanged:Connect(function(input)
        if input == dragInput and dragging then
            update(input)
        end
    end)
end

-- Apply draggable function to the Kavo UI frame
task.spawn(function()
    wait(1) -- Wait for UI to load
    local ScreenGui = game.CoreGui:FindFirstChild("ScreenGui") -- Change this if needed
    if ScreenGui then
        local MainFrame = ScreenGui:FindFirstChild("Main") -- Adjust based on UI structure
        if MainFrame then
            MakeDraggable(MainFrame)
        end
    end
end)

-- Create a tab
local Tab = Window:NewTab("Movable UI")
local Section = Tab:NewSection("Drag the window freely!")
```
## Key System
```lua
local Library = loadstring(game:HttpGet("https://raw.githubusercontent.com/xHeptc/Kavo-UI-Library/main/source.lua"))()
local Window = Library.CreateLib("Key System", "DarkTheme")

local Key = "MySecretKey123" -- Set your secret key here

-- Create the main tab
local Tab = Window:NewTab("Key System")
local Section = Tab:NewSection("Enter Key")

-- Key input
local KeyInput
Section:NewTextBox("Enter Key", "Type here...", function(value)
    KeyInput = value
end)

-- Submit button
Section:NewButton("Submit", "Check Key", function()
    if KeyInput == Key then
        Library:Notify("Access Granted!", "Correct key entered!")
        
        -- Load your script here after successful key input
        loadstring(game:HttpGet("https://your-script-link.com/script.lua"))()
        
    else
        Library:Notify("Access Denied!", "Incorrect key!")
    end
end)
```
