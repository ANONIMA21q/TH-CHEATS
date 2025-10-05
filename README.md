local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local player = Players.LocalPlayer
local playerGui = player:FindFirstChildOfClass("PlayerGui") or player:WaitForChild("PlayerGui")

-- Limpar GUI antiga caso exista
local existingGui = playerGui:FindFirstChild("FishCatcherGui")
if existingGui then
    existingGui:Destroy()
end

-- Criar ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "FishCatcherGui"
screenGui.Parent = playerGui
screenGui.ResetOnSpawn = false

-- Frame principal
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 360, 0, 400)
frame.Position = UDim2.new(0.5, -180, 0.5, -200)
frame.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
frame.BorderSizePixel = 0
frame.AnchorPoint = Vector2.new(0.5, 0.5)
frame.Parent = screenGui

local frameCorner = Instance.new("UICorner")
frameCorner.CornerRadius = UDim.new(0, 16)
frameCorner.Parent = frame

-- Título (área para mover o painel)
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, -20, 0, 40)
title.Position = UDim2.new(0, 10, 0, 10)
title.BackgroundTransparency = 1
title.Text = "🎣 TH CHEATS - Fish Catcher"
title.TextColor3 = Color3.new(1, 1, 1)
title.Font = Enum.Font.FredokaOne
title.TextSize = 24
title.TextXAlignment = Enum.TextXAlignment.Center
title.Parent = frame

-- Função para arrastar o painel (apenas clicando no título)
local dragging = false
local dragInput, dragStart, startPos

local function update(input)
    local delta = input.Position - dragStart
    frame.Position = UDim2.new(
        startPos.X.Scale,
        startPos.X.Offset + delta.X,
        startPos.Y.Scale,
        startPos.Y.Offset + delta.Y
    )
end

title.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 then
        dragging = true
        dragStart = input.Position
        startPos = frame.Position

        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

title.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement then
        dragInput = input
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if dragging and input == dragInput then
        update(input)
    end
end)

-- Barra de pesquisa
local searchBox = Instance.new("TextBox")
searchBox.Size = UDim2.new(1, -20, 0, 30)
searchBox.Position = UDim2.new(0, 10, 0, 60)
searchBox.PlaceholderText = "🔍 Pesquise o nome do peixe"
searchBox.Text = ""
searchBox.ClearTextOnFocus = false
searchBox.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
searchBox.TextColor3 = Color3.new(1, 1, 1)
searchBox.Font = Enum.Font.SourceSans
searchBox.TextSize = 18
searchBox.Parent = frame

local searchCorner = Instance.new("UICorner")
searchCorner.CornerRadius = UDim.new(0, 6)
searchCorner.Parent = searchBox

-- Dropdown de peixes
local listFrame = Instance.new("ScrollingFrame")
listFrame.Size = UDim2.new(1, -20, 0, 180)
listFrame.Position = UDim2.new(0, 10, 0, 100)
listFrame.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
listFrame.BorderSizePixel = 0
listFrame.CanvasSize = UDim2.new(0, 0, 0, 0)
listFrame.ScrollBarThickness = 8
listFrame.Parent = frame

local listCorner = Instance.new("UICorner")
listCorner.CornerRadius = UDim.new(0, 8)
listCorner.Parent = listFrame

local listLayout = Instance.new("UIListLayout")
listLayout.SortOrder = Enum.SortOrder.LayoutOrder
listLayout.Padding = UDim.new(0, 4)
listLayout.Parent = listFrame

-- Botão para capturar peixe
local getButton = Instance.new("TextButton")
getButton.Size = UDim2.new(1, -20, 0, 40)
getButton.Position = UDim2.new(0, 10, 1, -50)
getButton.BackgroundColor3 = Color3.fromRGB(85, 0, 255)
getButton.TextColor3 = Color3.new(1, 1, 1)
getButton.Font = Enum.Font.FredokaOne
getButton.TextSize = 20
getButton.Text = "✅ Pegar Peixe"
getButton.Parent = frame

local btnCorner = Instance.new("UICorner")
btnCorner.CornerRadius = UDim.new(0, 12)
btnCorner.Parent = getButton

getButton.MouseEnter:Connect(function()
    getButton.BackgroundColor3 = Color3.fromRGB(120, 0, 255)
end)

getButton.MouseLeave:Connect(function()
    getButton.BackgroundColor3 = Color3.fromRGB(85, 0, 255)
end)

-- Variáveis para carregar peixes
local fishFolder = ReplicatedStorage:WaitForChild("A__Assets"):WaitForChild("Fish")
local addToInventoryRF = ReplicatedStorage:WaitForChild("Packages")
    :WaitForChild("_Index")
    :WaitForChild("sleitnick_knit@1.7.0")
    :WaitForChild("knit")
    :WaitForChild("Services")
    :WaitForChild("FishService")
    :WaitForChild("RF")
    :WaitForChild("AddToInventory")

local fishButtons = {}
local selectedFish = nil

-- Carregar peixes na lista com ícones
for _, fish in ipairs(fishFolder:GetChildren()) do
    local fishButton = Instance.new("TextButton")
    fishButton.Size = UDim2.new(1, -10, 0, 40)
    fishButton.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
    fishButton.TextColor3 = Color3.new(1, 1, 1)
    fishButton.Font = Enum.Font.SourceSans
    fishButton.TextSize = 18
    fishButton.Text = "🐟 " .. fish.Name
    fishButton.Parent = listFrame

    local buttonCorner = Instance.new("UICorner")
    buttonCorner.CornerRadius = UDim.new(0, 6)
    buttonCorner.Parent = fishButton

    fishButton.MouseEnter:Connect(function()
        fishButton.BackgroundColor3 = Color3.fromRGB(80, 80, 80)
    end)

    fishButton.MouseLeave:Connect(function()
        fishButton.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
    end)

    fishButton.MouseButton1Click:Connect(function()
        selectedFish = fish.Name
        print("Peixe selecionado: " .. fish.Name)
    end)

    table.insert(fishButtons, fishButton)
end

-- Função de pesquisa
searchBox:GetPropertyChangedSignal("Text"):Connect(function()
    local searchQuery = searchBox.Text:lower()

    for _, button in ipairs(fishButtons) do
        if string.find(button.Text:lower(), searchQuery) then
            button.Visible = true
        else
            button.Visible = false
        end
    end

    listFrame.CanvasSize = UDim2.new(0, 0, 0, listLayout.AbsoluteContentSize.Y)
end)

listLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
    listFrame.CanvasSize = UDim2.new(0, 0, 0, listLayout.AbsoluteContentSize.Y)
end)

-- Lógica do botão "Pegar Peixe"
getButton.MouseButton1Click:Connect(function()
    if selectedFish then
        local args = {selectedFish, "Catch"}
        local success, err = pcall(function()
            return addToInventoryRF:InvokeServer(unpack(args))
        end)

        if success then
            print("[TH CHEATS] Peixe capturado com sucesso: " .. selectedFish)
        else
            warn("[TH CHEATS] Erro ao capturar o peixe: " .. err)
        end
    else
        warn("[TH CHEATS] Nenhum peixe selecionado!")
    end
end)

-- Alternar visibilidade com tecla Insert
UserInputService.InputBegan:Connect(function(input, isProcessed)
    if not isProcessed and input.KeyCode == Enum.KeyCode.Insert then
        screenGui.Enabled = not screenGui.Enabled
    end
end)

print("[TH CHEATS] Painel iniciado com funcionalidade de arrastar apenas pelo título!")
