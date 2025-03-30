## Loading
```lua
local LoadingScreen = XSX:CreateWindow("Loading...")
local LoadingLabel = LoadingScreen:CreateLabel("Please wait...")

-- Simulate Loading Delay
task.spawn(function()
    for i = 1, 5 do -- 5 seconds loading
        LoadingLabel:SetText("Loading... " .. i .. "/5")
        task.wait(1)
    end
    LoadingScreen:Destroy() -- Remove loading screen
end)

-- Wait before showing the main UI
task.wait(5)
```

## screengui loading
```lua
-- Create a ScreenGui
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = game.CoreGui
ScreenGui.Name = "LoadingScreen"

-- Create a Frame (Background)
local Frame = Instance.new("Frame")
Frame.Parent = ScreenGui
Frame.Size = UDim2.new(1, 0, 1, 0)
Frame.Position = UDim2.new(0, 0, 0, 0)
Frame.BackgroundColor3 = Color3.fromRGB(15, 15, 15) -- Dark background

-- Create a Loading Text Label
local LoadingText = Instance.new("TextLabel")
LoadingText.Parent = Frame
LoadingText.Size = UDim2.new(0, 300, 0, 50)
LoadingText.Position = UDim2.new(0.5, -150, 0.5, -25)
LoadingText.BackgroundTransparency = 1
LoadingText.TextColor3 = Color3.fromRGB(255, 255, 255)
LoadingText.TextSize = 24
LoadingText.Font = Enum.Font.SourceSansBold
LoadingText.Text = "Loading..."

-- Animate Loading Dots
task.spawn(function()
    local dots = ""
    while task.wait(0.5) do
        dots = dots == "..." and "" or dots .. "."
        LoadingText.Text = "Loading" .. dots
    end
end)

-- Simulate a Loading Delay
task.wait(5) -- Adjust this for longer loading

-- Fade Out and Remove the Loading Screen
for i = 1, 10 do
    Frame.BackgroundTransparency = i * 0.1
    LoadingText.TextTransparency = i * 0.1
    task.wait(0.1)
end

ScreenGui:Destroy() -- Remove loading screen after fade-out

print("Loading Complete!")
```
## Key System
```lua
-- Define the correct key
local CorrectKey = "YourSecureKey123" -- Change this to your own key

-- Create a ScreenGui
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = game.CoreGui
ScreenGui.Name = "KeySystem"

-- Create a Frame
local Frame = Instance.new("Frame")
Frame.Parent = ScreenGui
Frame.Size = UDim2.new(0, 300, 0, 150)
Frame.Position = UDim2.new(0.5, -150, 0.5, -75)
Frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Frame.BorderSizePixel = 2

-- Create a TextLabel (Title)
local Title = Instance.new("TextLabel")
Title.Parent = Frame
Title.Size = UDim2.new(1, 0, 0.3, 0)
Title.Position = UDim2.new(0, 0, 0, 0)
Title.BackgroundTransparency = 1
Title.Text = "Enter Key"
Title.TextSize = 20
Title.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Create a TextBox (User Input)
local KeyBox = Instance.new("TextBox")
KeyBox.Parent = Frame
KeyBox.Size = UDim2.new(0.8, 0, 0.3, 0)
KeyBox.Position = UDim2.new(0.1, 0, 0.4,
```
## open ui
```lua
-- Create a ScreenGui
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = game.CoreGui
ScreenGui.Name = "ToggleUI"

-- Create a Frame (Main UI)
local Frame = Instance.new("Frame")
Frame.Parent = ScreenGui
Frame.Size = UDim2.new(0, 400, 0, 250)
Frame.Position = UDim2.new(0.5, -200, 0.5, -125)
Frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Frame.BorderSizePixel = 2
Frame.Visible = true -- UI starts visible

-- Create a TextLabel (Title)
local Title = Instance.new("TextLabel")
Title.Parent = Frame
Title.Size = UDim2.new(1, 0, 0.2, 0)
Title.Position = UDim2.new(0, 0, 0, 0)
Title.BackgroundTransparency = 1
Title.Text = "My Custom UI"
Title.TextSize = 20
Title.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Create a Toggle Keybind (RightShift to Open/Close)
local UserInputService = game:GetService("UserInputService")

UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if not gameProcessed and input.KeyCode == Enum.KeyCode.RightShift then
        Frame.Visible = not Frame.Visible -- Toggle UI
    end
end)

print("UI Toggle Script Loaded! Press RightShift to open/close.")
```
## Close Ui
```lua
-- Create a ScreenGui
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = game.CoreGui
ScreenGui.Name = "ClosableUI"

-- Create a Frame (Main UI)
local Frame = Instance.new("Frame")
Frame.Parent = ScreenGui
Frame.Size = UDim2.new(0, 400, 0, 250)
Frame.Position = UDim2.new(0.5, -200, 0.5, -125)
Frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Frame.BorderSizePixel = 2

-- Create a TextLabel (Title)
local Title = Instance.new("TextLabel")
Title.Parent = Frame
Title.Size = UDim2.new(1, 0, 0.2, 0)
Title.Position = UDim2.new(0, 0, 0, 0)
Title.BackgroundTransparency = 1
Title.Text = "My UI"
Title.TextSize = 20
Title.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Create a Close Button
local CloseButton = Instance.new("TextButton")
CloseButton.Parent = Frame
CloseButton.Size = UDim2.new(0.2, 0, 0.2, 0)
CloseButton.Position = UDim2.new(0.8, 0, 0, 0)
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
CloseButton.Text = "X"
CloseButton.TextSize = 20
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Close Button Function
CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
    print("UI Closed!")
end)

-- Keybind to Close UI (Backspace)
local UserInputService = game:GetService("UserInputService")

UserInputService.InputBegan:Connect(function(input, gameProcessed)
    if not gameProcessed and input.KeyCode ==
```
## Gamepass
```lua
local Players = game:GetService("Players")
local MarketplaceService = game:GetService("MarketplaceService")

local GamePassID = 12345678 -- Replace with your actual GamePass ID

-- Function to check if a player owns the GamePass
local function hasGamePass(player)
    local success, result = pcall(function()
        return MarketplaceService:UserOwnsGamePassAsync(player.UserId, GamePassID)
    end)
    return success and result
end

-- Function to prompt purchase
local function promptPurchase(player)
    MarketplaceService:PromptGamePassPurchase(player, GamePassID)
end

-- When a player joins, check if they own the GamePass
Players.PlayerAdded:Connect(function(player)
    if hasGamePass(player) then
        print(player.Name .. " owns the GamePass!")
        -- Grant the player access to perks here
    else
        print(player.Name .. " does not own the GamePass.")
    end
end)

-- Example: Command to prompt purchase when a button is clicked
local function onButtonClick(player)
    if not hasGamePass(player) then
        promptPurchase(player)
    else
        print("You already own the GamePass!")
    end
end

-- Example usage: Replace with actual UI button event
-- Button.MouseButton1Click:Connect(function() onButtonClick(game.Players.LocalPlayer) end)
```
## Gui Shop
```lua
local Players = game:GetService("Players")
local MarketplaceService = game:GetService("MarketplaceService")

-- Replace with your Developer Product ID
local ProductID = 12345678 

-- Create a ScreenGui
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = game.CoreGui
ScreenGui.Name = "ShopGUI"

-- Create a Frame (Shop UI)
local Frame = Instance.new("Frame")
Frame.Parent = ScreenGui
Frame.Size = UDim2.new(0, 300, 0, 200)
Frame.Position = UDim2.new(0.5, -150, 0.5, -100)
Frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Frame.BorderSizePixel = 2

-- Create a Title Label
local Title = Instance.new("TextLabel")
Title.Parent = Frame
Title.Size = UDim2.new(1, 0, 0.2, 0)
Title.Position = UDim2.new(0, 0, 0, 0)
Title.BackgroundTransparency = 1
Title.Text = "Shop"
Title.TextSize = 20
Title.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Create a Purchase Button
local BuyButton = Instance.new("TextButton")
BuyButton.Parent = Frame
BuyButton.Size = UDim2.new(0.8, 0, 0.3, 0)
BuyButton.Position = UDim2.new(0.1, 0, 0.4, 0)
BuyButton.BackgroundColor3 = Color3.fromRGB(70, 130, 180)
BuyButton.Text = "Buy Item (50 Robux)"
BuyButton.TextSize = 18
BuyButton.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Close Button
local CloseButton = Instance.new("TextButton")
CloseButton.Parent = Frame
CloseButton.Size = UDim2.new(0.2, 0, 0.2, 0)
CloseButton.Position = UDim2.new(0.8, 0, 0, 0)
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
CloseButton.Text = "X"
CloseButton.TextSize = 20
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Function to prompt purchase
BuyButton.MouseButton1Click:Connect(function()
    local player = Players.LocalPlayer
    MarketplaceService:PromptProductPurchase(player, ProductID)
end)

-- Close Button Function
CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

print("Shop GUI Loaded! Click Buy to purchase an item.")
```
## Admin Panel
```lua
local Players = game:GetService("Players")

-- Create a ScreenGui
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = game.CoreGui
ScreenGui.Name = "AdminPanel"

-- Create a Frame (Admin UI)
local Frame = Instance.new("Frame")
Frame.Parent = ScreenGui
Frame.Size = UDim2.new(0, 300, 0, 200)
Frame.Position = UDim2.new(0.5, -150, 0.5, -100)
Frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Frame.BorderSizePixel = 2

-- Create a Title Label
local Title = Instance.new("TextLabel")
Title.Parent = Frame
Title.Size = UDim2.new(1, 0, 0.2, 0)
Title.BackgroundTransparency = 1
Title.Text = "Admin Panel"
Title.TextSize = 20
Title.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Create a Player Input Box
local PlayerBox = Instance.new("TextBox")
PlayerBox.Parent = Frame
PlayerBox.Size = UDim2.new(0.8, 0, 0.2, 0)
PlayerBox.Position = UDim2.new(0.1, 0, 0.3, 0)
PlayerBox.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
PlayerBox.TextSize = 16
PlayerBox.TextColor3 = Color3.fromRGB(255, 255, 255)
PlayerBox.PlaceholderText = "Enter Player Name"

-- Create Kick Button
local KickButton = Instance.new("TextButton")
KickButton.Parent = Frame
KickButton.Size = UDim2.new(0.8, 0, 0.2, 0)
KickButton.Position = UDim2.new(0.1, 0, 0.55, 0)
KickButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
KickButton.Text = "Kick Player"
KickButton.TextSize = 18
KickButton.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Create a Close Button
local CloseButton = Instance.new("TextButton")
CloseButton.Parent = Frame
CloseButton.Size = UDim2.new(0.2, 0, 0.2, 0)
CloseButton.Position = UDim2.new(0.8, 0, 0, 0)
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
CloseButton.Text = "X"
CloseButton.TextSize = 20
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Kick Player Function
KickButton.MouseButton1Click:Connect(function()
    local playerName = PlayerBox.Text
    local player = Players:FindFirstChild(playerName)
    
    if player then
        player:Kick("You have been kicked by an Admin!")
        print("Kicked player: " .. playerName)
    else
        print("Player not found!")
    end
end)

-- Close Button Function
CloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

print("Admin Panel Loaded! Use it to kick players.")
```
## Admin Panel Doors
```lua
local Players = game:GetService("Players")

-- Create a ScreenGui
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Parent = game.CoreGui
ScreenGui.Name = "AdminDoorPanel"

-- Create a Frame (Admin UI)
local Frame = Instance.new("Frame")
Frame.Parent = ScreenGui
Frame.Size = UDim2.new(0, 300, 0, 250)
Frame.Position = UDim2.new(0.5, -150, 0.5, -125)
Frame.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
Frame.BorderSizePixel = 2

-- Create a Title Label
local Title = Instance.new("TextLabel")
Title.Parent = Frame
Title.Size = UDim2.new(1, 0, 0.2, 0)
Title.BackgroundTransparency = 1
Title.Text = "Admin Door Panel"
Title.TextSize = 20
Title.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Create a Door Input Box
local DoorBox = Instance.new("TextBox")
DoorBox.Parent = Frame
DoorBox.Size = UDim2.new(0.8, 0, 0.2, 0)
DoorBox.Position = UDim2.new(0.1, 0, 0.25, 0)
DoorBox.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
DoorBox.TextSize = 16
DoorBox.TextColor3 = Color3.fromRGB(255, 255, 255)
DoorBox.PlaceholderText = "Enter Door Name"

-- Create Open Button
local OpenButton = Instance.new("TextButton")
OpenButton.Parent = Frame
OpenButton.Size = UDim2.new(0.8, 0, 0.15, 0)
OpenButton.Position = UDim2.new(0.1, 0, 0.5, 0)
OpenButton.BackgroundColor3 = Color3.fromRGB(0, 255, 0)
OpenButton.Text = "Open Door"
OpenButton.TextSize = 18
OpenButton.TextColor3 = Color3.fromRGB(0, 0, 0)

-- Create Close Button
local CloseButton = Instance.new("TextButton")
CloseButton.Parent = Frame
CloseButton.Size = UDim2.new(0.8, 0, 0.15, 0)
CloseButton.Position = UDim2.new(0.1, 0, 0.65, 0)
CloseButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
CloseButton.Text = "Close Door"
CloseButton.TextSize = 18
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Create Lock Button
local LockButton = Instance.new("TextButton")
LockButton.Parent = Frame
LockButton.Size = UDim2.new(0.8, 0, 0.15, 0)
LockButton.Position = UDim2.new(0.1, 0, 0.8, 0)
LockButton.BackgroundColor3 = Color3.fromRGB(128, 0, 128)
LockButton.Text = "Lock Door"
LockButton.TextSize = 18
LockButton.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Close Panel Button
local PanelCloseButton = Instance.new("TextButton")
PanelCloseButton.Parent = Frame
PanelCloseButton.Size = UDim2.new(0.2, 0, 0.2, 0)
PanelCloseButton.Position = UDim2.new(0.8, 0, 0, 0)
PanelCloseButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
PanelCloseButton.Text = "X"
PanelCloseButton.TextSize = 20
PanelCloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)

-- Function to Open Door
OpenButton.MouseButton1Click:Connect(function()
    local doorName = DoorBox.Text
    local door = game.Workspace:FindFirstChild(doorName)

    if door and door:IsA("Model") then
        for _, part in ipairs(door:GetChildren()) do
            if part:IsA("BasePart") then
                part.Transparency = 0.5
                part.CanCollide = false
            end
        end
        print("Opened door: " .. doorName)
    else
        print("Door not found!")
    end
end)

-- Function to Close Door
CloseButton.MouseButton1Click:Connect(function()
    local doorName = DoorBox.Text
    local door = game.Workspace:FindFirstChild(doorName)

    if door and door:IsA("Model") then
        for _, part in ipairs(door:GetChildren()) do
            if part:IsA("BasePart") then
                part.Transparency = 0
                part.CanCollide = true
            end
        end
        print("Closed door: " .. doorName)
    else
        print("Door not found!")
    end
end)

-- Function to Lock Door
LockButton.MouseButton1Click:Connect(function()
    local doorName = DoorBox.Text
    local door = game.Workspace:FindFirstChild(doorName)

    if door and door:IsA("Model") then
        for _, part in ipairs(door:GetChildren()) do
            if part:IsA("BasePart") then
                part.CanCollide = true
                part.Transparency = 0
            end
        end
        print("Locked door: " .. doorName)
    else
        print("Door not found!")
    end
end)

-- Close Panel Function
PanelCloseButton.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

print("Admin Door Panel Loaded! Use it to control doors.")
```
## Died
```lua
local Players = game:GetService("Players")

Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function(character)
        local humanoid = character:FindFirstChildOfClass("Humanoid")

        if humanoid then
            humanoid.Died:Connect(function()
                print(player.Name .. " has died!")
                
                -- Example: Show a death message
                local deathMessage = Instance.new("Message")
                deathMessage.Parent = game.Workspace
                deathMessage.Text = player.Name .. " has died!"
                
                -- Remove the message after 3 seconds
                wait(3)
                deathMessage:Destroy()
            end)
        end
    end)
end)
```
## Walkspeed
```lua
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:FindFirstChildOfClass("Humanoid")

if humanoid then
    humanoid.WalkSpeed = 50 -- Change this value to your desired speed
    print("WalkSpeed changed to " .. humanoid.WalkSpeed)
end
```
## Jump Power
```lua
local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local humanoid = character:FindFirstChildOfClass("Humanoid")

if humanoid then
    humanoid.JumpPower = 100 -- Change this value to your desired jump height
    print("Jump Power changed to " .. humanoid.JumpPower)
end
```
## error message
```lua
local Players = game:GetService("Players")

local function showError(player, message)
    local gui = Instance.new("ScreenGui")
    gui.Parent = player:FindFirstChild("PlayerGui")

    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(0.4, 0, 0.2, 0)
    frame.Position = UDim2.new(0.3, 0, 0.4, 0)
    frame.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
    frame.Parent = gui

    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(1, 0, 1, 0)
    label.Text = "Error: " .. message
    label.TextColor3 = Color3.fromRGB(255, 255, 255)
    label.TextScaled = true
    label.BackgroundTransparency = 1
    label.Parent = frame

    -- Remove the error message after 3 seconds
    task.wait(3)
    gui:Destroy()
end

-- Example Usage
local player = Players.LocalPlayer
showError(player, "Something went wrong!")
```
