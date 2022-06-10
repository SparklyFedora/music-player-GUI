-- Gui to Lua
-- Version: 3.2

-- Instances:

local ScreenGui = Instance.new("ScreenGui")
local GUIFrame = Instance.new("Frame")
local ID = Instance.new("TextBox")
local GUILabel = Instance.new("TextLabel")
local Play = Instance.new("TextButton")
local Stop = Instance.new("TextButton")

--Properties:

ScreenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

GUIFrame.Name = "GUIFrame"
GUIFrame.Parent = ScreenGui
GUIFrame.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
GUIFrame.Position = UDim2.new(0.708460748, 0, 0.349887133, 0)
GUIFrame.Size = UDim2.new(0, 286, 0, 133)
GUIFrame.Style = Enum.FrameStyle.RobloxRound

ID.Name = "ID"
ID.Parent = GUIFrame
ID.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
ID.Position = UDim2.new(0.12937063, 0, 0.0601503775, 0)
ID.Size = UDim2.new(0, 200, 0, 50)
ID.Font = Enum.Font.RobotoCondensed
ID.PlaceholderText = "Enter Music Id Here"
ID.Text = ""
ID.TextColor3 = Color3.fromRGB(0, 0, 0)
ID.TextSize = 14.000

GUILabel.Name = "GUILabel"
GUILabel.Parent = GUIFrame
GUILabel.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
GUILabel.Position = UDim2.new(-0.031468533, 0, -0.345864654, 0)
GUILabel.Size = UDim2.new(0, 286, 0, 32)
GUILabel.Font = Enum.Font.SourceSans
GUILabel.Text = "Music Player GUI"
GUILabel.TextColor3 = Color3.fromRGB(0, 0, 0)
GUILabel.TextSize = 14.000

Play.Name = "Play"
Play.Parent = GUIFrame
Play.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Play.Position = UDim2.new(0.0244755242, 0, 0.60150373, 0)
Play.Size = UDim2.new(0, 103, 0, 41)
Play.Style = Enum.ButtonStyle.RobloxRoundButton
Play.Font = Enum.Font.RobotoCondensed
Play.Text = "Play"
Play.TextColor3 = Color3.fromRGB(0, 0, 0)
Play.TextSize = 14.000

Stop.Name = "Stop"
Stop.Parent = GUIFrame
Stop.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
Stop.Position = UDim2.new(0.486013979, 0, 0.60150373, 0)
Stop.Size = UDim2.new(0, 114, 0, 41)
Stop.Style = Enum.ButtonStyle.RobloxRoundButton
Stop.Font = Enum.Font.SourceSans
Stop.Text = "Stop"
Stop.TextColor3 = Color3.fromRGB(0, 0, 0)
Stop.TextSize = 14.000

-- Scripts:

local function QCUT_fake_script() -- GUIFrame.LocalScript 
	local script = Instance.new('LocalScript', GUIFrame)

	local Music = game:GetService("ReplicatedStorage"):WaitForChild("Music")
	
	local Pa = script.Parent
	
	function Button (ThisButton)
		ThisButton.MouseButton1Down:Connect(function()
			Music:FireServer(Pa.ID.Text,ThisButton.Name)
		end)
	end
	
	Button(Pa:WaitForChild("Play"))
	Button(Pa:WaitForChild("Stop"))
	
end
coroutine.wrap(QCUT_fake_script)()
local function JBBOUWC_fake_script() -- GUIFrame.LocalScript 
	local script = Instance.new('LocalScript', GUIFrame)

	local UIS = game:GetService('UserInputService')
	local frame = script.Parent
	local dragToggle = nil
	local dragSpeed = 0
	local dragStart = nil
	local startPos = nil
	
	local function updateInput(input)
		local delta = input.Position - dragStart
		local position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X,
			startPos.Y.Scale, startPos.Y.Offset + delta.Y)
		game:GetService('TweenService'):Create(frame, TweenInfo.new(dragSpeed), {Position = position}):Play()
	end
	
	frame.InputBegan:Connect(function(input)
		if (input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch) then 
			dragToggle = true
			dragStart = input.Position
			startPos = frame.Position
			input.Changed:Connect(function()
				if input.UserInputState == Enum.UserInputState.End then
					dragToggle = false
				end
			end)
		end
	end)
	
	UIS.InputChanged:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
			if dragToggle then
				updateInput(input)
			end
		end
	end)
	
end
coroutine.wrap(JBBOUWC_fake_script)()
