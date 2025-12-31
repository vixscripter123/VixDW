--[=[
db    db d888888b db    db .d8888.  .o88b. d8888b. d888888b d8888b. d888888b 
88    88   `88'   `8b  d8' 88'  YP d8P  Y8 88  `8D   `88'   88  `8D `~~88~~' 
Y8    8P    88     `8bd8'  `8bo.   8P      88oobY'    88    88oodD'    88    
`8b  d8'    88     .dPYb.    `Y8b. 8b      88`8b      88    88~~~      88    
 `8bd8'    .88.   .8P  Y8. db   8D Y8b  d8 88 `88.   .88.   88         88    
   YP    Y888888P YP    YP `8888Y'  `Y88P' 88   YD Y888888P 88         YP    

VixScript - Dandy's World Edition | @uniquadev
]=]

local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local UIS = game:GetService("UserInputService")
local player = Players.LocalPlayer

-- Criar ScreenGui
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "VixScript"
ScreenGui.ResetOnSpawn = false
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
if gethui then ScreenGui.Parent = gethui() else ScreenGui.Parent = game.CoreGui end

-- Botão de Abrir
local OpenButton = Instance.new("TextButton", ScreenGui)
OpenButton.Size = UDim2.new(0, 70, 0, 70)
OpenButton.Position = UDim2.new(0, 20, 0, 20)
OpenButton.BackgroundColor3 = Color3.fromRGB(15, 35, 6)
OpenButton.Text = ""
OpenButton.BorderSizePixel = 0

local OpenCorner = Instance.new("UICorner", OpenButton)
OpenCorner.CornerRadius = UDim.new(0.2, 0)

local OpenStroke = Instance.new("UIStroke", OpenButton)
OpenStroke.Color = Color3.fromRGB(50, 255, 50)
OpenStroke.Thickness = 3

local OpenIcon = Instance.new("TextLabel", OpenButton)
OpenIcon.Size = UDim2.new(1, 0, 1, 0)
OpenIcon.BackgroundTransparency = 1
OpenIcon.Text = "V"
OpenIcon.TextColor3 = Color3.fromRGB(50, 255, 50)
OpenIcon.Font = Enum.Font.GothamBold
OpenIcon.TextSize = 42

-- Frame Principal
local MainFrame = Instance.new("Frame", ScreenGui)
MainFrame.Size = UDim2.new(0, 850, 0, 550)
MainFrame.Position = UDim2.new(0.5, -425, 0.5, -275)
MainFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 15)
MainFrame.BorderSizePixel = 0
MainFrame.Visible = false

local MainCorner = Instance.new("UICorner", MainFrame)
MainCorner.CornerRadius = UDim.new(0, 12)

local MainStroke = Instance.new("UIStroke", MainFrame)
MainStroke.Color = Color3.fromRGB(50, 255, 50)
MainStroke.Thickness = 2

-- Header
local Header = Instance.new("Frame", MainFrame)
Header.Size = UDim2.new(1, 0, 0, 70)
Header.BackgroundColor3 = Color3.fromRGB(21, 51, 6)
Header.BorderSizePixel = 0

local HeaderCorner = Instance.new("UICorner", Header)
HeaderCorner.CornerRadius = UDim.new(0, 12)

local HeaderBottom = Instance.new("Frame", Header)
HeaderBottom.Size = UDim2.new(1, 0, 0, 12)
HeaderBottom.Position = UDim2.new(0, 0, 1, -12)
HeaderBottom.BackgroundColor3 = Color3.fromRGB(21, 51, 6)
HeaderBottom.BorderSizePixel = 0

-- Título
local Title = Instance.new("TextLabel", Header)
Title.Size = UDim2.new(0, 300, 1, 0)
Title.Position = UDim2.new(0, 20, 0, 0)
Title.BackgroundTransparency = 1
Title.Text = "VixDW"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 32
Title.TextXAlignment = Enum.TextXAlignment.Left

local Subtitle = Instance.new("TextLabel", Header)
Subtitle.Size = UDim2.new(0, 300, 0, 20)
Subtitle.Position = UDim2.new(0, 20, 0, 45)
Subtitle.BackgroundTransparency = 1
Subtitle.Text = "Dandy's World Edition"
Subtitle.TextColor3 = Color3.fromRGB(150, 150, 150)
Subtitle.Font = Enum.Font.Gotham
Subtitle.TextSize = 14
Subtitle.TextXAlignment = Enum.TextXAlignment.Left

-- Botão Minimize
local MinimizeBtn = Instance.new("TextButton", Header)
MinimizeBtn.Size = UDim2.new(0, 50, 0, 50)
MinimizeBtn.Position = UDim2.new(1, -60, 0.5, -25)
MinimizeBtn.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
MinimizeBtn.Text = "_"
MinimizeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
MinimizeBtn.Font = Enum.Font.GothamBold
MinimizeBtn.TextSize = 28
MinimizeBtn.BorderSizePixel = 0

local MinCorner = Instance.new("UICorner", MinimizeBtn)
MinCorner.CornerRadius = UDim.new(0.2, 0)

-- Sidebar
local Sidebar = Instance.new("Frame", MainFrame)
Sidebar.Size = UDim2.new(0, 200, 1, -80)
Sidebar.Position = UDim2.new(0, 10, 0, 80)
Sidebar.BackgroundColor3 = Color3.fromRGB(21, 51, 6)
Sidebar.BorderSizePixel = 0

local SidebarCorner = Instance.new("UICorner", Sidebar)
SidebarCorner.CornerRadius = UDim.new(0, 10)

local SidebarLayout = Instance.new("UIListLayout", Sidebar)
SidebarLayout.Padding = UDim.new(0, 8)
SidebarLayout.SortOrder = Enum.SortOrder.LayoutOrder

local SidebarPadding = Instance.new("UIPadding", Sidebar)
SidebarPadding.PaddingTop = UDim.new(0, 10)
SidebarPadding.PaddingLeft = UDim.new(0, 10)
SidebarPadding.PaddingRight = UDim.new(0, 10)

-- Content Area
local ContentArea = Instance.new("ScrollingFrame", MainFrame)
ContentArea.Size = UDim2.new(0, 620, 1, -80)
ContentArea.Position = UDim2.new(0, 220, 0, 80)
ContentArea.BackgroundColor3 = Color3.fromRGB(21, 51, 6)
ContentArea.BorderSizePixel = 0
ContentArea.ScrollBarThickness = 8
ContentArea.ScrollBarImageColor3 = Color3.fromRGB(50, 255, 50)

local ContentCorner = Instance.new("UICorner", ContentArea)
ContentCorner.CornerRadius = UDim.new(0, 10)

local ContentLayout = Instance.new("UIListLayout", ContentArea)
ContentLayout.Padding = UDim.new(0, 10)
ContentLayout.SortOrder = Enum.SortOrder.LayoutOrder

local ContentPadding = Instance.new("UIPadding", ContentArea)
ContentPadding.PaddingTop = UDim.new(0, 15)
ContentPadding.PaddingLeft = UDim.new(0, 15)
ContentPadding.PaddingRight = UDim.new(0, 15)
ContentPadding.PaddingBottom = UDim.new(0, 15)

-- Funções de Criação de UI
local function CreateTab(name, order)
    local tab = Instance.new("TextButton", Sidebar)
    tab.Name = name
    tab.Size = UDim2.new(1, 0, 0, 50)
    tab.BackgroundColor3 = Color3.fromRGB(30, 75, 10)
    tab.Text = name
    tab.TextColor3 = Color3.fromRGB(255, 255, 255)
    tab.Font = Enum.Font.Gotham
    tab.TextSize = 16
    tab.BorderSizePixel = 0
    tab.LayoutOrder = order
    
    local corner = Instance.new("UICorner", tab)
    corner.CornerRadius = UDim.new(0.15, 0)
    
    tab.MouseEnter:Connect(function()
        TweenService:Create(tab, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(40, 100, 15)}):Play()
    end)
    
    tab.MouseLeave:Connect(function()
        TweenService:Create(tab, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(30, 75, 10)}):Play()
    end)
    
    return tab
end

local function CreateButton(text, callback)
    local button = Instance.new("TextButton", ContentArea)
    button.Size = UDim2.new(1, -20, 0, 45)
    button.BackgroundColor3 = Color3.fromRGB(30, 75, 10)
    button.Text = text
    button.TextColor3 = Color3.fromRGB(255, 255, 255)
    button.Font = Enum.Font.Gotham
    button.TextSize = 15
    button.BorderSizePixel = 0
    
    local corner = Instance.new("UICorner", button)
    corner.CornerRadius = UDim.new(0.15, 0)
    
    local stroke = Instance.new("UIStroke", button)
    stroke.Color = Color3.fromRGB(50, 255, 50)
    stroke.Thickness = 1
    
    button.MouseButton1Click:Connect(function()
        if callback then callback() end
    end)
    
    button.MouseEnter:Connect(function()
        TweenService:Create(button, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(40, 100, 15)}):Play()
    end)
    
    button.MouseLeave:Connect(function()
        TweenService:Create(button, TweenInfo.new(0.2), {BackgroundColor3 = Color3.fromRGB(30, 75, 10)}):Play()
    end)
    
    return button
end

local function CreateToggle(text, default, callback)
    local frame = Instance.new("Frame", ContentArea)
    frame.Size = UDim2.new(1, -20, 0, 45)
    frame.BackgroundColor3 = Color3.fromRGB(30, 75, 10)
    frame.BorderSizePixel = 0
    
    local corner = Instance.new("UICorner", frame)
    corner.CornerRadius = UDim.new(0.15, 0)
    
    local label = Instance.new("TextLabel", frame)
    label.Size = UDim2.new(1, -60, 1, 0)
    label.Position = UDim2.new(0, 15, 0, 0)
    label.BackgroundTransparency = 1
    label.Text = text
    label.TextColor3 = Color3.fromRGB(255, 255, 255)
    label.Font = Enum.Font.Gotham
    label.TextSize = 15
    label.TextXAlignment = Enum.TextXAlignment.Left
    
    local toggle = Instance.new("TextButton", frame)
    toggle.Size = UDim2.new(0, 40, 0, 25)
    toggle.Position = UDim2.new(1, -50, 0.5, -12.5)
    toggle.BackgroundColor3 = default and Color3.fromRGB(50, 255, 50) or Color3.fromRGB(100, 100, 100)
    toggle.Text = ""
    toggle.BorderSizePixel = 0
    
    local toggleCorner = Instance.new("UICorner", toggle)
    toggleCorner.CornerRadius = UDim.new(0.5, 0)
    
    local indicator = Instance.new("Frame", toggle)
    indicator.Size = UDim2.new(0, 18, 0, 18)
    indicator.Position = default and UDim2.new(1, -21, 0.5, -9) or UDim2.new(0, 3, 0.5, -9)
    indicator.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
    indicator.BorderSizePixel = 0
    
    local indicatorCorner = Instance.new("UICorner", indicator)
    indicatorCorner.CornerRadius = UDim.new(1, 0)
    
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

local function ClearContent()
    for _, child in ipairs(ContentArea:GetChildren()) do
        if not child:IsA("UIListLayout") and not child:IsA("UIPadding") then
            child:Destroy()
        end
    end
end

local function Notify(title, text)
    local notif = Instance.new("Frame", ScreenGui)
    notif.Size = UDim2.new(0, 300, 0, 80)
    notif.Position = UDim2.new(1, 320, 1, -100)
    notif.BackgroundColor3 = Color3.fromRGB(21, 51, 6)
    notif.BorderSizePixel = 0
    
    local notifCorner = Instance.new("UICorner", notif)
    notifCorner.CornerRadius = UDim.new(0, 10)
    
    local notifStroke = Instance.new("UIStroke", notif)
    notifStroke.Color = Color3.fromRGB(50, 255, 50)
    notifStroke.Thickness = 2
    
    local titleLabel = Instance.new("TextLabel", notif)
    titleLabel.Size = UDim2.new(1, -20, 0, 25)
    titleLabel.Position = UDim2.new(0, 10, 0, 5)
    titleLabel.BackgroundTransparency = 1
    titleLabel.Text = title
    titleLabel.TextColor3 = Color3.fromRGB(50, 255, 50)
    titleLabel.Font = Enum.Font.GothamBold
    titleLabel.TextSize = 16
    titleLabel.TextXAlignment = Enum.TextXAlignment.Left
    
    local textLabel = Instance.new("TextLabel", notif)
    textLabel.Size = UDim2.new(1, -20, 0, 45)
    textLabel.Position = UDim2.new(0, 10, 0, 30)
    textLabel.BackgroundTransparency = 1
    textLabel.Text = text
    textLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
    textLabel.Font = Enum.Font.Gotham
    textLabel.TextSize = 14
    textLabel.TextXAlignment = Enum.TextXAlignment.Left
    textLabel.TextWrapped = true
    
    TweenService:Create(notif, TweenInfo.new(0.5, Enum.EasingStyle.Back), {Position = UDim2.new(1, -310, 1, -100)}):Play()
    
    task.delay(3, function()
        TweenService:Create(notif, TweenInfo.new(0.5), {Position = UDim2.new(1, 320, 1, -100)}):Play()
        task.wait(0.5)
        notif:Destroy()
    end)
end

-- Variáveis Globais
_G.VixAutoExtract = false
_G.VixSpeed = false
_G.VixFullbright = false

-- Criar Tabs
local homeTab = CreateTab("🏠 Home", 1)
local playerTab = CreateTab("👤 Player", 2)
local espTab = CreateTab("👁️ ESP", 3)
local tpTab = CreateTab("🌍 Teleport", 4)
local settingsTab = CreateTab("⚙️ Settings", 5)

-- Home Tab
homeTab.MouseButton1Click:Connect(function()
    ClearContent()
    
    local welcome = Instance.new("TextLabel", ContentArea)
    welcome.Size = UDim2.new(1, -20, 0, 100)
    welcome.BackgroundTransparency = 1
    welcome.Text = "Bem-vindo ao VixDW!\n\nScript completo para Dandy's World"
    welcome.TextColor3 = Color3.fromRGB(255, 255, 255)
    welcome.Font = Enum.Font.GothamBold
    welcome.TextSize = 20
    welcome.TextWrapped = true
    
    CreateButton("✅ Auto Extract Machines", function()
        _G.VixAutoExtract = true
        Notify("Auto Extract", "Ativado!")
    end)
    
    CreateButton("❌ Stop Auto Extract", function()
        _G.VixAutoExtract = false
        Notify("Auto Extract", "Desativado!")
    end)
end)

-- Player Tab
playerTab.MouseButton1Click:Connect(function()
    ClearContent()
    
    CreateToggle("Speed Hack", false, function(enabled)
        _G.VixSpeed = enabled
        if player.Character and player.Character:FindFirstChild("Humanoid") then
            player.Character.Humanoid.WalkSpeed = enabled and 50 or 16
        end
        Notify("Speed", enabled and "Ativado!" or "Desativado!")
    end)
    
    CreateButton("Remove Fog", function()
        game.Lighting.FogEnd = 100000
        Notify("Fog", "Neblina removida!")
    end)
end)

-- ESP Tab
espTab.MouseButton1Click:Connect(function()
    ClearContent()
    
    CreateToggle("Fullbright", false, function(enabled)
        _G.VixFullbright = enabled
        game.Lighting.Brightness = enabled and 2 or 1
        game.Lighting.ClockTime = enabled and 14 or 12
        Notify("Fullbright", enabled and "Ativado!" or "Desativado!")
    end)
end)

-- Arrastar
local dragging, dragInput, dragStart, startPos

Header.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging = true
        dragStart = input.Position
        startPos = MainFrame.Position
        
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

Header.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
        dragInput = input
    end
end)

UIS.InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        local delta = input.Position - dragStart
        MainFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
    end
end)

-- Botões de Controle
OpenButton.MouseButton1Click:Connect(function()
    MainFrame.Visible = true
    OpenButton.Visible = false
    MainFrame.Size = UDim2.new(0, 0, 0, 0)
    MainFrame.Position = UDim2.new(0.5, 0, 0.5, 0)
    TweenService:Create(MainFrame, TweenInfo.new(0.4, Enum.EasingStyle.Back), {
        Size = UDim2.new(0, 850, 0, 550),
        Position = UDim2.new(0.5, -425, 0.5, -275)
    }):Play()
end)

MinimizeBtn.MouseButton1Click:Connect(function()
    TweenService:Create(MainFrame, TweenInfo.new(0.3, Enum.EasingStyle.Back), {
        Size = UDim2.new(0, 0, 0, 0),
        Position = UDim2.new(0.5, 0, 0.5, 0)
    }):Play()
    task.wait(0.3)
    MainFrame.Visible = false
    OpenButton.Visible = true
end)

-- Inicializar
Notify("VixScript", "Menu carregado!")
print("VixScript carregado! Pressione o botão 'V' verde")
