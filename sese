local Players = game:GetService("Players")
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local StarterPack = game:GetService("StarterPack")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local TextService = game:GetService("TextService")
local Camera = workspace.CurrentCamera
local Player = Players.LocalPlayer

print("✅ AUTORIZACIÓN CON ÉXITO: " .. Player.Name .. " - BOLTAGUE AIMBOT CARGADO!")

-- === INTERFACE - NUEVO DISEÑO ESTÉTICO ===
local ScreenGui = Instance.new("ScreenGui", game.CoreGui)
ScreenGui.Name = "Boltague_Aimbot_Menu"
ScreenGui.IgnoreGuiInset = true
ScreenGui.ResetOnSpawn = false

-- Contenedor principal con estilo
local MainFrame = Instance.new("Frame", ScreenGui)
MainFrame.Size = UDim2.new(0.35, 0, 0.70, 0)
MainFrame.Position = UDim2.new(0.325, 0, 0.15, 0)
MainFrame.BackgroundColor3 = Color3.fromRGB(12, 12, 18)
MainFrame.BorderSizePixel = 0
MainFrame.Visible = true
MainFrame.ClipsDescendants = true
Instance.new("UICorner", MainFrame).CornerRadius = UDim.new(0.035, 0)

-- Sombra externa
local Shadow = Instance.new("Frame", MainFrame)
Shadow.Size = UDim2.new(1.05, 0, 1.05, 0)
Shadow.Position = UDim2.new(-0.025, 0, -0.025, 0)
Shadow.BackgroundColor3 = Color3.fromRGB(0,0,0)
Shadow.BackgroundTransparency = 0.3
Shadow.ZIndex = -1
Instance.new("UICorner", Shadow).CornerRadius = UDim.new(0.037, 0)

-- Barra superior de arrastre
local TopBar = Instance.new("Frame", MainFrame)
TopBar.Size = UDim2.new(1, 0, 0.12, 0)
TopBar.BackgroundColor3 = Color3.fromRGB(25, 25, 35)
TopBar.BorderSizePixel = 0
Instance.new("UICorner", TopBar).CornerRadius = UDim.new(0.035, 0)

-- Título del menú
local Title = Instance.new("TextLabel", TopBar)
Title.Size = UDim2.new(1, -20, 1, 0)
Title.Position = UDim2.new(0, 10, 0, 0)
Title.BackgroundTransparency = 1
Title.Text = "⚡ BOLTAGUE AIMBOT ⚡"
Title.TextColor3 = Color3.fromRGB(255, 215, 0)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 22
Title.TextScaled = false
Title.TextWrapped = true

-- Etiqueta de estado e ID
local InfoLabel = Instance.new("TextLabel", MainFrame)
InfoLabel.Position = UDim2.new(0.05, 0, 0.125, 0)
InfoLabel.Size = UDim2.new(0.9, 0, 0.05, 0)
InfoLabel.BackgroundColor3 = Color3.fromRGB(18, 18, 28)
InfoLabel.Text = "Protected: 0 | ID: " .. Player.UserId .. " (Free Version)"
InfoLabel.TextColor3 = Color3.fromRGB(50, 255, 120)
InfoLabel.Font = Enum.Font.GothamSemibold
InfoLabel.TextSize = 15
InfoLabel.BackgroundTransparency = 0.1
Instance.new("UICorner", InfoLabel).CornerRadius = UDim.new(0.02, 0)

-- Función para crear botones con estilo
local function CreateStyledButton(parent, posY, texto, colorFondo, colorTexto)
    local Btn = Instance.new("TextButton", parent)
    Btn.Size = UDim2.new(0.9, 0, 0.085, 0)
    Btn.Position = UDim2.new(0.05, 0, posY, 0)
    Btn.BackgroundColor3 = colorFondo
    Btn.TextColor3 = colorTexto or Color3.new(1,1,1)
    Btn.Text = texto
    Btn.Font = Enum.Font.GothamBold
    Btn.TextSize = 18
    Btn.AutoButtonColor = false
    Btn.BorderSizePixel = 0
    Instance.new("UICorner", Btn).CornerRadius = UDim.new(0.025, 0)

    -- Efecto al pasar el mouse
    local CurrentColor = colorFondo

    Btn.MouseEnter:Connect(function()
        Btn.BackgroundColor3 = CurrentColor:Lerp(Color3.new(1,1,1), 0.15)
    end)

    Btn.MouseLeave:Connect(function()
        Btn.BackgroundColor3 = CurrentColor
    end)

    Btn:GetPropertyChangedSignal("BackgroundColor3"):Connect(function()
        CurrentColor = Btn.BackgroundColor3
    end)
    return Btn
end

-- Función para crear caja de texto (FOV)
local function CreateStyledTextBox(parent, posY, texto)
    local Box = Instance.new("TextBox", parent)
    Box.Size = UDim2.new(0.9, 0, 0.085, 0)
    Box.Position = UDim2.new(0.05, 0, posY, 0)
    Box.BackgroundColor3 = Color3.fromRGB(40, 40, 55)
    Box.TextColor3 = Color3.fromRGB(255, 80, 80)
    Box.PlaceholderColor3 = Color3.fromRGB(150,150,150)
    Box.Text = texto
    Box.Font = Enum.Font.GothamBold
    Box.TextSize = 18
    Box.TextEditable = true
    Box.ClearTextOnFocus = false
    Box.BorderSizePixel = 0
    Instance.new("UICorner", Box).CornerRadius = UDim.new(0.025, 0)
    return Box
end

-- Creación de botones
local ESPToggle = CreateStyledButton(MainFrame, 0.18, "ESP: OFF", Color3.fromRGB(220, 40, 40))
local AimbotToggle = CreateStyledButton(MainFrame, 0.28, "Aimbot: OFF", Color3.fromRGB(220, 40, 40))
local InventoryViewToggle = CreateStyledButton(MainFrame, 0.38, "InventoryView: OFF", Color3.fromRGB(220, 40, 40))
local FOVSlider = CreateStyledTextBox(MainFrame, 0.48, "FOV: 110")
local AimPartToggle = CreateStyledButton(MainFrame, 0.58, "Target: Head (fixed)", Color3.fromRGB(80, 120, 255))
local WallcheckToggle = CreateStyledButton(MainFrame, 0.68, "Wallcheck: ON", Color3.fromRGB(255, 110, 110))

-- Lista de jugadores protegidos
local PlayerListFrame = Instance.new("ScrollingFrame", MainFrame)
PlayerListFrame.Size = UDim2.new(0.9, 0, 0.23, 0)
PlayerListFrame.Position = UDim2.new(0.05, 0, 0.78, 0)
PlayerListFrame.BackgroundColor3 = Color3.fromRGB(22, 22, 32)
PlayerListFrame.ScrollBarThickness = 5
PlayerListFrame.ScrollBarImageColor3 = Color3.fromRGB(100,100,255)
PlayerListFrame.AutomaticCanvasSize = Enum.AutomaticSize.Y
PlayerListFrame.BorderSizePixel = 0
Instance.new("UICorner", PlayerListFrame).CornerRadius = UDim.new(0.025, 0)

local PlayerListLayout = Instance.new("UIListLayout", PlayerListFrame)
PlayerListLayout.Padding = UDim.new(0, 5)

-- Variables
local espEnabled = false
local AimbotOn = false
local InventoryViewEnabled = false
local FOVRadius = 110
local WallCheckEnabled = true
local ProtectedPlayers = {}
local PlayerButtons = {}
local AIM_SMOOTHNESS = 1.0
local guiOpen = true

local FOVCircle = Drawing.new("Circle")
FOVCircle.Radius = FOVRadius
FOVCircle.Thickness = 2
FOVCircle.Color = Color3.fromRGB(255,0,0)
FOVCircle.Transparency = 0.6
FOVCircle.Filled = false
FOVCircle.Visible = false

-- Almacenamiento de los objetos visuales del inventario
local InventoryObjects = {}
local LastInventoryState = {}
local ToolNameCache = {}

-- Aimbot modes
local AIM_MODES = {
    {name = "Head (fixed)",               part = "Head",                                color = Color3.fromRGB(100,100,255)},
    {name = "Torso (fixed)",              part = "HumanoidRootPart",                    color = Color3.fromRGB(255,150,50)},
    {name = "Right Arm (fixed)",          part = "RightUpperArm",                       color = Color3.fromRGB(50,205,50)},
    {name = "Left Arm (fixed)",           part = "LeftUpperArm",                        color = Color3.fromRGB(50,255,150)},
    {name = "Auto Switch (Head ↔ Torso)", parts = {"Head", "HumanoidRootPart"}, color = Color3.fromRGB(180,100,255)},
    {name = "Auto Switch (Right Arm ↔ Left Arm)", 
        parts = {"RightUpperArm", "LeftUpperArm"},                              color = Color3.fromRGB(255, 255, 0)}
}

local currentModeIndex = 1
local currentAutoIndex = 1
local lastSwitchTime = 0
local SWITCH_INTERVAL = 0.7

-- === UTILITY FUNCTIONS ===
local function IsAlive(char)
    local h = char and char:FindFirstChildOfClass("Humanoid")
    return h and h.Health > 0
end

local function IsVisible(part)
    if not part then return false end
    local origin = Camera.CFrame.Position
    local direction = (part.Position - origin)
    local params = RaycastParams.new()
    params.FilterType = Enum.RaycastFilterType.Blacklist
    params.FilterDescendantsInstances = {Player.Character or workspace, part.Parent}
    local result = workspace:Raycast(origin, direction, params)
    return not result
end

local function getRarityColor(rarity)
    local colors = {
        Common = Color3.fromRGB(0, 255, 0),     -- 🟢 Verde
        Rare = Color3.fromRGB(0, 0, 255),       -- 🔵 Azul
        Epic = Color3.fromRGB(128, 0, 128),     -- 🟣 Morado
        Legendary = Color3.fromRGB(255, 215, 0),-- 🟡 Dorado
        Uncommon = Color3.fromRGB(128, 128, 128)-- ⚪ Gris
    }
    return colors[rarity] or Color3.fromRGB(255,255,255)
end

local function getToolTexture(tool)
    if not tool then return "rbxassetid://4483345998" end
    if typeof(tool.TextureId) == "string" and tool.TextureId ~= "" then return tool.TextureId end
    if tool:GetAttribute("ImageId") then return tool:GetAttribute("ImageId") end
    local handle = tool:FindFirstChild("Handle")
    if handle then
        if handle:IsA("MeshPart") and handle.TextureID ~= "" then return handle.TextureID end
        for _, decal in ipairs(handle:GetChildren()) do
            if decal:IsA("Decal") and decal.Texture ~= "" then return decal.Texture end
        end
    end
    return "rbxassetid://4483345998"
end

local function matchToolName(tool)
    if not tool then return "Unknown", getToolTexture(nil) end
    
    if ToolNameCache[tool.Name] then
        return ToolNameCache[tool.Name], getToolTexture(tool)
    end
    
    local handle = tool:FindFirstChild("Handle")
    if not handle then 
        ToolNameCache[tool.Name] = tool.Name
        return tool.Name, getToolTexture(tool) 
    end
    
    local names = {}
    for _, child in ipairs(handle:GetChildren()) do names[child.Name] = true end
    
    for _, source in ipairs({ReplicatedStorage:FindFirstChild("Items"), StarterPack}) do
        if source then
            for _, item in ipairs(source:GetDescendants()) do
                if item:IsA("Tool") and item:FindFirstChild("Handle") then
                    local matches = true
                    for name in pairs(names) do
                        if not item.Handle:FindFirstChild(name) then matches = false break end
                    end
                    if matches then 
                        ToolNameCache[tool.Name] = item.Name
                        return item.Name, getToolTexture(item) 
                    end
                end
            end
        end
    end
    
    ToolNameCache[tool.Name] = tool.Name
    return tool.Name, getToolTexture(tool)
end

local function getPlayerTools(player)
    local tools = {}
    if not player then return tools end
    for _, container in ipairs({player.Backpack, player.Character}) do
        if container then
            for _, tool in ipairs(container:GetChildren()) do
                if tool:IsA("Tool") then 
                    local realName = matchToolName(tool)
                    local rarity = tool:GetAttribute("RarityName") or "Common"
                    local isEquipped = (tool.Parent == player.Character)
                    table.insert(tools, {
                        name = realName,
                        rarity = rarity,
                        equipped = isEquipped
                    })
                end
            end
        end
    end
    return tools
end

-- === SISTEMA DE INVENTARIO ===
local function createInventoryDisplay(player)
    if not player or InventoryObjects[player.Name] then return end
    local character = player.Character
    if not character then return end
    local rootPart = character:FindFirstChild("HumanoidRootPart")
    if not rootPart then return end

    local billboard = Instance.new("BillboardGui", rootPart)
    billboard.Name = "InventoryView"
    billboard.Size = UDim2.new(0, 300, 0, 100)
    billboard.StudsOffset = Vector3.new(0, -4, 0)
    billboard.AlwaysOnTop = true
    billboard.Active = false

    local listContainer = Instance.new("Frame", billboard)
    listContainer.Size = UDim2.new(1, 0, 1, 0)
    listContainer.BackgroundTransparency = 1

    local listLayout = Instance.new("UIListLayout", listContainer)
    listLayout.SortOrder = Enum.SortOrder.LayoutOrder
    listLayout.Padding = UDim.new(0, 2)

    InventoryObjects[player.Name] = {
        Gui = billboard,
        Container = listContainer,
        Layout = listLayout
    }
end

local function updateInventoryDisplay(player)
    if not InventoryViewEnabled or not InventoryObjects[player.Name] then return end

    local tools = getPlayerTools(player)
    local inventoryString = ""
    for _, toolData in ipairs(tools) do
        inventoryString = inventoryString .. toolData.name .. toolData.rarity .. tostring(toolData.equipped)
    end
    if LastInventoryState[player] == inventoryString then
        return
    end
    LastInventoryState[player] = inventoryString

    local data = InventoryObjects[player.Name]

    for _, child in ipairs(data.Container:GetChildren()) do
        if child:IsA("TextLabel") then child:Destroy() end
    end

    if #tools > 0 then
        for _, toolData in ipairs(tools) do
            local line = Instance.new("TextLabel", data.Container)
            line.Size = UDim2.new(1, 0, 0, 14)
            line.BackgroundTransparency = 1
            line.Font = Enum.Font.GothamBold
            line.TextSize = 12
            line.Text = "- " .. toolData.name
            line.TextColor3 = getRarityColor(toolData.rarity)

            if toolData.equipped then
                line.TextTransparency = 0
                line.TextStrokeTransparency = 0.8
            else
                line.TextTransparency = 0.1
                line.TextStrokeTransparency = 1
            end
        end
    end
end

local function removeInventoryDisplay(player)
    if InventoryObjects[player.Name] then
        InventoryObjects[player.Name].Gui:Destroy()
        InventoryObjects[player.Name] = nil
        LastInventoryState[player] = nil
    end
end

InventoryViewToggle.MouseButton1Click:Connect(function()
    InventoryViewEnabled = not InventoryViewEnabled
    InventoryViewToggle.Text = "InventoryView: " .. (InventoryViewEnabled and "ON" or "OFF")
    InventoryViewToggle.BackgroundColor3 = InventoryViewEnabled and Color3.fromRGB(30, 200, 60) or Color3.fromRGB(220, 40, 40)

    if InventoryViewEnabled then
        for _, p in pairs(Players:GetPlayers()) do
            if p ~= Player then createInventoryDisplay(p) end
        end
    else
        for _, p in pairs(Players:GetPlayers()) do removeInventoryDisplay(p) end
        InventoryObjects = {}
        LastInventoryState = {}
    end
end)

Players.PlayerAdded:Connect(function(p)
    p.CharacterAdded:Connect(function()
        task.wait(0.5)
        if InventoryViewEnabled then createInventoryDisplay(p) end
    end)
end)
Players.PlayerRemoving:Connect(removeInventoryDisplay)

-- === ESP ===
local function removeESP(char)
    if char then
        local head = char:FindFirstChild("Head")
        if head then 
            local b = head:FindFirstChild("AnouarNameHP") 
            if b then b:Destroy() end 
        end
        local h = char:FindFirstChild("AnouarHighlight") 
        if h then h:Destroy() end
    end
end

local function applyESP(char)
    local plr = Players:GetPlayerFromCharacter(char)
    if not plr or plr == Player then return end
    removeESP(char)

    local head = char:FindFirstChild("Head")
    local hum = char:FindFirstChildOfClass("Humanoid")
    if not head or not hum or not IsAlive(char) then return end

    local bill = Instance.new("BillboardGui", head)
    bill.Name = "AnouarNameHP"
    bill.Adornee = head
    bill.Size = UDim2.new(0,180,0,40)
    bill.StudsOffset = Vector3.new(0,2.8,0)
    bill.AlwaysOnTop = true

    local name = Instance.new("TextLabel", bill)
    name.Size = UDim2.new(1,0,0,18)
    name.BackgroundTransparency = 1
    name.Text = plr.DisplayName ~= plr.Name and (plr.DisplayName .. " (@" .. plr.Name .. ")") or plr.Name
    name.TextColor3 = Color3.new(1,1,1)
    name.TextStrokeTransparency = 0
    name.Font = Enum.Font.GothamBold
    name.TextSize = 14

    local hpBg = Instance.new("Frame", bill)
    hpBg.Size = UDim2.new(1,-6,0,6)
    hpBg.Position = UDim2.new(0,3,0,18)
    hpBg.BackgroundColor3 = Color3.new(0,0,0)
    Instance.new("UICorner", hpBg).CornerRadius = UDim.new(0,3)

    local hpFill = Instance.new("Frame", hpBg)
    hpFill.Size = UDim2.new(1,0,1,0)
    hpFill.BackgroundColor3 = Color3.fromRGB(0,255,100)
    Instance.new("UICorner", hpFill).CornerRadius = UDim.new(0,3)

    local hpText = Instance.new("TextLabel", hpBg)
    hpText.Size = UDim2.new(1,0,1,0)
    hpText.BackgroundTransparency = 1
    hpText.TextColor3 = Color3.new(1,1,1)
    hpText.TextStrokeTransparency = 0
    hpText.TextSize = 9
    hpText.Font = Enum.Font.GothamBold

    local function updateHP()
        if hum.Parent and IsAlive(char) then
            local r = math.clamp(hum.Health / hum.MaxHealth, 0, 1)
            hpFill.Size = UDim2.new(r, 0, 1, 0)
            hpText.Text = math.floor(hum.Health) .. "/" .. hum.MaxHealth
        else
            removeESP(char)
        end
    end

    hum.HealthChanged:Connect(updateHP)
    hum.Died:Connect(function() removeESP(char) end)
    updateHP()

    local hl = Instance.new("Highlight", char)
    hl.Name = "AnouarHighlight"
    hl.OutlineColor = Color3.fromRGB(255,215,0)
    hl.OutlineTransparency = 0
    hl.FillTransparency = 1
end

local function onCharAdded(char)
    local plr = Players:GetPlayerFromCharacter(char)
    if not plr or plr == Player then return end
    task.delay(0.6, function()
        removeESP(char)
        if espEnabled then applyESP(char) end
        if InventoryViewEnabled then createInventoryDisplay(plr) end
    end)
end

for _, p in Players:GetPlayers() do
    if p ~= Player then
        p.CharacterAdded:Connect(onCharAdded)
        if p.Character then onCharAdded(p.Character) end
    end
end
Players.PlayerAdded:Connect(function(p)
    if p ~= Player then
        p.CharacterAdded:Connect(onCharAdded)
        if p.Character then onCharAdded(p.Character) end
    end
end)

RunService.Heartbeat:Connect(function()
    if espEnabled then
        for _, p in Players:GetPlayers() do
            if p ~= Player and p.Character then
                local head = p.Character:FindFirstChild("Head")
                if head and not head:FindFirstChild("AnouarNameHP") then
                    applyESP(p.Character)
                end
            end
        end
    end
    if InventoryViewEnabled then
        for _, p in pairs(Players:GetPlayers()) do
            if p ~= Player then updateInventoryDisplay(p) end
        end
    end
end)

ESPToggle.MouseButton1Click:Connect(function()
    espEnabled = not espEnabled
    ESPToggle.Text = "ESP: " .. (espEnabled and "ON" or "OFF")
    ESPToggle.BackgroundColor3 = espEnabled and Color3.fromRGB(30, 200, 60) or Color3.fromRGB(220, 40, 40)
    for _, p in Players:GetPlayers() do
        if p ~= Player and p.Character then
            if espEnabled then 
                applyESP(p.Character) 
            else 
                removeESP(p.Character) 
            end
        end
    end
end)

-- === Protected Friends List ===
local function UpdateProtectedList()
    for _, b in PlayerButtons do b:Destroy() end
    PlayerButtons = {}
    for _, p in Players:GetPlayers() do
        if p ~= Player then
            local btn = Instance.new("TextButton", PlayerListFrame)
            btn.Size = UDim2.new(1,-10,0,30)
            local prot = ProtectedPlayers[p] or false
            btn.BackgroundColor3 = prot and Color3.fromRGB(40, 80, 200) or Color3.fromRGB(45, 45, 60)
            btn.Text = p.DisplayName .. " (@" .. p.Name .. ")" .. (prot and " ✔" or "")
            btn.TextColor3 = Color3.new(1,1,1)
            btn.Font = Enum.Font.GothamSemibold
            btn.TextSize = 13
            btn.AutoButtonColor = false
            Instance.new("UICorner", btn).CornerRadius = UDim.new(0,6)
            table.insert(PlayerButtons, btn)

            btn.MouseButton1Click:Connect(function()
                ProtectedPlayers[p] = not ProtectedPlayers[p]
                UpdateProtectedList()
            end)
        end
    end
    local count = 0 
    for _ in pairs(ProtectedPlayers) do count = count + 1 end
    InfoLabel.Text = "Protected: " .. count .. " | ID: " .. Player.UserId .. " (Free Version)"
end

Players.PlayerAdded:Connect(UpdateProtectedList)
Players.PlayerRemoving:Connect(UpdateProtectedList)
UpdateProtectedList()

-- === AIMBOT ===
local function GetTargetPart(char)
    local mode = AIM_MODES[currentModeIndex]
    local partName

    if mode.parts then
        partName = mode.parts[currentAutoIndex]
    else
        partName = mode.part
    end

    local part = char:FindFirstChild(partName)
    
    if not part then
        if partName == "RightUpperArm" then part = char:FindFirstChild("Right Arm") end
        if partName == "LeftUpperArm"   then part = char:FindFirstChild("Left Arm") end
    end
    
    return part or char:FindFirstChild("Head") or char:FindFirstChild("HumanoidRootPart")
end

local function GetClosest()
    local closest, distMin = nil, math.huge
    local center = Camera.ViewportSize / 2

    for _, p in Players:GetPlayers() do
        if p ~= Player and not ProtectedPlayers[p] and p.Character and IsAlive(p.Character) then
            local part = GetTargetPart(p.Character)
            if part then
                local screenPos, onScreen = Camera:WorldToViewportPoint(part.Position)
                if onScreen then
                    local dist = (Vector2.new(screenPos.X, screenPos.Y) - center).Magnitude
                    if dist < distMin and dist <= FOVRadius then
                        if not WallCheckEnabled or IsVisible(part) then
                            distMin = dist
                            closest = p
                        end
                    end
                end
            end
        end
    end
    return closest
end

RunService.RenderStepped:Connect(function()
    FOVCircle.Position = Camera.ViewportSize / 2
    FOVCircle.Radius = FOVRadius
    FOVCircle.Visible = AimbotOn

    if AimbotOn then
        local target = GetClosest()
        if target and target.Character then
            local part = GetTargetPart(target.Character)
            if part then
                local cf = CFrame.new(Camera.CFrame.Position, part.Position)
                Camera.CFrame = Camera.CFrame:Lerp(cf, AIM_SMOOTHNESS)
            end
        end
    end
end)

RunService.Heartbeat:Connect(function(dt)
    if not AimbotOn then return end
    local mode = AIM_MODES[currentModeIndex]
    if not mode.parts then return end

    lastSwitchTime = lastSwitchTime + dt
    if lastSwitchTime >= SWITCH_INTERVAL then
        lastSwitchTime = 0
        currentAutoIndex = currentAutoIndex % #mode.parts + 1
    end
end)

-- === FUNCIONALIDADES DE BOTONES ===
AimbotToggle.MouseButton1Click:Connect(function()
    AimbotOn = not AimbotOn
    AimbotToggle.Text = "Aimbot: " .. (AimbotOn and "ON" or "OFF")
    AimbotToggle.BackgroundColor3 = AimbotOn and Color3.fromRGB(30, 200, 60) or Color3.fromRGB(220, 40, 40)
end)

AimPartToggle.MouseButton1Click:Connect(function()
    currentModeIndex = currentModeIndex % #AIM_MODES + 1
    local mode = AIM_MODES[currentModeIndex]
    AimPartToggle.Text = "Target: " .. mode.name
    AimPartToggle.BackgroundColor3 = mode.color
end)

WallcheckToggle.MouseButton1Click:Connect(function()
    WallCheckEnabled = not WallCheckEnabled
    WallcheckToggle.Text = "Wallcheck: " .. (WallCheckEnabled and "ON" or "OFF")
    WallcheckToggle.BackgroundColor3 = WallCheckEnabled and Color3.fromRGB(30, 200, 60) or Color3.fromRGB(220, 40, 40)
end)

FOVSlider.FocusLost:Connect(function(enterPressed)
    if enterPressed then
        local num = tonumber(FOVSlider.Text:match("%d+"))
        if num and num >= 20 and num <= 600 then
            FOVRadius = num
            FOVCircle.Radius = num
            FOVSlider.Text = "FOV: " .. num
        else
            FOVSlider.Text = "FOV: " .. FOVRadius
        end
    end
end)

-- === TECLA G PARA ABRIR/CERRAR ===
UserInputService.InputBegan:Connect(function(input, gp)
    if gp then return end
    if input.KeyCode == Enum.KeyCode.G then
        guiOpen = not guiOpen
        MainFrame.Visible = guiOpen
        if guiOpen then UpdateProtectedList() end
    end
end)

-- === ARRASTRAR MENÚ ===
local function makeDraggable(frame, dragArea)
    local dragging, startPos, startMouse
    dragArea.InputBegan:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragging = true
            startPos = frame.Position
            startMouse = input.Position
        end
    end)
    dragArea.InputChanged:Connect(function(input)
        if dragging and input.UserInputType == Enum.UserInputType.MouseMovement then
            local delta = input.Position - startMouse
            frame.Position = UDim2.new(
                startPos.X.Scale, startPos.X.Offset + delta.X,
                startPos.Y.Scale, startPos.Y.Offset + delta.Y
            )
        end
    end)
    UserInputService.InputEnded:Connect(function(input)
        if input.UserInputType == Enum.UserInputType.MouseButton1 then
            dragging = false
        end
    end)
end

makeDraggable(MainFrame, TopBar)

print("✅ MENÚ BOLTAGUE CARGADO - VERSIÓN ABIERTA Y GRATUITA")
