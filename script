-- LocalScript em StarterPlayerScripts
-- ESP com botão na interface (UI)

local Players = game:GetService("Players")
local player = Players.LocalPlayer
local espAtivo = false

-- Criar GUI
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "ESPGui"
screenGui.ResetOnSpawn = false
screenGui.Parent = player:WaitForChild("PlayerGui")

-- Criar botão
local toggleButton = Instance.new("TextButton")
toggleButton.Size = UDim2.new(0, 150, 0, 50)
toggleButton.Position = UDim2.new(0, 10, 0, 10)
toggleButton.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
toggleButton.TextColor3 = Color3.fromRGB(255, 255, 255)
toggleButton.TextScaled = true
toggleButton.Text = "Ativar ESP"
toggleButton.Parent = screenGui

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
	toggleButton.Text = espAtivo and "Desativar ESP" or "Ativar ESP"

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

-- Ação do botão
toggleButton.MouseButton1Click:Connect(function()
	alternarESP()
end)

-- Novos jogadores
Players.PlayerAdded:Connect(function
