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
local Music = game:GetService("ReplicatedStorage"):WaitForChild("Music")

local Pa = script.Parent

function Button (ThisButton)
	ThisButton.MouseButton1Down:Connect(function()
		Music:FireServer(Pa.ID.Text,ThisButton.Name)
	end)
end

Button(Pa:WaitForChild("Play"))
Button(Pa:WaitForChild("Stop"))
