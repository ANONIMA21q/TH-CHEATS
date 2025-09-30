
-- Title label
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, -20, 0, 40)
title.Position = UDim2.new(0, 10, 0, 10)
title.BackgroundTransparency = 1
title.Text = "TH CHEATS"
title.TextColor3 = Color3.new(1, 1, 1)
title.Font = Enum.Font.SourceSansBold
title.TextSize = 28
title.TextXAlignment = Enum.TextXAlignment.Left
title.Parent = frame
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local player = Players.LocalPlayer
local playerGui = player:FindFirstChildOfClass("PlayerGui") or player:WaitForChild("PlayerGui")

-- Clean old GUI if exists
local existingGui = playerGui:FindFirstChild("FishCatcherGui")
if existingGui then
    existingGui:Destroy()
end

local fishFolder = ReplicatedStorage:WaitForChild("A__Assets"):WaitForChild("Fish")
local addToInventoryRF = ReplicatedStorage:WaitForChild("Packages")
    :WaitForChild("_Index")
    :WaitForChild("sleitnick_knit@1.7.0")
    :WaitForChild("knit")
    :WaitForChild("Services")
    :WaitForChild("FishService")
    :WaitForChild("RF")
    :WaitForChild("AddToInventory")

-- Create ScreenGui
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "FishCatcherGui"
screenGui.Parent = playerGui
screenGui.ResetOnSpawn = false

-- Frame principal
local frame = Instance.new("Frame")
frame.Size = UDim2.new(0, 360, 0, 300)
frame.Position = UDim2.new(0.5, -180, 0.4, -150)
frame.BackgroundTransparency = 1
frame.BorderSizePixel = 0
frame.AnchorPoint = Vector2.new(0, 0)
frame.ZIndex = 10
frame.Parent = screenGui

local frameCorner = Instance.new("UICorner")
frameCorner.CornerRadius = UDim.new(0, 16)
frameCorner.Parent = frame

local frameCorner = Instance.new("UICorner")
frameCorner.CornerRadius = UDim.new(0, 12)
frameCorner.Parent = frame

-- Imagem de fundo
local background = Instance.new("ImageLabel")
background.Size = UDim2.new(1, 0, 1, 0)
background.BackgroundTransparency = 1
background.Image = "rbxassetid://[SEU_ID_AQUI]" -- Coloque seu ID
background.ScaleType = Enum.ScaleType.Crop
background.ZIndex = 9
background.Parent = frame

-- Painel roxo semi-transparente
local panel = Instance.new("Frame")
panel.Size = UDim2.new(1, 0, 1, 0)
panel.Position = UDim2.new(0, 0, 0, 0)
panel.BackgroundColor3 = Color3.fromRGB(95, 45, 145)
panel.BackgroundTransparency = 0.3
panel.ZIndex = 10
panel.Parent = frame

local panelCorner = Instance.new("UICorner")
panelCorner.CornerRadius = UDim.new(0, 16)
panelCorner.Parent = panel

-- Dragging
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

panel.InputBegan:Connect(function(input)
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

panel.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement then
        dragInput = input
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if dragging and input == dragInput then
        update(input)
    end
end)

-- Título
local title = Instance.new("TextLabel")
title.Size = UDim2.new(1, -20, 0, 40)
title.Position = UDim2.new(0, 10, 0, 10)
title.BackgroundTransparency = 1
title.Text = "TH CHEATS"
title.TextColor3 = Color3.new(1, 1, 1)
title.Font = Enum.Font.LuckiestGuy
title.TextSize = 28
title.TextXAlignment = Enum.TextXAlignment.Left
title.ZIndex = 11
title.Parent = panel

-- Select Fish Label
local selectLabel = Instance.new("TextLabel")
selectLabel.Size = UDim2.new(1, -20, 0, 25)
selectLabel.Position = UDim2.new(0, 10, 0, 60)
selectLabel.BackgroundTransparency = 1
selectLabel.Text = "Menu Peixe:"
selectLabel.TextColor3 = Color3.new(1, 1, 1)
selectLabel.Font = Enum.Font.Arcade
selectLabel.TextSize = 19
selectLabel.TextXAlignment = Enum.TextXAlignment.Left
selectLabel.Parent = frame

-- Dropdown button
local dropdownButton = Instance.new("TextButton")
dropdownButton.Size = UDim2.new(1, -20, 0, 30)
dropdownButton.Position = UDim2.new(0, 10, 0, 90)
dropdownButton.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
dropdownButton.TextColor3 = Color3.new(1, 1, 1)
dropdownButton.Font = Enum.Font.SourceSans
dropdownButton.TextSize = 20
dropdownButton.Text = "Selecine o peixe!"
dropdownButton.AutoButtonColor = true
dropdownButton.Parent = frame
dropdownButton.ZIndex = 90

-- Botão Executar Infinity Eald
local infinityButton = Instance.new("TextButton")
infinityButton.Size = UDim2.new(1, -20, 0, 40)
infinityButton.Position = UDim2.new(0, 10, 0, 170) -- Ajuste a posição conforme necessário
infinityButton.BackgroundColor3 = Color3.fromRGB(85, 0, 255)
infinityButton.TextColor3 = Color3.new(1, 1, 1)
infinityButton.Font = Enum.Font.SourceSansBold
infinityButton.TextSize = 20
infinityButton.Text = "Executar Infinity Eald"
infinityButton.AutoButtonColor = true
infinityButton.ZIndex = 11
infinityButton.Parent = panel

local infinityBtnCorner = Instance.new("UICorner")
infinityBtnCorner.CornerRadius = UDim.new(0, 10)
infinityBtnCorner.Parent = infinityButton

infinityButton.MouseEnter:Connect(function()
    infinityButton.BackgroundColor3 = Color3.fromRGB(120, 0, 255)
end)
infinityButton.MouseLeave:Connect(function()
    infinityButton.BackgroundColor3 = Color3.fromRGB(85, 0, 255)
end)

-- Evento para executar o script do Infinity Eald
infinityButton.MouseButton1Click:Connect(function()
    -- Coloque aqui o código do Infinity Eald
    loadstring(game:HttpGet('https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source'))()
end)

-- Serviços
local UserInputService = game:GetService("UserInputService")

-- Função para alternar visibilidade com Insert
UserInputService.InputBegan:Connect(function(input, isProcessed)
    if not isProcessed then
        if input.KeyCode == Enum.KeyCode.Insert then
            screenGui.Enabled = not screenGui.Enabled
        end
    end
end)

-- Search bar
local searchBox = Instance.new("TextBox")
searchBox.Size = UDim2.new(1, -20, 0, 28)
searchBox.Position = UDim2.new(0, 10, 0, 130)
searchBox.PlaceholderText = "Pesquise o neme do peixe!"
searchBox.Text = ""
searchBox.ClearTextOnFocus = false
searchBox.BackgroundColor3 = Color3.fromRGB(80, 80, 80)
searchBox.TextColor3 = Color3.new(1, 1, 1)
searchBox.Font = Enum.Font.SourceSans
searchBox.TextSize = 18
searchBox.Parent = frame
searchBox.ZIndex = 12

local searchCorner = Instance.new("UICorner")
searchCorner.CornerRadius = UDim.new(0, 6)
searchCorner.Parent = searchBox

-- Dropdown frame and layout
local listFrame = Instance.new("ScrollingFrame")
listFrame.Size = UDim2.new(1, -20, 0, 100)
listFrame.BackgroundColor3 = Color3.fromRGB(60, 60, 60)
listFrame.BorderSizePixel = 0
listFrame.Position = UDim2.new(0, 10, 0, 165)
listFrame.Visible = false
listFrame.CanvasSize = UDim2.new(0, 0, 0, 0)
listFrame.ScrollBarThickness = 8
listFrame.Parent = frame
listFrame.ZIndex = 11

local listCorner = Instance.new("UICorner")
listCorner.CornerRadius = UDim.new(0, 8)
listCorner.Parent = listFrame

local UIListLayout = Instance.new("UIListLayout")
UIListLayout.SortOrder = Enum.SortOrder.LayoutOrder
UIListLayout.Padding = UDim.new(0, 4)
UIListLayout.Parent = listFrame

-- Get all fish names
local fishNames = {}
for _, fish in ipairs(fishFolder:GetChildren()) do
    table.insert(fishNames, fish.Name)
end

local selectedFishName = nil

-- Functions to open/close dropdown
local function closeDropdown()
    listFrame.Visible = false
end

local function openDropdown()
    listFrame.Visible = true
    local screenHeight = playerGui.AbsoluteSize.Y
    local dropdownAbsoluteY = dropdownButton.AbsolutePosition.Y
    local dropdownHeight = dropdownButton.AbsoluteSize.Y
    local listHeight = listFrame.AbsoluteSize.Y > 0 and listFrame.AbsoluteSize.Y or 100
    local spaceBelow = screenHeight - (dropdownAbsoluteY + dropdownHeight)
    if spaceBelow < listHeight then
        listFrame.Position = UDim2.new(0, 10, 0, dropdownButton.Position.Y.Offset - listHeight - 6)
    else
        listFrame.Position = UDim2.new(0, 10, 0, dropdownButton.Position.Y.Offset + dropdownHeight + 6)
    end
end

-- Populate fish list buttons
local fishButtons = {}
for i, fishName in ipairs(fishNames) do
    local fishBtn = Instance.new("TextButton")
    fishBtn.Size = UDim2.new(1, -10, 0, 28)
    fishBtn.BackgroundColor3 = Color3.fromRGB(90, 90, 90)
    fishBtn.TextColor3 = Color3.new(1, 1, 1)
    fishBtn.Font = Enum.Font.SourceSans
    fishBtn.TextSize = 18
    fishBtn.Text = fishName
    fishBtn.LayoutOrder = i
    fishBtn.AutoButtonColor = true
    fishBtn.Parent = listFrame
    fishBtn.ZIndex = 12

    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0, 6)
    corner.Parent = fishBtn

    fishBtn.MouseEnter:Connect(function()
        fishBtn.BackgroundColor3 = Color3.fromRGB(115, 115, 115)
    end)
    fishBtn.MouseLeave:Connect(function()
        fishBtn.BackgroundColor3 = Color3.fromRGB(90, 90, 90)
    end)

    fishBtn.MouseButton1Click:Connect(function()
        selectedFishName = fishName
        dropdownButton.Text = fishName
        closeDropdown()
    end)

    table.insert(fishButtons, fishBtn)
end

-- Filter function for search box
local function filterFish(query)
    query = query:lower()
    for _, btn in ipairs(fishButtons) do
        if string.find(btn.Text:lower(), query) then
            btn.Visible = true
        else
            btn.Visible = false
        end
    end
end

searchBox:GetPropertyChangedSignal("Text"):Connect(function()
    filterFish(searchBox.Text)
end)

UIListLayout:GetPropertyChangedSignal("AbsoluteContentSize"):Connect(function()
    listFrame.CanvasSize = UDim2.new(0, 0, 0, UIListLayout.AbsoluteContentSize.Y + 8)
end)

dropdownButton.MouseButton1Click:Connect(function()
    if listFrame.Visible then
        closeDropdown()
    else
        openDropdown()
    end
end)

-- Botão Get Fish
local getButton = Instance.new("TextButton")
getButton.Size = UDim2.new(1, -20, 0, 40)
getButton.Position = UDim2.new(0, 10, 1, -50)
getButton.BackgroundColor3 = Color3.fromRGB(85, 0, 255)
getButton.TextColor3 = Color3.new(1, 1, 1)
getButton.Font = Enum.Font.SourceSansBold
getButton.TextSize = 26
getButton.Text = "Pegar o Peixe"
getButton.AutoButtonColor = true
getButton.ZIndex = 11
getButton.Parent = panel

local btnCorner = Instance.new("UICorner")
btnCorner.CornerRadius = UDim.new(0, 10)
btnCorner.Parent = getButton

getButton.MouseEnter:Connect(function() getButton.BackgroundColor3 = Color3.fromRGB(120, 0, 255) end)
getButton.MouseLeave:Connect(function() getButton.BackgroundColor3 = Color3.fromRGB(85, 0, 255) end)

getButton.MouseButton1Click:Connect(function()
    if not selectedFishName then
        warn("[TH CHEATS] Please select a fish first!")
        return
    end
    local args = {selectedFishName, "Catch"}
    local success, err = pcall(function()
        return addToInventoryRF:InvokeServer(unpack(args))
    end)
    if success then
        print("[TH CHEATS] Successfully added fish:", selectedFishName)
    else
        warn("[TH CHEATS] Failed to add fish:", err)
    end
end)
