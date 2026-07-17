# *UNTITLED CHARACTER GLIDER

##To use Untitled Character Glider for Roblox, you need to follow these steps:

1. Have a roblox executor / Roblox studio - This is the first requrirement that you need, if you want to use it anywhere else, Use an executor.

SETUP ROBLOX STUDIO / Optional

1. Open Roblox Studio.
2. Click "+ New Experience" On the top left side.
3. Put your Mouse Over "StarterGui".
4. Click The "+" Next to its name.
5. Select Local Script In the list.
6. Erase anything in the LocalScript e.g. "print("Hello world!")".
7. Paste This Entire Script Into Roblox Studio:

-- Script

``` luau

-- // CONFIGURATION //

local Settings = { Enabled = true, Cooldown = 3, MoveSpeed = 80, LastTrigger = 0, AimMode = false }



-- // SERVICES //

local UserInputService = game:GetService("UserInputService")

local RunService = game:GetService("RunService")

local TweenService = game:GetService("TweenService")

local player = game:GetService("Players").LocalPlayer

local mouse = player:GetMouse()



-- // SETUP //

if player.PlayerGui:FindFirstChild("GlideGui") then player.PlayerGui.GlideGui:Destroy() end

local screenGui = Instance.new("ScreenGui", player.PlayerGui)

screenGui.Name = "GlideGui"

screenGui.ResetOnSpawn = false 



-- // UI CONTAINERS //

local canvasGroup = Instance.new("CanvasGroup", screenGui)

canvasGroup.Size = UDim2.new(0, 480, 0, 260)

canvasGroup.Position = UDim2.new(0.5, -240, 0.5, -130)

canvasGroup.AnchorPoint = Vector2.new(0.5, 0.5)

canvasGroup.BackgroundTransparency = 1 -- Back to fully transparent



local main = Instance.new("Frame", canvasGroup)

main.Size = UDim2.new(1, 0, 1, 0)

main.BackgroundColor3 = Color3.fromRGB(25, 25, 25) -- Background color is here

Instance.new("UICorner", main).CornerRadius = UDim.new(0, 12) -- Corner styling is here



local icon = Instance.new("ImageButton", screenGui)

icon.Size = UDim2.new(0, 0, 0, 0)

icon.Position = UDim2.new(0.5, 0, 0.2, 0)

icon.AnchorPoint = Vector2.new(0.5, 0.5)

icon.BackgroundColor3 = Color3.fromRGB(25, 25, 25)

icon.Image = "rbxassetid://6319951708"

icon.Visible = false

Instance.new("UICorner", icon).CornerRadius = UDim.new(0, 12)



-- // DRAGGING //

local dragging, dragStart, startPos

local function enableDragging(object, target)

    object.InputBegan:Connect(function(input)

        if input.UserInputType == Enum.UserInputType.MouseButton1 then

            dragging = true; dragStart = input.Position; startPos = target.Position

        end

    end)

end

enableDragging(canvasGroup, canvasGroup)

enableDragging(icon, icon)



UserInputService.InputEnded:Connect(function(input) if input.UserInputType == Enum.UserInputType.MouseButton1 then dragging = false end end)

UserInputService.InputChanged:Connect(function(input)

    if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then

        local delta = input.Position - dragStart

        local target = icon.Visible and icon or canvasGroup

        target.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)

    end

end)



-- // ANIMATONS //

local pillBar = Instance.new("TextButton", main)

pillBar.Size = UDim2.new(0, 60, 0, 8); pillBar.Position = UDim2.new(0.5, -30, 0, 10); pillBar.BackgroundColor3 = Color3.fromRGB(100, 100, 100); pillBar.Text = ""

Instance.new("UICorner", pillBar).CornerRadius = UDim.new(1, 0)



local function toggleUI(open)

    local info = TweenInfo.new(0.4, Enum.EasingStyle.Exponential, Enum.EasingDirection.Out)

    if not open then

        TweenService:Create(canvasGroup, info, {GroupTransparency = 1, Size = UDim2.new(0, 0, 0, 0)}):Play()

        task.wait(0.2); icon.Visible = true; TweenService:Create(icon, info, {Size = UDim2.new(0, 60, 0, 60)}):Play()

    else

        TweenService:Create(icon, info, {Size = UDim2.new(0, 0, 0, 0)}):Play()

        task.wait(0.2); icon.Visible = false; canvasGroup.Size = UDim2.new(0, 480, 0, 260)

        TweenService:Create(canvasGroup, info, {GroupTransparency = 0}):Play()

    end

end

pillBar.MouseButton1Click:Connect(function() toggleUI(false) end)

icon.MouseButton1Click:Connect(function() toggleUI(true) end)



-- // UI ELEMENTS //

local title = Instance.new("TextLabel", main); title.Size = UDim2.new(1, 0, 0, 40); title.Position = UDim2.new(0, 20, 0, 15); title.Text = "UCG"; title.TextColor3 = Color3.new(1, 1, 1); title.Font = Enum.Font.GothamBold; title.TextSize = 18; title.BackgroundTransparency = 1; title.TextXAlignment = Enum.TextXAlignment.Left



-- Sidebar

local sidebar = Instance.new("Frame", main); sidebar.Size = UDim2.new(0, 160, 1, -60); sidebar.Position = UDim2.new(0, 10, 0, 50); sidebar.BackgroundColor3 = Color3.fromRGB(20, 20, 20); Instance.new("UICorner", sidebar).CornerRadius = UDim.new(0, 10)

local adjust = Instance.new("TextLabel", sidebar); adjust.Size = UDim2.new(1, -20, 0, 30); adjust.Position = UDim2.new(0, 10, 0, 10); adjust.Text = "Adjust"; adjust.TextColor3 = Color3.new(0, 0, 0); adjust.Font = Enum.Font.GothamBold; adjust.TextSize = 14; adjust.BackgroundColor3 = Color3.new(1, 1, 1); Instance.new("UICorner", adjust).CornerRadius = UDim.new(0, 8)

local btnActivate = Instance.new("TextButton", sidebar); btnActivate.Size = UDim2.new(1, -20, 0, 40); btnActivate.Position = UDim2.new(0, 10, 0, 50); btnActivate.Text = "Activate - Mobile Players"; btnActivate.TextColor3 = Color3.new(1, 1, 1); btnActivate.BackgroundColor3 = Color3.fromRGB(0, 120, 255); btnActivate.Font = Enum.Font.GothamBold; btnActivate.TextScaled = true; Instance.new("UICorner", btnActivate).CornerRadius = UDim.new(0, 8)



-- Settings Container

local container = Instance.new("Frame", main); container.Size = UDim2.new(1, -180, 1, -70); container.Position = UDim2.new(0, 180, 0, 60); container.BackgroundTransparency = 1

local hint = Instance.new("TextLabel", screenGui); hint.Size = UDim2.new(0, 400, 0, 50); hint.Position = UDim2.new(0.5, -200, 0.05, 0); hint.Text = "Click where you want to glide to!"; hint.TextColor3 = Color3.new(1, 1, 0); hint.Font = Enum.Font.GothamBold; hint.TextSize = 24; hint.Visible = false; hint.BackgroundTransparency = 1; hint.TextStrokeTransparency = 0

btnActivate.MouseButton1Click:Connect(function() Settings.AimMode = true; hint.Visible = true end)



-- // UI //

local function createSetting(name, val, callback, yOffset)

    local lbl = Instance.new("TextLabel", container); lbl.Size = UDim2.new(0.5, 0, 0, 30); lbl.Position = UDim2.new(0, 0, 0, yOffset); lbl.Text = name; lbl.TextColor3 = Color3.new(1, 1, 1); lbl.Font = Enum.Font.Gotham; lbl.TextSize = 14; lbl.BackgroundTransparency = 1; lbl.TextXAlignment = Enum.TextXAlignment.Left

    if type(val) == "boolean" then

        local btn = Instance.new("TextButton", container); btn.Size = UDim2.new(0, 60, 0, 30); btn.Position = UDim2.new(0.7, 0, 0, yOffset); btn.Text = ""; btn.BackgroundColor3 = Color3.fromRGB(15, 15, 15); Instance.new("UICorner", btn).CornerRadius = UDim.new(1, 0)

        local knob = Instance.new("Frame", btn); knob.Size = UDim2.new(0, 26, 0, 26); knob.Position = val and UDim2.new(0.5, 2, 0, 2) or UDim2.new(0, 2, 0, 2); knob.BackgroundColor3 = Color3.new(1, 1, 1); Instance.new("UICorner", knob).CornerRadius = UDim.new(1, 0)

        btn.MouseButton1Click:Connect(function() Settings.Enabled = not Settings.Enabled; knob:TweenPosition(Settings.Enabled and UDim2.new(0.5, 2, 0, 2) or UDim2.new(0, 2, 0, 2), "Out", "Quad", 0.2) end)

    else

        local bg = Instance.new("Frame", container); bg.Size = UDim2.new(0, 60, 0, 30); bg.Position = UDim2.new(0.5, 0, 0, yOffset); bg.BackgroundColor3 = Color3.fromRGB(15, 15, 15); Instance.new("UICorner", bg).CornerRadius = UDim.new(0, 8)

        local box = Instance.new("TextBox", bg); box.Size = UDim2.new(1, 0, 1, 0); box.Text = tostring(val); box.TextColor3 = Color3.new(1, 1, 1); box.BackgroundTransparency = 1; box.Font = Enum.Font.Gotham; box.TextSize = 14

        local set = Instance.new("TextButton", container); set.Size = UDim2.new(0, 60, 0, 30); set.Position = UDim2.new(0.75, 0, 0, yOffset); set.Text = "Set"; set.TextColor3 = Color3.new(1, 1, 1); set.BackgroundColor3 = Color3.fromRGB(15, 15, 15); Instance.new("UICorner", set).CornerRadius = UDim.new(0, 8)

        set.MouseButton1Click:Connect(function() callback(tonumber(box.Text) or val) end)

    end

end



createSetting("Ctrl+Click Glide", Settings.Enabled, nil, 0)

createSetting("Cooldown (s)", Settings.Cooldown, function(v) Settings.Cooldown = v end, 50)

createSetting("Move Speed", Settings.MoveSpeed, function(v) Settings.MoveSpeed = v end, 100)



-- // PLAYER GLIDE //

UserInputService.InputBegan:Connect(function(input, gpe)

    if gpe or input.UserInputType ~= Enum.UserInputType.MouseButton1 then return end

    local canTrigger = Settings.AimMode or UserInputService:IsKeyDown(Enum.KeyCode.LeftControl)

    if canTrigger and Settings.Enabled and (tick() - Settings.LastTrigger >= Settings.Cooldown) then

        local char = player.Character; local humRoot = char and char:FindFirstChild("HumanoidRootPart")

        if humRoot then

            local targetPos = mouse.Hit.Position; local direction = (targetPos - humRoot.Position).Unit

            local duration = (targetPos - humRoot.Position).Magnitude / Settings.MoveSpeed 

            player.Character.Humanoid.PlatformStand = true; Settings.AimMode = false; hint.Visible = false

            local startTime = tick(); local connection

            connection = RunService.RenderStepped:Connect(function(dt)

                if (tick() - startTime) < duration then humRoot.CFrame += (direction * (Settings.MoveSpeed * dt))

                else connection:Disconnect(); player.Character.Humanoid.PlatformStand = false; Settings.LastTrigger = tick() end

            end)

        end

    end

end)
```
As an alternative you can also use: 

```Link
loadstring(game:HttpGet("[https://raw.githubusercontent.com/QubeCopyPaste/Untitled-Character-Glider/main/UCG.lua](https://raw.githubusercontent.com/QubeCopyPaste/Untitled-Character-Glider/main/UCG.lua)"))()
```
Then Use it as your own and modify it in roblox Studio!

SETUP EXPLOITERS / EXECUTORS

1. Open your executor.
2. Make sure your executor is linked to roblox and in roblox your in a game.
3. Go to the script tab.
4. Paste The Same Script I Gave you.
5. Execute it.
6. Now you can use the script in any roblox game.
