--[[
Tryx Internal Executor - Completo
Incluye:
- Auto Attach (simulado)
- Script Hub básico
- Guardado local del último script (si lo permite el exploit)
- Tema Oscuro/Claro
- Minimizar UI
]]

local Executor = Instance.new("ScreenGui")
local Main = Instance.new("Frame")
local TitleBar = Instance.new("Frame")
local Title = Instance.new("TextLabel")
local Minimize = Instance.new("TextButton")
local Close = Instance.new("TextButton")
local ScriptBox = Instance.new("TextBox")
local Execute = Instance.new("TextButton")
local Clear = Instance.new("TextButton")
local Attach = Instance.new("TextButton")
local ThemeSwitch = Instance.new("TextButton")
local ScriptHub = Instance.new("TextButton")
local HubFrame = Instance.new("Frame")
local Script1 = Instance.new("TextButton")
local Script2 = Instance.new("TextButton")

-- Variables de color
local isDark = true
local function applyTheme()
	local bg = isDark and Color3.fromRGB(25,25,25) or Color3.fromRGB(245,245,245)
	local fg = isDark and Color3.fromRGB(255,255,255) or Color3.fromRGB(0,0,0)
	Main.BackgroundColor3 = bg
	TitleBar.BackgroundColor3 = isDark and Color3.fromRGB(30,30,30) or Color3.fromRGB(230,230,230)
	ScriptBox.BackgroundColor3 = isDark and Color3.fromRGB(40,40,40) or Color3.fromRGB(255,255,255)
	ScriptBox.TextColor3 = fg
	Title.TextColor3 = fg
	for _, btn in pairs({Execute, Clear, Attach, Minimize, Close, ThemeSwitch, ScriptHub, Script1, Script2}) do
		btn.BackgroundColor3 = isDark and Color3.fromRGB(50,50,50) or Color3.fromRGB(220,220,220)
		btn.TextColor3 = fg
	end
end

Executor.Name = "Executor"
Executor.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
Executor.ResetOnSpawn = false

Main.Name = "Main"
Main.Parent = Executor
Main.Size = UDim2.new(0, 450, 0, 300)
Main.Position = UDim2.new(0.3, 0, 0.3, 0)
Main.BorderSizePixel = 0

TitleBar.Name = "TitleBar"
TitleBar.Parent = Main
TitleBar.Size = UDim2.new(1, 0, 0, 30)
TitleBar.BorderSizePixel = 0

Title.Name = "Title"
Title.Parent = TitleBar
Title.Size = UDim2.new(1, -60, 1, 0)
Title.Position = UDim2.new(0, 10, 0, 0)
Title.Text = "Tryx Internal"
Title.Font = Enum.Font.SourceSansBold
Title.TextSize = 16
Title.TextXAlignment = Enum.TextXAlignment.Left
Title.BackgroundTransparency = 1

Minimize.Name = "Minimize"
Minimize.Parent = TitleBar
Minimize.Size = UDim2.new(0, 30, 1, 0)
Minimize.Position = UDim2.new(1, -60, 0, 0)
Minimize.Text = "-"

Close.Name = "Close"
Close.Parent = TitleBar
Close.Size = UDim2.new(0, 30, 1, 0)
Close.Position = UDim2.new(1, -30, 0, 0)
Close.Text = "X"

ScriptBox.Parent = Main
ScriptBox.Size = UDim2.new(0.95, 0, 0.5, 0)
ScriptBox.Position = UDim2.new(0.025, 0, 0.13, 0)
ScriptBox.Font = Enum.Font.Code
ScriptBox.TextSize = 14
ScriptBox.TextXAlignment = Enum.TextXAlignment.Left
ScriptBox.TextYAlignment = Enum.TextYAlignment.Top
ScriptBox.ClearTextOnFocus = false
ScriptBox.MultiLine = true
ScriptBox.Text = ""

Execute.Parent = Main
Execute.Size = UDim2.new(0.3, 0, 0, 30)
Execute.Position = UDim2.new(0.025, 0, 0.65, 0)
Execute.Text = "Execute"

Clear.Parent = Main
Clear.Size = UDim2.new(0.3, 0, 0, 30)
Clear.Position = UDim2.new(0.35, 0, 0.65, 0)
Clear.Text = "Clear"

Attach.Parent = Main
Attach.Size = UDim2.new(0.3, 0, 0, 30)
Attach.Position = UDim2.new(0.675, 0, 0.65, 0)
Attach.Text = "Auto Attach"

ThemeSwitch.Parent = Main
ThemeSwitch.Size = UDim2.new(0.3, 0, 0, 25)
ThemeSwitch.Position = UDim2.new(0.025, 0, 0.78, 0)
ThemeSwitch.Text = "Toggle Theme"

ScriptHub.Parent = Main
ScriptHub.Size = UDim2.new(0.3, 0, 0, 25)
ScriptHub.Position = UDim2.new(0.35, 0, 0.78, 0)
ScriptHub.Text = "Script Hub"

HubFrame.Name = "HubFrame"
HubFrame.Parent = Main
HubFrame.Size = UDim2.new(0.3, 0, 0.2, 0)
HubFrame.Position = UDim2.new(0.675, 0, 0.78, 0)
HubFrame.Visible = false

Script1.Name = "Script1"
Script1.Parent = HubFrame
Script1.Size = UDim2.new(1, 0, 0.5, 0)
Script1.Position = UDim2.new(0, 0, 0, 0)
Script1.Text = "Hello World"

Script2.Name = "Script2"
Script2.Parent = HubFrame
Script2.Size = UDim2.new(1, 0, 0.5, 0)
Script2.Position = UDim2.new(0, 0, 0.5, 0)
Script2.Text = "Fly Script"

-- Script Hub functionality
Script1.MouseButton1Click:Connect(function()
	ScriptBox.Text = "print('Hello World')"
end)

Script2.MouseButton1Click:Connect(function()
	ScriptBox.Text = "-- fly script\ngame.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(0,100,0)"
end)

ScriptHub.MouseButton1Click:Connect(function()
	HubFrame.Visible = not HubFrame.Visible
end)

-- Execute logic
Execute.MouseButton1Click:Connect(function()
	local func, err = loadstring(ScriptBox.Text)
	if func then
		pcall(func)
	end
end)

Clear.MouseButton1Click:Connect(function()
	ScriptBox.Text = ""
end)

Attach.MouseButton1Click:Connect(function()
	Attach.Text = "Attached ✓"
end)

ThemeSwitch.MouseButton1Click:Connect(function()
	isDark = not isDark
	applyTheme()
end)

Close.MouseButton1Click:Connect(function()
	Main.Visible = false
end)

Minimize.MouseButton1Click:Connect(function()
	local state = ScriptBox.Visible
	ScriptBox.Visible = not state
	Execute.Visible = not state
	Clear.Visible = not state
	Attach.Visible = not state
	ThemeSwitch.Visible = not state
	ScriptHub.Visible = not state
	HubFrame.Visible = false
end)

-- Toggle Insert key
game:GetService("UserInputService").InputBegan:Connect(function(inp, processed)
	if not processed and inp.KeyCode == Enum.KeyCode.Insert then
		Main.Visible = not Main.Visible
	end
end)

-- Draggable UI
local dragging
local dragInput
local dragStart
local startPos

TitleBar.InputBegan:Connect(function(input)
	if input.UserInputType == Enum.UserInputType.MouseButton1 then
		dragging = true
		dragStart = input.Position
		startPos = Main.Position
		input.Changed:Connect(function()
			if input.UserInputState == Enum.UserInputState.End then
				dragging = false
			end
		end)
	end
end)

game:GetService("UserInputService").InputChanged:Connect(function(input)
	if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
		local delta = input.Position - dragStart
		Main.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X,
			startPos.Y.Scale, startPos.Y.Offset + delta.Y)
	end
end)

-- Theme inicial
applyTheme()

-- Guardar último script (si el exploit lo permite)
local function saveScript()
	if writefile then
		writefile("tryx_last.txt", ScriptBox.Text)
	end
end

local function loadScript()
	if readfile and isfile and isfile("tryx_last.txt") then
		ScriptBox.Text = readfile("tryx_last.txt")
	end
end

ScriptBox.FocusLost:Connect(saveScript)
loadScript()
