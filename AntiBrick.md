# Tunx
-- Instances:

local ScreenGui = Instance.new("ScreenGui")
local Frame = Instance.new("Frame")
local TextLabel = Instance.new("TextLabel")
local TextButton = Instance.new("TextButton")

--Properties:

ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
ScreenGui.ResetOnSpawn = false

Frame.Parent = ScreenGui
Frame.BackgroundColor3 = Color3.fromRGB(144, 238, 144)
Frame.BorderColor3 = Color3.fromRGB(255, 0, 0)
Frame.BorderSizePixel = 0
Frame.Position = UDim2.new(0.390366644, 0, 0.301782697, 0)
Frame.Size = UDim2.new(0, 163, 0, 82)
Frame.Active = true
Frame.Draggable = true

TextLabel.Parent = Frame
TextLabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
TextLabel.BorderColor3 = Color3.fromRGB(255, 0, 0)
TextLabel.BorderSizePixel = 0
TextLabel.Size = UDim2.new(0, 163, 0, 23)
TextLabel.Font = Enum.Font.SourceSansBold
TextLabel.Text = "Truong Ky AntiBrick"
TextLabel.TextColor3 = Color3.fromRGB(0, 0, 0)
TextLabel.TextSize = 18.000

TextButton.Parent = Frame
TextButton.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
TextButton.BorderColor3 = Color3.fromRGB(255, 255, 255)
TextButton.BorderSizePixel = 0
TextButton.Position = UDim2.new(0.175683141, 0, 0.408666462, 0)
TextButton.Size = UDim2.new(0, 104, 0, 31)
TextButton.Font = Enum.Font.SourceSansItalic
TextButton.Text = "Đóng"
TextButton.TextColor3 = Color3.fromRGB(255, 255, 255)
TextButton.TextSize = 15.000

-- Scripts:

local function LILMOQ_fake_script() -- TextButton.LocalScript 
    local script = Instance.new('LocalScript', TextButton)

    local player = game:GetService("Players").LocalPlayer
    local nega = true
    
    local toggleButton = script.Parent
    
    local function updateButtonText()
        if nega then
            toggleButton.Text = "Đóng"
        else
            toggleButton.Text = "Mở"
        end
    end
    
    local function toggleFeature()
        nega = not nega
        updateButtonText()
    end
    
    toggleButton.MouseButton1Click:Connect(function()
        toggleFeature()
    end)
    
    local function applyToggleEffect()
        while task.wait() do
            local character = player.Character or player.CharacterAdded:Wait()
            local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
            local parts = workspace:GetPartBoundsInRadius(humanoidRootPart.Position, 10)
            for _, part in ipairs(parts) do
                part.CanTouch = nega
            end
        end
    end
    
    player.CharacterAdded:Connect(function()
        applyToggleEffect()
        updateButtonText()
    end)
    
    applyToggleEffect()
    updateButtonText()
    
end
coroutine.wrap(LILMOQ_fake_script)()