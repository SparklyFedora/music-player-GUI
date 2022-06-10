--created by Sparklyfedorablox lol
local UIS = game:GetService('UserInputService')
local GUIframe = script.Parent
local dragToggle = nil
local dragSpeed = 0
local dragStart = nil
local startPos = nil

local function updateInput(input)
	local delta = input.Position - dragStart
	local position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X,
		startPos.Y.Scale, startPos.Y.Offset + delta.Y)
	game:GetService('TweenService'):Create(GUIframe, TweenInfo.new(dragSpeed), {Position = position}):Play()
end

GUIframe.InputBegan:Connect(function(input)
	if  (input.UserInputType == Enum.UserInputType.Touch) then 
		dragToggle = true
		dragStart = input.Position
		startPos = GUIframe.Position
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
local Music = game:GetService("ReplicatedStorage"):WaitForChild("Music")

local Pa = script.Parent

function Button (ThisButton)
	ThisButton.MouseButton1Down:Connect(function()
		Music:FireServer(Pa.ID.Text,ThisButton.Name)
	end)
end

Button(Pa:WaitForChild("Play"))
Button(Pa:WaitForChild("Stop"))
