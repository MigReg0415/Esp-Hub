local Players = game:GetService("Players")
local Workspace = game:GetService("Workspace")

local LocalPlayer = Players.LocalPlayer
local Character = LocalPlayer.Character

local function createESP(object, color)
  local esp = Instance.new("BillboardGui")
  esp.Size = UDim2.new(0, 100, 0, 20)
  esp.Adornee = object
  esp.Parent = object

  local textLabel = Instance.new("TextLabel")
  textLabel.Size = UDim2.new(1, 0, 1, 0)
  textLabel.BackgroundTransparency = 1
  textLabel.TextColor3 = color
  textLabel.Text = object.Name
  textLabel.Parent = esp

  return esp
end

local function updateESP()
  for _, player in pairs(Players:GetPlayers()) do
    if player ~= LocalPlayer and player.Character then
      local esp = player.Character:FindFirstChild("BillboardGui")
      if not esp then
        createESP(player.Character.HumanoidRootPart, Color3.new(0, 1, 0)) -- Verde para jogadores
      end
    end
  end

  for _, fruit in pairs(Workspace:GetDescendants()) do
    if fruit:IsA("Part") and fruit.Name:find("Fruit") then
      local esp = fruit:FindFirstChild("BillboardGui")
      if not esp then
        createESP(fruit, Color3.new(1, 0, 0)) -- Vermelho para frutas
      end
    end
  end
end
