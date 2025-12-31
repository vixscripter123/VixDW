--[=[
db    db d888888b db    db .d8888.  .o88b. d8888b. d888888b d8888b. d888888b 
88    88   `88'   `8b  d8' 88'  YP d8P  Y8 88  `8D   `88'   88  `8D `~~88~~' 
Y8    8P    88     `8bd8'  `8bo.   8P      88oobY'    88    88oodD'    88    
`8b  d8'    88     .dPYb.    `Y8b. 8b      88`8b      88    88~~~      88    
 `8bd8'    .88.   .8P  Y8. db   8D Y8b  d8 88 `88.   .88.   88         88    
   YP    Y888888P YP    YP `8888Y'  `Y88P' 88   YD Y888888P 88         YP    

VixScript - Menu Completo para Dandy's World
Baseado nos scripts Vix-gobby e Vix-Noxipus - Versão Completa 2024
]=]

local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")
local Workspace = game:GetService("Workspace")
local Lighting = game:GetService("Lighting")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

local player = Players.LocalPlayer

-- ============================================
-- SISTEMA DE ARMAZENAMENTO
-- ============================================
local VixData = {}

function VixData:save(key, value)
    local success, err = pcall(function()
        writefile("VixDW_"..key..".json", game:GetService("HttpService"):JSONEncode(value))
    end)
    return success
end

function VixData:load(key, default)
    local success, result = pcall(function()
        if isfile("VixDW_"..key..".json") then
            return game:GetService("HttpService"):JSONDecode(readfile("VixDW_"..key..".json"))
        end
        return default
    end)
    return success and result or default
end

-- ============================================
-- CRIAÇÃO DA UI
-- ============================================
local VixUI = {}

VixUI.ScreenGui = Instance.new("ScreenGui")
VixUI.ScreenGui.Name = "VixScript"
VixUI.ScreenGui.ResetOnSpawn = false
VixUI.ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

-- Proteger de exclusão
if gethui then
    VixUI.ScreenGui.Parent = gethui()
elseif syn and syn.protect_gui then
    syn.protect_gui(VixUI.ScreenGui)
    VixUI.ScreenGui.Parent = game:GetService("CoreGui")
else
    VixUI.ScreenGui.Parent = game:GetService("CoreGui")
end

-- Botão de abrir menu (móvel)
VixUI.OpenButton = Instance.new("TextButton")
VixUI.OpenButton.Name = "OpenButton"
VixUI.OpenButton.Size = UDim2.new(0, 70, 0, 70)
VixUI.OpenButton.Position = UDim2.new(0, 20, 0, 20)
VixUI.OpenButton.BackgroundColor3 = Color3.fromRGB(15, 35, 6)
VixUI.OpenButton.Text = ""
VixUI.OpenButton.BorderSizePixel = 0
VixUI.OpenButton.Parent = VixUI.ScreenGui

local OpenCorner = Instance.new("UICorner")
OpenCorner.CornerRadius = UDim.new(0.15, 0)
OpenCorner.Parent = VixUI.OpenButton

local OpenStroke = Instance.new("UIStroke")
OpenStroke.Color = Color3.fromRGB(50, 255, 50)
OpenStroke.Thickness = 3
OpenStroke.Parent = VixUI.OpenButton

local OpenIcon = Instance.new("TextLabel")
OpenIcon.Size = UDim2.new(1, 0, 1, 0)
OpenIcon.BackgroundTransparency = 1
OpenIcon.Text = "V"
OpenIcon.TextColor3 = Color3.fromRGB(50, 255, 50)
OpenIcon.Font = Enum.Font.GothamBold
OpenIcon.TextSize = 42
OpenIcon.Parent = VixUI.OpenButton

-- Frame principal
VixUI.MainFrame = Instance.new("Frame")
VixUI.MainFrame.Name = "MainFrame"
VixUI.MainFrame.Size = UDim2.new(0, 850, 0, 550)
VixUI.MainFrame.Position = UDim2.new(0.5, -425, 0.5, -275)
VixUI.MainFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
VixUI.MainFrame.BorderSizePixel = 0
VixUI.MainFrame.Visible = false
VixUI.MainFrame.Parent = VixUI.ScreenGui

local MainCorner = Instance.new("UICorner")
MainCorner.CornerRadius = UDim.new(0, 12)
MainCorner.Parent = VixUI.MainFrame

local MainStroke = Instance.new("UIStroke")
MainStroke.Color = Color3.fromRGB(50, 255, 50)
MainStroke.Thickness = 2
MainStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
MainStroke.Parent = VixUI.MainFrame

-- Header
VixUI.Header = Instance.new("Frame")
VixUI.Header.Name = "Header"
VixUI.Header.Size = UDim2.new(1, 0, 0, 70)
VixUI.Header.BackgroundColor3 = Color3.fromRGB(21, 51, 6)
VixUI.Header.BorderSizePixel = 0
VixUI.Header.Parent = VixUI.MainFrame

local HeaderCorner = Instance.new("UICorner")
HeaderCorner.CornerRadius = UDim.new(0, 12)
HeaderCorner.Parent = VixUI.Header

local HeaderBottom = Instance.new("Frame")
HeaderBottom.Size = UDim2.new(1, 0, 0, 12)
HeaderBottom.Position = UDim2.new(0, 0, 1, -12)
HeaderBottom.BackgroundColor3 = Color3.fromRGB(21, 51, 6)
HeaderBottom.BorderSizePixel = 0
HeaderBottom.Parent = VixUI.Header

-- Título
VixUI.Title = Instance.new("TextLabel")
VixUI.Title.Name = "Title"
VixUI.Title.Size = UDim2.new(0, 300, 1, 0)
VixUI.Title.Position = UDim2.new(0, 20, 0, 0)
VixUI.Title.BackgroundTransparency = 1
VixUI.Title.Text = "VixDW"
VixUI.Title.TextColor3 = Color3.fromRGB(255, 255, 255)
VixUI.Title.Font = Enum.Font.GothamBold
VixUI.Title.TextSize = 32
VixUI.Title.TextXAlignment = Enum.TextXAlignment.Left
VixUI.Title.Parent = VixUI.Header

-- Subtitle
VixUI.Subtitle = Instance.new("TextLabel")
VixUI.Subtitle.Size = UDim2.new(0, 300, 0, 20)
VixUI.Subtitle.Position = UDim2.new(0, 20, 0, 45)
VixUI.Subtitle.BackgroundTransparency = 1
VixUI.Subtitle.Text = "Dandy's World Edition v2.0"
VixUI.Subtitle.TextColor3 = Color3.fromRGB(150, 150, 150)
VixUI.Subtitle.Font = Enum.Font.Gotham
VixUI.Subtitle.TextSize = 14
VixUI.Subtitle.TextXAlignment = Enum.TextXAlignment.Left
VixUI.Subtitle.Parent = VixUI.Header

-- Botão Minimize
VixUI.MinimizeBtn = Instance.new("TextButton")
VixUI.MinimizeBtn.Name = "MinimizeBtn"
VixUI.MinimizeBtn.Size = UDim2.new(0, 50, 0, 50)
VixUI.MinimizeBtn.Position = UDim2.new(1, -60, 0.5, -25)
VixUI.MinimizeBtn.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
VixUI.MinimizeBtn.Text = "_"
VixUI.MinimizeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
VixUI.MinimizeBtn.Font = Enum.Font.GothamBold
VixUI.MinimizeBtn.TextSize = 28
VixUI.MinimizeBtn.BorderSizePixel = 0
VixUI.MinimizeBtn.Parent = VixUI.Header

local MinCorner = Instance.new("UICorner")
MinCorner.CornerRadius = UDim.new(0.2, 0)
MinCorner.Parent = VixUI.MinimizeBtn

-- Sidebar
VixUI.Sidebar = Instance.new("Frame")
VixUI.Sidebar.Name = "Sidebar"
VixUI.Sidebar.Size = UDim2.new(0, 200, 1, -80)
VixUI.Sidebar.Position = UDim2.new(0, 10, 0, 80)
VixUI.Sidebar.BackgroundColor3 = Color3.fromRGB(21, 51, 6)
VixUI.Sidebar.BorderSizePixel = 0
VixUI.Sidebar.Parent = VixUI.MainFrame

local SidebarCorner = Instance.new("UICorner")
SidebarCorner.CornerRadius = UDim.new(0, 10)
SidebarCorner.Parent = VixUI.Sidebar

local SidebarLayout = Instance.new("UIListLayout")
SidebarLayout.Padding = UDim.new(0, 8)
SidebarLayout.SortOrder = Enum.SortOrder.LayoutOrder
SidebarLayout.Parent = VixUI.Sidebar

local SidebarPadding = Instance.new("UIPadding")
SidebarPadding.PaddingTop = UDim.new(0, 10)
SidebarPadding.PaddingLeft = UDim.new(0, 10)
SidebarPadding.PaddingRight = UDim.new(0, 10)
SidebarPadding.Parent = VixUI.Sidebar

-- Content Area
VixUI.ContentArea = Instance.new("ScrollingFrame")
VixUI.ContentArea.Name = "ContentArea"
VixUI.ContentArea.Size = UDim2.new(0, 620, 1, -80)
VixUI.ContentArea.Position = UDim2.new(0, 220, 0, 80)
VixUI.ContentArea.BackgroundColor3 = Color3.fromRGB(21, 51, 6)
VixUI.ContentArea.BorderSizePixel = 0
VixUI.ContentArea.ScrollBarThickness = 8
VixUI.ContentArea.ScrollBarImageColor3 = Color3.fromRGB(50, 255, 50)
VixUI.ContentArea.Parent = VixUI.MainFrame

local ContentCorner = Instance.new("UICorner")
ContentCorner.CornerRadius = UDim.new(0, 10)
ContentCorner.Parent = VixUI.ContentArea

local ContentLayout = Instance.new("UIListLayout")
ContentLayout.Padding = UDim.new(0, 10)
ContentLayout.SortOrder = Enum.SortOrder.LayoutOrder
ContentLayout.Parent = VixUI.ContentArea

local ContentPadding = Instance.new("UIPadding")
ContentPadding.PaddingTop = UDim.new(0, 15)
ContentPadding.PaddingLeft = UDim.new(0, 15)
ContentPadding.PaddingRight = UDim.new(0, 15)
ContentPadding.PaddingBottom = UDim.new(0, 15)
ContentPadding.Parent = VixUI.ContentArea

-- ============================================
-- FUNÇÕES DE UTILIDADE
-- ============================================

function VixUI:CreateTab(name, icon, order)
    local tab = Instance.new("TextButton")
    tab.Name = name
    tab.Size = UDim2.new(1, 0, 0, 50)
    tab.BackgroundColor3 = Color3.fromRGB(30, 75, 10)
    tab.Text = (icon and icon.." " or "")..name
    tab.TextColor3 = Color3.fromRGB(255, 255, 255)
    tab.Font = Enum.Font.Gotham
    tab.TextSize = 16
    tab.BorderSizePixel = 0
    tab.LayoutOrder = order
    tab.Parent = VixUI.Sidebar
    
    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0.15, 0)
    corner.Parent = tab
    
    tab.MouseEnter:Connect(function()
        TweenService:Create(tab, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(40, 100, 15)}):Play()
    end)
    
    tab.MouseLeave:Connect(function()
        TweenService:Create(tab, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(30, 75, 10)}):Play()
    end)
    
    return tab
end

function VixUI:CreateButton(text, callback)
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(1, -20, 0, 45)
    button.BackgroundColor3 = Color3.fromRGB(30, 75, 10)
    button.Text = text
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.Font = Enum.Font.Gotham
    button.TextSize = 15
    button.BorderSizePixel = 0
    button.Parent = VixUI.ContentArea
    
    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0.15, 0)
    corner.Parent = button
    
    local stroke = Instance.new("UIStroke")
    stroke.Color = Color3.fromRGB(50, 255, 50)
    stroke.Thickness = 1
    stroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border
    stroke.Parent = button
    
    button.MouseButton1Click:Connect(function()
        if callback then callback() end
    end)
    
    button.MouseEnter:Connect(function()
        TweenService:Create(button, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(40, 100, 15)}):Play()
        TweenService:Create(stroke, TweenInfo.new(0.2), {Thickness = 2}):Play()
    end)
    
    button.MouseLeave:Connect(function()
        TweenService:Create(button, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(30, 75, 10)}):Play()
        TweenService:Create(stroke, TweenInfo.new(0.2), {Thickness = 1}):Play()
    end)
    
    return button
end

function VixUI:CreateToggle(text, default, callback)
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(1, -20, 0, 45)
    frame.BackgroundColor3 = Color3.fromRGB(30, 75, 10)
    frame.BorderSizePixel = 0
    frame.Parent = VixUI.ContentArea
    
    local corner = Instance.new("UICorner")
    corner.CornerRadius = UDim.new(0.15, 0)
    corner.Parent = frame
    
    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(1, -60, 1, 0)
    label.Position = UDim2.new(0, 15, 0, 0)
    label.BackgroundTransparency = 1
    label.Text = text
    label.TextColor3 = Color3.fromRGB(255, 255, 255)
    label.Font = Enum.Font.Gotham
    label.TextSize = 15
    label.TextXAlignment = Enum.TextXAlignment.Left
    label.Parent = frame
    
    local toggle = Instance.new("TextButton")
    toggle.Size = UDim2.new(0, 40, 0, 25)
    toggle.Position = UDim2.new(1, -50, 0.5, -12.5)
    toggle.BackgroundColor3 = default and Color3.fromRGB(50, 255, 50) or Color3.fromRGB(100, 100, 100)
    toggle.Text = ""
    toggle.BorderSizePixel = 0
    toggle.Parent = frame
    
    local toggleCorner = Instance.new("UICorner")
    toggleCorner.CornerRadius = UDim.new(0.5, 0)
    toggleCorner.Parent = toggle
    
    local indicator = Instance.new("Frame")
    indicator.Size = UDim2.new(0, 18, 0, 18)
    indicator.Position = default and UDim2.new(1, -21, 0.5, -9) or UDim2.new(0, 3, 0.5, -9)
    indicator.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    indicator.BorderSizePixel = 0
    indicator.Parent = toggle
    
    local indicatorCorner = Instance.new("UICorner")
    indicatorCorner.CornerRadius = UDim.new(1, 0)
    indicatorCorner.Parent = indicator
    
    local enabled = default
    
    toggle.MouseButton1Click:Connect(function()
        enabled = not enabled
        
        TweenService:Create(toggle, TweenInfo.new(0.2), {
            BackgroundColor3 = enabled and Color3.fromRGB(50, 255, 50) or Color3.fromRGB(100, 100, 100)
        }):Play()
        
        TweenService:Create(indicator, TweenInfo.new(0.2), {
            Position = enabled and UDim2.new(1, -21, 0.5, -9) or UDim2.new(0, 3, 0.5, -9)
        }):Play()
        
        if callback then callback(enabled) end
    end)
    
    return frame
end

function VixUI:ClearContent()
    for _, child in ipairs(VixUI.ContentArea:GetChildren()) do
        if not child:IsA("UIListLayout") and not child:IsA("UIPadding") then
            child:Destroy()
        end
    end
end

-- ============================================
-- SISTEMA DE NOTIFICAÇÕES
-- ============================================

function VixUI:Notify(title, text, duration)
    local notif = Instance.new("Frame")
    notif.Size = UDim2.new(0, 300, 0, 80)
    notif.Position = UDim2.new(1, 320, 1, -100)
    notif.BackgroundColor3 = Color3.fromRGB(21, 51, 6)
    notif.BorderSizePixel = 0
    notif.Parent = VixUI.ScreenGui
    
    local notifCorner = Instance.new("UICorner")
    notifCorner.CornerRadius = UDim.new(0, 10)
    notifCorner.Parent = notif
    
    local notifStroke = Instance.new("UIStroke")
    notifStroke.Color = Color3.fromRGB(50, 255, 50)
    notifStroke.Thickness = 2
    notifStroke.Parent = notif
    
    local titleLabel = Instance.new("TextLabel")
    titleLabel.Size = UDim2.new(1, -20, 0, 25)
    titleLabel.Position = UDim2.new(0, 10, 0, 5)
    titleLabel.BackgroundTransparency = 1
    titleLabel.Text = title
    titleLabel.TextColor3 = Color3.fromRGB(50, 255, 50)
    titleLabel.Font = Enum.Font.GothamBold
    titleLabel.TextSize = 16
    titleLabel.TextXAlignment = Enum.TextXAlignment.Left
    titleLabel.Parent = notif
    
    local textLabel = Instance.new("TextLabel")
    textLabel.Size = UDim2.new(1, -20, 0, 45)
    textLabel.Position = UDim2.new(0, 10, 0, 30)
    textLabel.BackgroundTransparency = 1
    textLabel.Text = text
    textLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    textLabel.Font = Enum.Font.Gotham
    textLabel.TextSize = 14
    textLabel.TextXAlignment = Enum.TextXAlignment.Left
    textLabel.TextWrapped = true
    textLabel.Parent = notif
    
    TweenService:Create(notif, TweenInfo.new(0.5, Enum.EasingStyle.Back), {Position = UDim2.new(1, -310, 1, -100)}):Play()
    
    task.delay(duration or 3, function()
        TweenService:Create(notif, TweenInfo.new(0.5), {Position = UDim2.new(1, 320, 1, -100)}):Play()
        task.wait(0.5)
        notif:Destroy()
    end)
end

-- ============================================
-- FUNCIONALIDADES DO JOGO
-- ============================================

-- Variáveis globais
_G.VixAutoExtract = false
_G.VixAutoDistract = false
_G.VixESP = false
_G.VixFullbright = false
_G.VixSpeed = false
_G.VixInfiniteStamina = false
_G.VixNoclip = false
_G.VixAutoFarm = false

-- ============================================
-- NOCLIP V3 (DO VIX-GOBBY)
-- ============================================
local NoclipV3 = {}
NoclipV3.Enabled = false
NoclipV3.Connection = nil

function NoclipV3:Toggle(enabled)
    self.Enabled = enabled
    
    if enabled then
        self.Connection = RunService.Stepped:Connect(function()
            if not self.Enabled then return end
            
            local character = player.Character
            if character then
                for _, part in pairs(character:GetDescendants()) do
                    if part:IsA("BasePart") and part.CanCollide then
                        part.CanCollide = false
                    end
                end
            end
        end)
    else
        if self.Connection then
            self.Connection:Disconnect()
            self.Connection = nil
        end
        
        local character = player.Character
        if character then
            for _, part in pairs(character:GetDescendants()) do
                if part:IsA("BasePart") then
                    part.CanCollide = true
                end
            end
        end
    end
end

-- ============================================
-- ESP COMPLETO
-- ============================================
local ESPManager = {}
ESPManager.Enabled = false
ESPManager.Players = {}
ESPManager.Machines = {}
ESPManager.Items = {}
ESPManager.Twisteds = {}

function ESPManager:CreateESP(object, name, color)
    local billboard = Instance.new("BillboardGui")
    billboard.Name = "ESP"
    billboard.Adornee = object
    billboard.Size = UDim2.new(0, 100, 0, 50)
    billboard.StudsOffset = Vector3.new(0, 2, 0)
    billboard.AlwaysOnTop = true
    billboard.Parent = object
    
    local frame = Instance.new("Frame")
    frame.Size = UDim2.new(1, 0, 1, 0)
    frame.BackgroundTransparency = 1
    frame.Parent = billboard
    
    local label = Instance.new("TextLabel")
    label.Size = UDim2.new(1, 0, 1, 0)
    label.BackgroundTransparency = 1
    label.Text = name
    label.TextColor3 = color
    label.TextStrokeTransparency = 0.5
    label.Font = Enum.Font.GothamBold
    label.TextSize = 14
    label.Parent = frame
    
    return billboard
end

function ESPManager:Toggle(enabled)
    self.Enabled = enabled
    
    if enabled then
        -- ESP para jogadores
        for _, plr in pairs(Players:GetPlayers()) do
            if plr ~= player and plr.Character then
                local esp = self:CreateESP(plr.Character.HumanoidRootPart, plr.Name, Color3.fromRGB(0, 255, 0))
                table.insert(self.Players, esp)
            end
        end
        
        -- ESP para máquinas
        for _, machine in pairs(Workspace:GetDescendants()) do
            if machine.Name == "Machine" and machine:FindFirstChild("Activate") then
                local esp = self:CreateESP(machine, "Machine", Color3.fromRGB(255, 255, 0))
                table.insert(self.Machines, esp)
            end
        end
        
        -- ESP para itens
        for _, item in pairs(Workspace:GetDescendants()) do
            if item:IsA("Tool") or (item:IsA("Model") and item:FindFirstChild("Handle")) then
                local esp = self:CreateESP(item.PrimaryPart or item:FindFirstChild("Handle"), "Item", Color3.fromRGB(0, 255, 255))
                table.insert(self.Items, esp)
            end
        end
        
        -- ESP para Twisteds
        for _, twisted in pairs(Workspace:GetDescendants()) do
            if twisted.Name:find("Twisted") or twisted:FindFirstChild("TwistedTag") then
                local esp = self:CreateESP(twisted.PrimaryPart or twisted:FindFirstChild("HumanoidRootPart"), "Twisted!", Color3.fromRGB(255, 0, 0))
                table.insert(self.Twisteds, esp)
            end
        end
    else
        -- Remover todos os ESPs
        for _, esp in pairs(self.Players) do esp:Destroy() end
        for _, esp in pairs(self.Machines) do esp:Destroy() end
        for _, esp in pairs(self.Items) do esp:Destroy() end
        for _, esp in pairs(self.Twisteds) do esp:Destroy() end
        
        self.Players = {}
        self.Machines = {}
        self.Items = {}
        self.Twisteds = {}
    end
end

-- ============================================
-- AUTO EXTRACT AVANÇADO
-- ============================================
function StartAutoExtract()
    _G.VixAutoExtract = true
    spawn(function()
        while _G.VixAutoExtract do
            pcall(function()
                for _, machine in pairs(Workspace:GetDescendants()) do
                    if machine.Name == "Machine" and machine:FindFirstChild("Activate") then
                        local proximityPrompt = machine.Activate
                        if proximityPrompt:IsA("ProximityPrompt") then
                            fireproximityprompt(proximityPrompt)
                        end
                    end
                end
            end)
            task.wait(0.5)
        end
    end)
end

-- ============================================
-- FULLBRIGHT
-- ============================================
function ToggleFullbright(enabled)
    _G.VixFullbright = enabled
    if enabled then
        Lighting.Brightness = 2
        Lighting.ClockTime = 14
        Lighting.FogEnd = 100000
        Lighting.GlobalShadows = false
        Lighting.OutdoorAmbient = Color3.fromRGB(128, 128, 128)
    else
        Lighting.Brightness = 1
        Lighting.ClockTime = 12
        Lighting.FogEnd = 100000
        Lighting.GlobalShadows = true
    end
end

-- ============================================
-- SPEED HACK
-- ============================================
function ToggleSpeed(enabled)
    _G.VixSpeed = enabled
    local character = player.Character
    if character then
        local humanoid = character:FindFirstChild("Humanoid")
        if humanoid then
            humanoid.WalkSpeed = enabled and 50 or 16
        end
    end
end

-- ============================================
-- INFINITE STAMINA
-- ============================================
function ToggleInfiniteStamina(enabled)
    _G.VixInfiniteStamina = enabled
    if enabled then
        spawn(function()
            while _G.VixInfiniteStamina do
                pcall(function()
                    local character = player.Character
                    if character and character:FindFirstChild("Stamina") then
                        character.Stamina.Value = 100
                    end
                end)
                task.wait(0.1)
            end
        end)
    end
end

-- ============================================
-- REMOVE FOG
-- ============================================
function RemoveFog()
    Lighting.FogEnd = 100000
    for _, effect in pairs(Lighting:GetChildren()) do
        if effect:IsA("Atmosphere") then
            effect.Density = 0
        end
    end
end

-- ============================================
-- AUTO FARM COMPLETO
-- ============================================
function StartAutoFarm()
    _G.VixAutoFarm = true
    spawn(function()
        while _G.VixAutoFarm do
            pcall(function()
                -- Auto collect items
                for _, item in pairs(Workspace:GetDescendants()) do
                    if item:IsA("Tool") or (item:IsA("Model") and item:FindFirstChild("Handle")) then
                        local character = player.Character
                        if character and character:FindFirstChild("HumanoidRootPart") then
                            local distance = (character.HumanoidRootPart.Position - (item.PrimaryPart or item.Handle).Position).Magnitude
                            if distance < 50 then
                                character.HumanoidRootPart.CFrame = (item.PrimaryPart or item.Handle).CFrame
                                task.wait(0.5)
                            end
                        end
                    end
                end
                
                -- Auto extract machines
                for _, machine in pairs(Workspace:GetDescendants()) do
                    if machine.Name == "Machine" and machine:FindFirstChild("Activate") then
                        fireproximityprompt(machine.Activate)
                    end
                end
            end)
            task.wait(1)
        end
    end)
end

-- ============================================
-- TELEPORTS
-- ============================================
function TeleportToElevator()
    local elevator = Workspace:FindFirstChild("Elevators") and Workspace.Elevators:FindFirstChild("Elevator")
    if elevator then
        local character = player.Character
        if character and character:FindFirstChild("HumanoidRootPart") then
            character.HumanoidRootPart.CFrame = elevator:GetPivot() * CFrame.new(0, 3, 0)
            VixUI:Notify("Teleporte", "Teleportado para o elevador!", 2)
        end
    else
        VixUI:Notify("Erro", "Elevador não encontrado!", 2)
    end
end

-- ============================================
-- TABS
-- ============================================

-- Home Tab
local homeTab = VixUI:CreateTab("🏠 Home", nil, 1)
homeTab.MouseButton1Click:Connect(function()
    VixUI:ClearContent()
    
    local welcome = Instance.new("TextLabel")
    welcome.Size = UDim2.new(1, -20, 0, 100)
    welcome.BackgroundTransparency = 1
    welcome.Text = "Bem-vindo ao VixDW v2.0!\n\nScript completo para Dandy's World\nCom Noclip V3, ESP avançado e muito mais!"
    welcome.TextColor3 = Color3.fromRGB(255, 255, 255)
    welcome.Font = Enum.Font.GothamBold
    welcome.TextSize = 20
    welcome.TextWrapped = true
    welcome.Parent = VixUI.ContentArea
    
    VixUI:CreateButton("✅ Auto Extract Machines", function()
        StartAutoExtract()
        VixUI:Notify("Auto Extract", "Auto Extract ativado!", 2)
    end)
    
    VixUI:CreateButton("❌ Stop Auto Extract", function()
        _G.VixAutoExtract = false
        VixUI:Notify("Auto Extract", "Auto Extract desativado!", 2)
    end)
    
    VixUI:CreateButton("🚀 Start Auto Farm", function()
        StartAutoFarm()
        VixUI:Notify("Auto Farm", "Auto Farm ativado!", 2)
    end)
    
    VixUI:CreateButton("🛑 Stop Auto Farm", function()
        _G.VixAutoFarm = false
        VixUI:Notify("Auto Farm", "Auto Farm desativado!", 2)
    end)
end)

-- Player Tab
local playerTab = VixUI:CreateTab("👤 Player", nil, 2)
playerTab.MouseButton1Click:Connect(function()
    VixUI:ClearContent()
    
    VixUI:CreateToggle("Speed Hack (50)", false, function(enabled)
        ToggleSpeed(enabled)
        VixUI:Notify("Speed", enabled and "Speed ativado!" or "Speed desativado!", 2)
    end)
    
    VixUI:CreateToggle("Noclip V3", false, function(enabled)
        _G.VixNoclip = enabled
        NoclipV3:Toggle(enabled)
        VixUI:Notify("Noclip", enabled and "Noclip V3 ativado!" or "Noclip V3 desativado!", 2)
    end)
    
    VixUI:CreateToggle("Infinite Stamina", false, function(enabled)
        ToggleInfiniteStamina(enabled)
        VixUI:Notify("Stamina", enabled and "Stamina infinita ativada!" or "Stamina infinita desativada!", 2)
    end)
    
    VixUI:CreateButton("Remove Fog", function()
        RemoveFog()
        VixUI:Notify("Fog", "Neblina removida!", 2)
    end)
end)

-- ESP Tab
local espTab = VixUI:CreateTab("👁️ ESP", nil, 3)
espTab.MouseButton1Click:Connect(function()
    VixUI:ClearContent()
    
    VixUI:CreateToggle("ESP Completo", false, function(enabled)
        ESPManager:Toggle(enabled)
        VixUI:Notify("ESP", enabled and "ESP ativado!" or "ESP desativado!", 2)
    end)
    
    VixUI:CreateToggle("Fullbright", false, function(enabled)
        ToggleFullbright(enabled)
        VixUI:Notify("Fullbright", enabled and "Fullbright ativado!" or "Fullbright desativado!", 2)
    end)
    
    VixUI:CreateButton("Show Twisteds", function()
        for _, twisted in pairs(Workspace:GetDescendants()) do
            if twisted.Name:find("Twisted") then
                local highlight = Instance.new("Highlight")
                highlight.FillColor = Color3.fromRGB(255, 0, 0)
                highlight.OutlineColor = Color3.fromRGB(255, 255, 255)
                highlight.Parent = twisted
            end
        end
        VixUI:Notify("Twisteds", "Twisteds destacados!", 2)
    end)
end)

-- Teleport Tab
local tpTab = VixUI:CreateTab("🌍 Teleport", nil, 4)
tpTab.MouseButton1Click:Connect(function()
    VixUI:ClearContent()
    
    VixUI:CreateButton("Teleport to Elevator", function()
        TeleportToElevator()
    end)
    
    VixUI:CreateButton("Teleport to Players", function()
        for _, plr in pairs(Players:GetPlayers()) do
            if plr ~= player and plr.Character then
                local character = player.Character
                if character and character:FindFirstChild("HumanoidRootPart") then
                    character.HumanoidRootPart.CFrame = plr.Character.HumanoidRootPart.CFrame
                    VixUI:Notify("Teleporte", "Teleportado para " .. plr.Name, 2)
                    break
                end
            end
        end
    end)
end)

-- Settings Tab
local settingsTab = VixUI:CreateTab("⚙️ Settings", nil, 5)
settingsTab.MouseButton1Click:Connect(function()
    VixUI:ClearContent()
    
    VixUI:CreateButton("Save Settings", function()
        local settings = {
            Speed = _G.VixSpeed,
            Noclip = _G.VixNoclip,
            ESP = _G.VixESP,
            Fullbright = _G.VixFullbright,
            InfiniteStamina = _G.VixInfiniteStamina
        }
        VixData:save("settings", settings)
        VixUI:Notify("Settings", "Configurações salvas!", 2)
    end)
    
    VixUI:CreateButton("Load Settings", function()
        local settings = VixData:load("settings", {})
        if settings.Speed then ToggleSpeed(true) end
        if settings.Noclip then NoclipV3:Toggle(true) end
        if settings.ESP then ESPManager:Toggle(true) end
        if settings.Fullbright then ToggleFullbright(true) end
        if settings.InfiniteStamina then ToggleInfiniteStamina(true) end
        VixUI:Notify("Settings", "Configurações carregadas!", 2)
    end)
    
    VixUI:CreateButton("Reset All", function()
        _G.VixAutoExtract = false
        _G.VixAutoFarm = false
        _G.VixSpeed = false
        _G.VixNoclip = false
        _G.VixESP = false
        _G.VixFullbright = false
        _G.VixInfiniteStamina = false
        
        NoclipV3:Toggle(false)
        ESPManager:Toggle(false)
        ToggleSpeed(false)
        ToggleFullbright(false)
        
        VixUI:Notify("Reset", "Todas as funções desativadas!", 2)
    end)
end)

-- ============================================
-- SISTEMA DE ARRASTAR
-- ============================================

local dragging, dragInput, dragStart, startPos

VixUI.Header.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging = true
        dragStart = input.Position
        startPos = VixUI.MainFrame.Position
        
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

VixUI.Header.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
        dragInput = input
    end
end)

UserInputService.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        local delta = input.Position - dragStart
        VixUI.MainFrame.Position = UDim2.new(
            startPos.X.Scale,
            startPos.X.Offset + delta.X,
            startPos.Y.Scale,
            startPos.Y.Offset + delta.Y
        )
    end
end)

-- ============================================
-- BOTÕES DE CONTROLE
-- ============================================

VixUI.OpenButton.MouseButton1Click:Connect(function()
    VixUI.MainFrame.Visible = true
    VixUI.OpenButton.Visible = false
    
    VixUI.MainFrame.Size = UDim2.new(0, 0, 0, 0)
    VixUI.MainFrame.Position = UDim2.new(0.5, 0, 0.5, 0)
    
    TweenService:Create(VixUI.MainFrame, TweenInfo.new(0.4, Enum.EasingStyle.Back), {
        Size = UDim2.new(0, 850, 0, 550),
        Position = UDim2.new(0.5, -425, 0.5, -275)
    }):Play()
end)

VixUI.MinimizeBtn.MouseButton1Click:Connect(function()
    TweenService:Create(VixUI.MainFrame, TweenInfo.new(0.4, Enum.EasingStyle.Back), {
        Size = UDim2.new(0, 0, 0, 0),
        Position = UDim2.new(0.5, 0, 0.5, 0)
    }):Play()
    
    task.wait(0.4)
    VixUI.MainFrame.Visible = false
    VixUI.OpenButton.Visible = true
end)

-- ============================================
-- INICIALIZAÇÃO
-- ============================================

VixUI:Notify("VixDW", "Script carregado com sucesso! Pressione o botão V para abrir.", 5)

-- Auto-load home tab
homeTab.MouseButton1Click()

print("VixDW v2.0 - Dandy's World Script Carregado!")
print("Criado com base em Vix-gobby e Vix-Noxipus")
print("Features: Noclip V3, ESP Completo, Auto Farm, Speed Hack e mais!")
