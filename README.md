
-- ═══════════════════════════════════════════════════════════
--     BATATA HUB - SISTEMA DE KEY PREMIUM v2.3
--     Criado por: batata
-- ═══════════════════════════════════════════════════════════

wait(0.5)

-- ════════════════ SERVIÇOS ════════════════
local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local player = Players.LocalPlayer

-- ════════════════ CONFIGURAÇÕES ════════════════
local CONFIG = {
    KEY = "BATATA2025",
    HUB_URL = "https://raw.githubusercontent.com/batata3ftt/script-completo-04-12-2025/refs/heads/main/Script%20sem%20key",
    
    -- ⚠️ IDs DAS IMAGENS ⚠️
    BACKGROUND_IMAGE = "rbxassetid://140370248943220",
    LOGO_IMAGE = "rbxassetid://133584317870203", -- ← NOVO CADEADO
    DISCORD_ICON = "rbxassetid://95649005720075",
    
    DISCORD_USERNAME = "hunter.exe7133",
    
    -- Cores do tema azul
    COLORS = {
        Primary = Color3.fromRGB(0, 122, 255),
        Secondary = Color3.fromRGB(10, 132, 255),
        Background = Color3.fromRGB(15, 15, 20),
        Surface = Color3.fromRGB(25, 25, 35),
        Text = Color3.fromRGB(255, 255, 255),
        TextSecondary = Color3.fromRGB(160, 160, 180),
        Success = Color3.fromRGB(52, 211, 153),
        Error = Color3.fromRGB(239, 68, 68),
        Warning = Color3.fromRGB(251, 191, 36),
        Discord = Color3.fromRGB(88, 101, 242),
    }
}

-- ════════════════ CRIAR SCREEN GUI ════════════════
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "BatataKeySystem_" .. tick()
ScreenGui.ResetOnSpawn = false
ScreenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling

pcall(function()
    ScreenGui.Parent = game:GetService("CoreGui")
end)

if not ScreenGui.Parent then
    ScreenGui.Parent = player:WaitForChild("PlayerGui")
end

-- ════════════════ BLUR DE FUNDO ════════════════
local Blur = Instance.new("BlurEffect")
Blur.Parent = game:GetService("Lighting")
Blur.Size = 0
TweenService:Create(Blur, TweenInfo.new(0.5), {Size = 15}):Play()

-- ════════════════ FRAME PRINCIPAL (MENOR) ════════════════
local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.Parent = ScreenGui
MainFrame.AnchorPoint = Vector2.new(0.5, 0.5)
MainFrame.BackgroundColor3 = CONFIG.COLORS.Background
MainFrame.BorderSizePixel = 0
MainFrame.Position = UDim2.new(0.5, 0, 0.5, 0)
MainFrame.Size = UDim2.new(0, 320, 0, 380) -- MENOR: 320x380
MainFrame.ClipsDescendants = true

local MainCorner = Instance.new("UICorner")
MainCorner.CornerRadius = UDim.new(0, 16)
MainCorner.Parent = MainFrame

-- Borda animada
local BorderGradient = Instance.new("UIStroke")
BorderGradient.Parent = MainFrame
BorderGradient.Thickness = 2.5
BorderGradient.Color = CONFIG.COLORS.Primary

local GradientColor = Instance.new("UIGradient")
GradientColor.Parent = BorderGradient
GradientColor.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, CONFIG.COLORS.Primary),
    ColorSequenceKeypoint.new(0.5, CONFIG.COLORS.Secondary),
    ColorSequenceKeypoint.new(1, CONFIG.COLORS.Primary),
}

task.spawn(function()
    while MainFrame.Parent do
        TweenService:Create(GradientColor, TweenInfo.new(3, Enum.EasingStyle.Linear), {Rotation = 360}):Play()
        task.wait(3)
        GradientColor.Rotation = 0
    end
end)

-- ════════════════ IMAGEM DE FUNDO ════════════════
local BackgroundImage = Instance.new("ImageLabel")
BackgroundImage.Parent = MainFrame
BackgroundImage.BackgroundTransparency = 1
BackgroundImage.Size = UDim2.new(1, 0, 1, 0)
BackgroundImage.Image = CONFIG.BACKGROUND_IMAGE
BackgroundImage.ImageTransparency = 0.85
BackgroundImage.ScaleType = Enum.ScaleType.Crop
BackgroundImage.ZIndex = 1

local BgCorner = Instance.new("UICorner")
BgCorner.CornerRadius = UDim.new(0, 16)
BgCorner.Parent = BackgroundImage

-- Overlay escuro
local Overlay = Instance.new("Frame")
Overlay.Parent = MainFrame
Overlay.BackgroundColor3 = CONFIG.COLORS.Background
Overlay.BackgroundTransparency = 0.3
Overlay.Size = UDim2.new(1, 0, 1, 0)
Overlay.ZIndex = 2

local OverlayCorner = Instance.new("UICorner")
OverlayCorner.CornerRadius = UDim.new(0, 16)
OverlayCorner.Parent = Overlay

-- ════════════════ CONTAINER DE CONTEÚDO ════════════════
local ContentFrame = Instance.new("Frame")
ContentFrame.Parent = MainFrame
ContentFrame.BackgroundTransparency = 1
ContentFrame.Position = UDim2.new(0, 20, 0, 20)
ContentFrame.Size = UDim2.new(1, -40, 1, -40)
ContentFrame.ZIndex = 3

-- ════════════════ LOGO 3D (CADEADO NOVO) ════════════════
local LogoFrame = Instance.new("Frame")
LogoFrame.Parent = ContentFrame
LogoFrame.AnchorPoint = Vector2.new(0.5, 0)
LogoFrame.BackgroundColor3 = CONFIG.COLORS.Primary
LogoFrame.BackgroundTransparency = 0.95
LogoFrame.Position = UDim2.new(0.5, 0, 0, 0)
LogoFrame.Size = UDim2.new(0, 60, 0, 60)

local LogoCorner = Instance.new("UICorner")
LogoCorner.CornerRadius = UDim.new(1, 0)
LogoCorner.Parent = LogoFrame

local LogoStroke = Instance.new("UIStroke")
LogoStroke.Parent = LogoFrame
LogoStroke.Color = CONFIG.COLORS.Primary
LogoStroke.Thickness = 2.5

local LogoImage = Instance.new("ImageLabel")
LogoImage.Parent = LogoFrame
LogoImage.BackgroundTransparency = 1
LogoImage.Size = UDim2.new(0.7, 0, 0.7, 0)
LogoImage.Position = UDim2.new(0.15, 0, 0.15, 0)
LogoImage.Image = CONFIG.LOGO_IMAGE
LogoImage.ScaleType = Enum.ScaleType.Fit

-- ════════════════ TÍTULO ════════════════
local Title = Instance.new("TextLabel")
Title.Parent = ContentFrame
Title.BackgroundTransparency = 1
Title.Position = UDim2.new(0, 0, 0, 70)
Title.Size = UDim2.new(1, 0, 0, 26)
Title.Font = Enum.Font.GothamBold
Title.Text = "BATATA HUB"
Title.TextColor3 = CONFIG.COLORS.Text
Title.TextSize = 22

local TitleGradient = Instance.new("UIGradient")
TitleGradient.Parent = Title
TitleGradient.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, CONFIG.COLORS.Primary),
    ColorSequenceKeypoint.new(0.5, CONFIG.COLORS.Secondary),
    ColorSequenceKeypoint.new(1, CONFIG.COLORS.Primary),
}
TitleGradient.Rotation = 45

-- ════════════════ SUBTÍTULO ════════════════
local Subtitle = Instance.new("TextLabel")
Subtitle.Parent = ContentFrame
Subtitle.BackgroundTransparency = 1
Subtitle.Position = UDim2.new(0, 0, 0, 96)
Subtitle.Size = UDim2.new(1, 0, 0, 14)
Subtitle.Font = Enum.Font.Gotham
Subtitle.Text = "Sistema de Autenticação"
Subtitle.TextColor3 = CONFIG.COLORS.TextSecondary
Subtitle.TextSize = 9

-- ════════════════ DIVISOR ════════════════
local Divider = Instance.new("Frame")
Divider.Parent = ContentFrame
Divider.BackgroundColor3 = CONFIG.COLORS.Primary
Divider.BackgroundTransparency = 0.7
Divider.BorderSizePixel = 0
Divider.Position = UDim2.new(0.25, 0, 0, 118)
Divider.Size = UDim2.new(0.5, 0, 0, 2)

-- ════════════════ LABEL DO INPUT ════════════════
local InputLabel = Instance.new("TextLabel")
InputLabel.Parent = ContentFrame
InputLabel.BackgroundTransparency = 1
InputLabel.Position = UDim2.new(0, 0, 0, 130)
InputLabel.Size = UDim2.new(1, 0, 0, 12)
InputLabel.Font = Enum.Font.GothamBold
InputLabel.Text = "DIGITE SUA KEY"
InputLabel.TextColor3 = CONFIG.COLORS.Text
InputLabel.TextSize = 9
InputLabel.TextXAlignment = Enum.TextXAlignment.Left

-- ════════════════ INPUT DA KEY ════════════════
local InputFrame = Instance.new("Frame")
InputFrame.Parent = ContentFrame
InputFrame.BackgroundColor3 = CONFIG.COLORS.Surface
InputFrame.BorderSizePixel = 0
InputFrame.Position = UDim2.new(0, 0, 0, 148)
InputFrame.Size = UDim2.new(1, 0, 0, 38)

local InputCorner = Instance.new("UICorner")
InputCorner.CornerRadius = UDim.new(0, 10)
InputCorner.Parent = InputFrame

local InputStroke = Instance.new("UIStroke")
InputStroke.Parent = InputFrame
InputStroke.Color = CONFIG.COLORS.Primary
InputStroke.Thickness = 2
InputStroke.Transparency = 0.5

local InputIcon = Instance.new("TextLabel")
InputIcon.Parent = InputFrame
InputIcon.BackgroundTransparency = 1
InputIcon.Position = UDim2.new(0, 8, 0, 0)
InputIcon.Size = UDim2.new(0, 22, 1, 0)
InputIcon.Font = Enum.Font.GothamBold
InputIcon.Text = "🔑"
InputIcon.TextColor3 = CONFIG.COLORS.Primary
InputIcon.TextSize = 13

local KeyInput = Instance.new("TextBox")
KeyInput.Parent = InputFrame
KeyInput.BackgroundTransparency = 1
KeyInput.Position = UDim2.new(0, 34, 0, 0)
KeyInput.Size = UDim2.new(1, -40, 1, 0)
KeyInput.Font = Enum.Font.Gotham
KeyInput.PlaceholderText = "Insira sua key aqui..."
KeyInput.PlaceholderColor3 = CONFIG.COLORS.TextSecondary
KeyInput.Text = ""
KeyInput.TextColor3 = CONFIG.COLORS.Text
KeyInput.TextSize = 11
KeyInput.TextXAlignment = Enum.TextXAlignment.Left
KeyInput.ClearTextOnFocus = false

-- ════════════════ BOTÃO VERIFICAR ════════════════
local VerifyButton = Instance.new("TextButton")
VerifyButton.Parent = ContentFrame
VerifyButton.BackgroundColor3 = CONFIG.COLORS.Primary
VerifyButton.BorderSizePixel = 0
VerifyButton.Position = UDim2.new(0, 0, 0, 198)
VerifyButton.Size = UDim2.new(1, 0, 0, 38)
VerifyButton.AutoButtonColor = false
VerifyButton.Font = Enum.Font.GothamBold
VerifyButton.Text = "VERIFICAR KEY"
VerifyButton.TextColor3 = Color3.fromRGB(255, 255, 255)
VerifyButton.TextSize = 12

local ButtonCorner = Instance.new("UICorner")
ButtonCorner.CornerRadius = UDim.new(0, 10)
ButtonCorner.Parent = VerifyButton

local ButtonGradient = Instance.new("UIGradient")
ButtonGradient.Parent = VerifyButton
ButtonGradient.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, CONFIG.COLORS.Primary),
    ColorSequenceKeypoint.new(1, CONFIG.COLORS.Secondary),
}
ButtonGradient.Rotation = 45

-- ════════════════ BOTÃO GET DISCORD (EMBAIXO) ════════════════
local DiscordButton = Instance.new("TextButton")
DiscordButton.Parent = ContentFrame
DiscordButton.BackgroundColor3 = CONFIG.COLORS.Discord
DiscordButton.BorderSizePixel = 0
DiscordButton.Position = UDim2.new(0, 0, 0, 244) -- LOGO EMBAIXO
DiscordButton.Size = UDim2.new(1, 0, 0, 38)
DiscordButton.AutoButtonColor = false
DiscordButton.Font = Enum.Font.GothamBold
DiscordButton.Text = ""
DiscordButton.TextSize = 12

local DiscordCorner = Instance.new("UICorner")
DiscordCorner.CornerRadius = UDim.new(0, 10)
DiscordCorner.Parent = DiscordButton

local DiscordImage = Instance.new("ImageLabel")
DiscordImage.Parent = DiscordButton
DiscordImage.BackgroundTransparency = 1
DiscordImage.Position = UDim2.new(0, 8, 0.5, -9)
DiscordImage.Size = UDim2.new(0, 18, 0, 18)
DiscordImage.Image = CONFIG.DISCORD_ICON
DiscordImage.ScaleType = Enum.ScaleType.Fit

local DiscordText = Instance.new("TextLabel")
DiscordText.Parent = DiscordButton
DiscordText.BackgroundTransparency = 1
DiscordText.Position = UDim2.new(0, 32, 0, 0)
DiscordText.Size = UDim2.new(1, -38, 1, 0)
DiscordText.Font = Enum.Font.GothamBold
DiscordText.Text = "GET DISCORD"
DiscordText.TextColor3 = Color3.fromRGB(255, 255, 255)
DiscordText.TextSize = 12
DiscordText.TextXAlignment = Enum.TextXAlignment.Left

-- ════════════════ STATUS ════════════════
local StatusLabel = Instance.new("TextLabel")
StatusLabel.Parent = ContentFrame
StatusLabel.BackgroundTransparency = 1
StatusLabel.Position = UDim2.new(0, 0, 0, 290)
StatusLabel.Size = UDim2.new(1, 0, 0, 22)
StatusLabel.Font = Enum.Font.GothamBold
StatusLabel.Text = ""
StatusLabel.TextColor3 = CONFIG.COLORS.Warning
StatusLabel.TextSize = 10
StatusLabel.TextTransparency = 1

-- ════════════════ FOOTER ════════════════
local Footer = Instance.new("TextLabel")
Footer.Parent = ContentFrame
Footer.BackgroundTransparency = 1
Footer.Position = UDim2.new(0, 0, 1, -18)
Footer.Size = UDim2.new(1, 0, 0, 18)
Footer.Font = Enum.Font.Gotham
Footer.Text = "Criado por batata • v2.3"
Footer.TextColor3 = CONFIG.COLORS.TextSecondary
Footer.TextSize = 8
Footer.TextTransparency = 0.5

-- ════════════════ BOTÃO X (SUPERIOR DIREITO) ════════════════
local CloseButton = Instance.new("TextButton")
CloseButton.Parent = MainFrame
CloseButton.AnchorPoint = Vector2.new(1, 0)
CloseButton.BackgroundColor3 = CONFIG.COLORS.Error
CloseButton.BackgroundTransparency = 0.7
CloseButton.BorderSizePixel = 0
CloseButton.Position = UDim2.new(1, -8, 0, 8)
CloseButton.Size = UDim2.new(0, 24, 0, 24)
CloseButton.AutoButtonColor = false
CloseButton.Font = Enum.Font.GothamBold
CloseButton.Text = "✕"
CloseButton.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseButton.TextSize = 15
CloseButton.ZIndex = 10

local CloseCorner = Instance.new("UICorner")
CloseCorner.CornerRadius = UDim.new(1, 0)
CloseCorner.Parent = CloseButton

local CloseStroke = Instance.new("UIStroke")
CloseStroke.Parent = CloseButton
CloseStroke.Color = CONFIG.COLORS.Error
CloseStroke.Thickness = 1.5

-- ════════════════ FUNÇÕES ════════════════

local function showNotification(text, color, icon)
    StatusLabel.Text = icon .. " " .. text
    StatusLabel.TextColor3 = color
    StatusLabel.TextTransparency = 0
    
    TweenService:Create(StatusLabel, TweenInfo.new(0.3), {TextTransparency = 0}):Play()
    
    task.delay(3, function()
        TweenService:Create(StatusLabel, TweenInfo.new(0.5), {TextTransparency = 1}):Play()
    end)
end

local function shakeFrame(frame)
    local originalPos = frame.Position
    for i = 1, 8 do
        frame.Position = UDim2.new(
            originalPos.X.Scale, originalPos.X.Offset + math.random(-8, 8),
            originalPos.Y.Scale, originalPos.Y.Offset + math.random(-8, 8)
        )
        task.wait(0.04)
    end
    frame.Position = originalPos
end

local function verifyKey()
    local enteredKey = KeyInput.Text
    
    if enteredKey == "" then
        showNotification("Digite uma key!", CONFIG.COLORS.Warning, "⚠️")
        shakeFrame(InputFrame)
        return
    end
    
    VerifyButton.Text = "VERIFICANDO..."
    VerifyButton.BackgroundColor3 = CONFIG.COLORS.Secondary
    
    task.wait(0.8)
    
    if enteredKey == CONFIG.KEY then
        showNotification("Key verificada!", CONFIG.COLORS.Success, "✓")
        VerifyButton.Text = "✓ VERIFICADO"
        VerifyButton.BackgroundColor3 = CONFIG.COLORS.Success
        
        if writefile then 
            pcall(function() 
                writefile("BatataKey.txt", enteredKey) 
            end) 
        end
        
        task.wait(1)
        
        TweenService:Create(MainFrame, TweenInfo.new(0.5, Enum.EasingStyle.Back, Enum.EasingDirection.In), {
            Size = UDim2.new(0, 0, 0, 0),
            Rotation = 180
        }):Play()
        
        TweenService:Create(Blur, TweenInfo.new(0.5), {Size = 0}):Play()
        
        task.wait(0.6)
        ScreenGui:Destroy()
        Blur:Destroy()
        
        loadstring(game:HttpGet(CONFIG.HUB_URL))()
    else
        showNotification("Key incorreta!", CONFIG.COLORS.Error, "✕")
        VerifyButton.Text = "VERIFICAR KEY"
        VerifyButton.BackgroundColor3 = CONFIG.COLORS.Primary
        KeyInput.Text = ""
        shakeFrame(MainFrame)
    end
end

local function copyDiscord()
    if setclipboard then
        setclipboard(CONFIG.DISCORD_USERNAME)
        showNotification("Discord copiado!", CONFIG.COLORS.Success, "✓")
        
        DiscordButton.BackgroundColor3 = CONFIG.COLORS.Success
        DiscordText.Text = "✓ COPIADO!"
        
        task.wait(1.5)
        
        DiscordButton.BackgroundColor3 = CONFIG.COLORS.Discord
        DiscordText.Text = "GET DISCORD"
    else
        showNotification("Executor não suporta clipboard!", CONFIG.COLORS.Error, "✕")
    end
end

-- ════════════════ EVENTOS ════════════════

VerifyButton.MouseButton1Click:Connect(verifyKey)
DiscordButton.MouseButton1Click:Connect(copyDiscord)

KeyInput.FocusLost:Connect(function(enterPressed)
    if enterPressed then
        verifyKey()
    end
end)

CloseButton.MouseButton1Click:Connect(function()
    TweenService:Create(MainFrame, TweenInfo.new(0.3), {Size = UDim2.new(0, 0, 0, 0)}):Play()
    TweenService:Create(Blur, TweenInfo.new(0.3), {Size = 0}):Play()
    task.wait(0.4)
    ScreenGui:Destroy()
    Blur:Destroy()
end)

-- ════════════════ HOVER EFFECTS ════════════════

VerifyButton.MouseEnter:Connect(function()
    TweenService:Create(VerifyButton, TweenInfo.new(0.2), {
        Size = UDim2.new(1, 0, 0, 42),
        BackgroundColor3 = CONFIG.COLORS.Secondary
    }):Play()
end)

VerifyButton.MouseLeave:Connect(function()
    TweenService:Create(VerifyButton, TweenInfo.new(0.2), {
        Size = UDim2.new(1, 0, 0, 38),
        BackgroundColor3 = CONFIG.COLORS.Primary
    }):Play()
end)

DiscordButton.MouseEnter:Connect(function()
    TweenService:Create(DiscordButton, TweenInfo.new(0.2), {
        Size = UDim2.new(1, 0, 0, 42),
        BackgroundColor3 = Color3.fromRGB(78, 91, 222)
    }):Play()
end)

DiscordButton.MouseLeave:Connect(function()
    TweenService:Create(DiscordButton, TweenInfo.new(0.2), {
        Size = UDim2.new(1, 0, 0, 38),
        BackgroundColor3 = CONFIG.COLORS.Discord
    }):Play()
end)

CloseButton.MouseEnter:Connect(function()
    TweenService:Create(CloseButton, TweenInfo.new(0.2), {
        BackgroundTransparency = 0.1,
        Size = UDim2.new(0, 26, 0, 26)
    }):Play()
end)

CloseButton.MouseLeave:Connect(function()
    TweenService:Create(CloseButton, TweenInfo.new(0.2), {
        BackgroundTransparency = 0.7,
        Size = UDim2.new(0, 24, 0, 24)
    }):Play()
end)

InputFrame.MouseEnter:Connect(function()
    TweenService:Create(InputStroke, TweenInfo.new(0.2), {
        Transparency = 0,
        Thickness = 3
    }):Play()
end)

InputFrame.MouseLeave:Connect(function()
    TweenService:Create(InputStroke, TweenInfo.new(0.2), {
        Transparency = 0.5,
        Thickness = 2
    }):Play()
end)

-- ════════════════ ANIMAÇÃO DE ENTRADA ════════════════

MainFrame.Size = UDim2.new(0, 0, 0, 0)
MainFrame.Rotation = -180

TweenService:Create(MainFrame, TweenInfo.new(0.7, Enum.EasingStyle.Back, Enum.EasingDirection.Out), {
    Size = UDim2.new(0, 320, 0, 380),
    Rotation = 0
}):Play()

-- Fade-in dos elementos
for _, element in pairs(ContentFrame:GetChildren()) do
    if element:IsA("GuiObject") then
        element.BackgroundTransparency = 1
        if element:IsA("TextLabel") or element:IsA("TextButton") or element:IsA("TextBox") then
            element.TextTransparency = 1
        end
    end
end

task.wait(0.3)

for i, element in pairs(ContentFrame:GetChildren()) do
    if element:IsA("GuiObject") then
        task.spawn(function()
            TweenService:Create(element, TweenInfo.new(0.5, Enum.EasingStyle.Quad, Enum.EasingDirection.Out), {
                BackgroundTransparency = element.Name == "InputFrame" and 0 or 1
            }):Play()
            
            if element:IsA("TextLabel") or element:IsA("TextButton") then
                TweenService:Create(element, TweenInfo.new(0.5), {
                    TextTransparency = element.Name == "Footer" and 0.5 or 0
                }):Play()
            end
        end)
        task.wait(0.05)
    end
end

-- ════════════════ ANIMAÇÃO 3D DO CADEADO ════════════════

task.spawn(function()
    while LogoFrame.Parent do
        -- Rotação 360°
        TweenService:Create(LogoFrame, TweenInfo.new(2.5, Enum.EasingStyle.Linear), {
            Rotation = 360
        }):Play()
        
        -- Efeito 3D (zoom in/out)
        TweenService:Create(LogoImage, TweenInfo.new(1.25, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), {
            Size = UDim2.new(0.8, 0, 0.8, 0),
            Position = UDim2.new(0.1, 0, 0.1, 0)
        }):Play()
        
        task.wait(1.25)
        
        TweenService:Create(LogoImage, TweenInfo.new(1.25, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), {
            Size = UDim2.new(0.7, 0, 0.7, 0),
            Position = UDim2.new(0.15, 0, 0.15, 0)
        }):Play()
        
        task.wait(1.25)
        LogoFrame.Rotation = 0
    end
end)

print("✅ BATATA HUB Key System v2.3 carregado!")
print("🔑 Key: " .. CONFIG.KEY)
print("💬 Discord: " .. CONFIG.DISCORD_USERNAME)
