-- // HOOK SPEED BYPASS — LEAKED BY WEEKLY //

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local CoreGui = game:GetService("CoreGui")

local lp = Players.LocalPlayer
local activated = false
local keybind = Enum.KeyCode.E
local waitingForKey = false
local power = 97000
local lagAmount = 0.12
local lagConn = nil

local function applyPower(val)
	power = math.clamp(val, 10000, 300000)
	local t = (power - 10000) / 290000
	lagAmount = t * 0.2
end
applyPower(power)

local function startLag()
	if lagConn then lagConn:Disconnect() end
	lagConn = RunService.RenderStepped:Connect(function()
		if not activated then return end
		if lagAmount > 0 then
			local t = tick()
			while tick() - t < lagAmount do end
		end
	end)
end

local function stopLag()
	activated = false
	if lagConn then lagConn:Disconnect(); lagConn = nil end
end

if CoreGui:FindFirstChild("K7_Ultimate_Bypass") then
	CoreGui.K7_Ultimate_Bypass:Destroy()
end

local gui = Instance.new("ScreenGui")
gui.Name = "K7_Ultimate_Bypass"
gui.ResetOnSpawn = false
gui.Parent = CoreGui

local main = Instance.new("Frame")
main.Size = UDim2.new(0, 200, 0, 200)
main.Position = UDim2.new(0.5, -100, 0.5, -100)
main.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
main.BorderSizePixel = 0
main.Active = true
main.Draggable = true
main.Parent = gui

local mainStroke = Instance.new("UIStroke")
mainStroke.Thickness = 2
mainStroke.Color = Color3.fromRGB(148, 0, 211)
mainStroke.Parent = main
Instance.new("UICorner", main).CornerRadius = UDim.new(0, 8)

local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, 0, 0, 25)
title.Position = UDim2.new(0, 0, 0, 5)
title.BackgroundTransparency = 1
title.Text = "Hook Speed Bypass"
title.TextColor3 = Color3.fromRGB(255, 255, 255)
title.Font = Enum.Font.GothamBold
title.TextSize = 14
title.Parent = main

local statusFrame = Instance.new("TextButton")
statusFrame.Size = UDim2.new(0.85, 0, 0, 30)
statusFrame.Position = UDim2.new(0.075, 0, 0, 35)
statusFrame.BackgroundColor3 = Color3.fromRGB(25, 25, 25)
statusFrame.AutoButtonColor = false
statusFrame.Parent = main
Instance.new("UICorner", statusFrame).CornerRadius = UDim.new(0, 6)

local statusText = Instance.new("TextLabel")
statusText.Size = UDim2.new(1, 0, 1, 0)
statusText.BackgroundTransparency = 1
statusText.Text = "STATUS: DISABLED"
statusText.TextColor3 = Color3.fromRGB(180, 80, 255)
statusText.Font = Enum.Font.GothamBold
statusText.TextSize = 12
statusText.Parent = statusFrame

local function toggle()
	if not activated then
		activated = true
		statusText.Text = "STATUS: ENABLED"
		statusText.TextColor3 = Color3.fromRGB(148, 0, 211)
		startLag()
	else
		stopLag()
		statusText.Text = "STATUS: DISABLED"
		statusText.TextColor3 = Color3.fromRGB(180, 80, 255)
	end
end
statusFrame.MouseButton1Click:Connect(toggle)

local kbLabel = Instance.new("TextLabel")
kbLabel.Size = UDim2.new(0, 0, 0, 20)
kbLabel.Position = UDim2.new(0.08, 0, 0, 75)
kbLabel.BackgroundTransparency = 1
kbLabel.Text = "Keybind:"
kbLabel.TextColor3 = Color3.fromRGB(180, 180, 180)
kbLabel.Font = Enum.Font.GothamMedium
kbLabel.TextSize = 10
kbLabel.TextXAlignment = Enum.TextXAlignment.Left
kbLabel.Parent = main

local kbBtn = Instance.new("TextButton")
kbBtn.Size = UDim2.new(0, 60, 0, 25)
kbBtn.Position = UDim2.new(0.6, 0, 0, 72)
kbBtn.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
kbBtn.Text = "E"
kbBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
kbBtn.Font = Enum.Font.GothamBold
kbBtn.TextSize = 12
kbBtn.BorderSizePixel = 0
kbBtn.AutoButtonColor = false
kbBtn.Parent = main
Instance.new("UICorner", kbBtn).CornerRadius = UDim.new(0, 6)

kbBtn.MouseButton1Click:Connect(function()
	waitingForKey = true
	kbBtn.Text = "..."
	kbBtn.TextColor3 = Color3.fromRGB(255, 100, 100)
end)

local modeLabel = Instance.new("TextLabel")
modeLabel.Size = UDim2.new(0, 0, 0, 20)
modeLabel.Position = UDim2.new(0.08, 0, 0, 105)
modeLabel.BackgroundTransparency = 1
modeLabel.Text = "Mode:"
modeLabel.TextColor3 = Color3.fromRGB(180, 180, 180)
modeLabel.Font = Enum.Font.GothamMedium
modeLabel.TextSize = 10
modeLabel.TextXAlignment = Enum.TextXAlignment.Left
modeLabel.Parent = main

local modeBtn = Instance.new("TextButton")
modeBtn.Size = UDim2.new(0, 60, 0, 25)
modeBtn.Position = UDim2.new(0.6, 0, 0, 102)
modeBtn.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
modeBtn.Text = "V1"
modeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
modeBtn.Font = Enum.Font.GothamBold
modeBtn.TextSize = 12
modeBtn.BorderSizePixel = 0
modeBtn.Parent = main
Instance.new("UICorner", modeBtn).CornerRadius = UDim.new(0, 6)

local powerLabel = Instance.new("TextLabel")
powerLabel.Size = UDim2.new(0.8, 0, 0, 15)
powerLabel.Position = UDim2.new(0.1, 0, 0, 135)
powerLabel.BackgroundTransparency = 1
powerLabel.Text = "Power: 97000"
powerLabel.TextColor3 = Color3.fromRGB(200, 200, 200)
powerLabel.Font = Enum.Font.GothamMedium
powerLabel.TextSize = 10
powerLabel.TextXAlignment = Enum.TextXAlignment.Left
powerLabel.Parent = main

local sliderFrame = Instance.new("Frame")
sliderFrame.Size = UDim2.new(0.8, 0, 0, 3)
sliderFrame.Position = UDim2.new(0.1, 0, 0, 155)
sliderFrame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
sliderFrame.BorderSizePixel = 0
sliderFrame.Parent = main
Instance.new("UICorner", sliderFrame).CornerRadius = UDim.new(1, 0)

local startPercent = (97000 - 10000) / 290000
local sliderFill = Instance.new("Frame")
sliderFill.Size = UDim2.new(startPercent, 0, 1, 0)
sliderFill.BackgroundColor3 = Color3.fromRGB(148, 0, 211)
sliderFill.BorderSizePixel = 0
sliderFill.Parent = sliderFrame
Instance.new("UICorner", sliderFill).CornerRadius = UDim.new(1, 0)

local sliderKnob = Instance.new("Frame")
sliderKnob.Size = UDim2.new(0, 14, 0, 14)
sliderKnob.Position = UDim2.new(startPercent, -7, 0.5, -7)
sliderKnob.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
sliderKnob.BorderSizePixel = 0
sliderKnob.Parent = sliderFrame
Instance.new("UICorner", sliderKnob).CornerRadius = UDim.new(1, 0)

local powerBox = Instance.new("TextBox")
powerBox.Size = UDim2.new(0.8, 0, 0, 25)
powerBox.Position = UDim2.new(0.1, 0, 0, 162)
powerBox.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
powerBox.TextColor3 = Color3.fromRGB(255, 255, 255)
powerBox.Font = Enum.Font.GothamBold
powerBox.TextSize = 12
powerBox.Text = "97000"
powerBox.BorderSizePixel = 0
powerBox.ClearTextOnFocus = false
powerBox.Parent = main
Instance.new("UICorner", powerBox).CornerRadius = UDim.new(0, 6)

local dragging = false
sliderKnob.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		dragging = true
	end
end)

UserInputService.InputEnded:Connect(function(input, gpe)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		dragging = false
	end
end)

local function updateUIFromPower(newPower)
	applyPower(newPower)
	local percent = (newPower - 10000) / 290000
	sliderFill.Size = UDim2.new(percent, 0, 1, 0)
	sliderKnob.Position = UDim2.new(percent, -7, 0.5, -7)
	powerLabel.Text = "Power: " .. tostring(newPower)
	powerBox.Text = tostring(newPower)
end

local function updateSlider(xPos)
	local frameWidth = sliderFrame.AbsoluteSize.X
	local clampedPos = math.clamp(xPos - sliderFrame.AbsolutePosition.X, 0, frameWidth)
	local percent = clampedPos / frameWidth
	local newPower = math.floor(10000 + (percent * 290000))
	updateUIFromPower(newPower)
end

sliderFrame.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		updateSlider(input.Position.X)
	end
end)

UserInputService.InputChanged:Connect(function(input, gpe)
	if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
		updateSlider(input.Position.X)
	end
end)

-- FIXED: Proper Lua comment
powerBox.FocusLost:Connect(function()
	local val = tonumber(powerBox.Text)
	if val then
		val = math.clamp(val, 10000, 300000)
		updateUIFromPower(val)
	else
		powerBox.Text = tostring(power)
	end
end)

UserInputService.InputBegan:Connect(function(input, gpe)
	if gpe then return end
	if waitingForKey then
		if input.UserInputType == Enum.UserInputType.Keyboard then
			keybind = input.KeyCode
			kbBtn.Text = keybind.Name
			kbBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
			waitingForKey = false
		end
		return
	end
	if input.KeyCode == keybind then
		toggle()
	end
end)

lp.CharacterAdded:Connect(function()
	task.wait(1)
	if activated then
		stopLag()
		activated = true
		startLag()
	end
end)
