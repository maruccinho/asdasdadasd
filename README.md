-- LocalScript em StarterPlayerScripts
-- ESP com toggle pelo botão lateral do mouse (ButtonX1)

local UserInputService = game:GetService("UserInputService")
local Players = game:GetService("Players")
local player = Players.LocalPlayer
local espAtivo = false

-- Criar UI de status
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "ESPStatus"
screenGui.ResetOnSpawn = false
screenGui.Parent = player:WaitForChild("PlayerGui")

local statusLabel = Instance.new("TextLabel")
statusLabel.Size = UDim2.new(0, 200, 0, 50)
statusLabel.Position = UDim2.new(0, 10, 0, 10)
statusLabel.BackgroundTransparency = 0.5
statusLabel.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
statusLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
statusLabel.TextScaled = true
statusLabel.Text = "ESP Desativado"
statusLabel.Parent = screenGui

-- Função para criar ESP
local function criarESP(character)
	if character and character:FindFirstChild("HumanoidRootPart") then
		if not character:FindFirstChild("ESP") then
			local highlight = Instance.new("Highlight")
			highlight.Name = "ESP"
			highlight.Adornee = character
			highlight.FillColor = Color3.fromRGB(255, 0, 0)
			highlight.FillTransparency = 0.7
			highlight.OutlineColor = Color3.fromRGB(255, 255, 255)
			highlight.Parent = character
		end
	end
end

-- Função para remover ESP
local function removerESP(character)
	local esp = character:FindFirstChild("ESP")
	if esp then
		esp:Destroy()
	end
end

-- Alternar ESP
local function alternarESP()
	espAtivo = not espAtivo
	statusLabel.Text = espAtivo and "ESP Ativado" or "ESP Desativado"

	for _, plr in pairs(Players:GetPlayers()) do
		if plr ~= player and plr.Character then
			if espAtivo then
				criarESP(plr.Character)
			else
				removerESP(plr.Character)
			end
		end
	end
end

-- Detectar botão lateral do mouse
UserInputService.InputBegan:Connect(function(input, gp)
	if not gp and input.UserInputType == Enum.UserInputType.MouseButton4 then
		alternarESP()
	end
end)

-- Novos jogadores
Players.PlayerAdded:Connect(function(plr)
	plr.CharacterAdded:Connect(function(char)
		if espAtivo then
			criarESP(char)
		end
	end)
end)
