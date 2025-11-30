-- TESTE RÁPIDO - Cole APENAS este código no executor
-- NÃO use loadstring, cole DIRETO

wait(1) -- Espera o jogo carregar

print("=" .. string.rep("=", 50))
print("🔐 SPECTRAL HUB - KEY SYSTEM")
print("=" .. string.rep("=", 50))

local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local player = Players.LocalPlayer

-- Configurações
local KEY_CORRETA = "SPECTRAL2025"
local SPECTRAL_URL = "https://raw.githubusercontent.com/batata3ftt/Spectral-hub/refs/heads/main/Spectral"

-- Criar GUI
print("📋 Criando interface...")

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "SpectralKey_" .. tick()
ScreenGui.ResetOnSpawn = false

-- Tenta colocar no CoreGui, se falhar vai pro PlayerGui
pcall(function()
    ScreenGui.Parent = game:GetService("CoreGui")
end)

if not ScreenGui.Parent then
    ScreenGui.Parent = player:WaitForChild("PlayerGui")
end

print("✅ ScreenGui criado em: " .. ScreenGui.Parent.Name)

-- Frame Principal
local Frame = Instance.new("Frame")
Frame.Parent = ScreenGui
Frame.AnchorPoint = Vector2.new(0.5, 0.5)
Frame.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
Frame.BorderSizePixel = 0
Frame.Position = UDim2.new(0.5, 0, 0.5, 0)
Frame.Size = UDim2.new(0, 300, 0, 300)

local UICorner = Instance.new("UICorner")
UICorner.CornerRadius = UDim.new(0, 15)
UICorner.Parent = Frame

local Stroke = Instance.new("UIStroke")
Stroke.Parent = Frame
Stroke.Color = Color3.fromRGB(255, 0, 0)
Stroke.Thickness = 3

print("✅ Frame principal criado")

-- Título
local Title = Instance.new("TextLabel")
Title.Parent = Frame
Title.BackgroundTransparency = 1
Title.Size = UDim2.new(1, 0, 0, 50)
Title.Font = Enum.Font.GothamBold
Title.Text = "SPECTRAL HUB"
Title.TextColor3 = Color3.fromRGB(255, 0, 0)
Title.TextSize = 28

local TitleStroke = Instance.new("UIStroke")
TitleStroke.Parent = Title
TitleStroke.Color = Color3.fromRGB(200, 0, 0)
TitleStroke.Thickness = 2

-- Subtítulo
local Subtitle = Instance.new("TextLabel")
Subtitle.Parent = Frame
Subtitle.BackgroundTransparency = 1
Subtitle.Position = UDim2.new(0, 0, 0, 50)
Subtitle.Size = UDim2.new(1, 0, 0, 30)
Subtitle.Font = Enum.Font.Gotham
Subtitle.Text = "KEY SYSTEM"
Subtitle.TextColor3 = Color3.fromRGB(200, 200, 200)
Subtitle.TextSize = 14

-- Input da Key
local KeyBox = Instance.new("TextBox")
KeyBox.Parent = Frame
KeyBox.BackgroundColor3 = Color3.fromRGB(20, 0, 0)
KeyBox.BorderSizePixel = 0
KeyBox.Position = UDim2.new(0.1, 0, 0.35, 0)
KeyBox.Size = UDim2.new(0.8, 0, 0, 40)
KeyBox.Font = Enum.Font.Gotham
KeyBox.PlaceholderText = "Digite a key..."
KeyBox.PlaceholderColor3 = Color3.fromRGB(100, 100, 100)
KeyBox.Text = ""
KeyBox.TextColor3 = Color3.fromRGB(255, 255, 255)
KeyBox.TextSize = 14
KeyBox.ClearTextOnFocus = false

local KeyCorner = Instance.new("UICorner")
KeyCorner.CornerRadius = UDim.new(0, 8)
KeyCorner.Parent = KeyBox

local KeyStroke = Instance.new("UIStroke")
KeyStroke.Parent = KeyBox
KeyStroke.Color = Color3.fromRGB(255, 0, 0)
KeyStroke.Thickness = 2

-- Botão Verificar
local VerifyBtn = Instance.new("TextButton")
VerifyBtn.Parent = Frame
VerifyBtn.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
VerifyBtn.BorderSizePixel = 0
VerifyBtn.Position = UDim2.new(0.1, 0, 0.55, 0)
VerifyBtn.Size = UDim2.new(0.8, 0, 0, 40)
VerifyBtn.Font = Enum.Font.GothamBold
VerifyBtn.Text = "✓ VERIFICAR KEY"
VerifyBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
VerifyBtn.TextSize = 16

local BtnCorner = Instance.new("UICorner")
BtnCorner.CornerRadius = UDim.new(0, 8)
BtnCorner.Parent = VerifyBtn

-- Status
local Status = Instance.new("TextLabel")
Status.Parent = Frame
Status.BackgroundTransparency = 1
Status.Position = UDim2.new(0, 0, 0.75, 0)
Status.Size = UDim2.new(1, 0, 0, 30)
Status.Font = Enum.Font.GothamBold
Status.Text = ""
Status.TextColor3 = Color3.fromRGB(255, 255, 0)
Status.TextSize = 12
Status.TextTransparency = 1

-- Info
local Info = Instance.new("TextLabel")
Info.Parent = Frame
Info.BackgroundTransparency = 1
Info.Position = UDim2.new(0, 0, 0.88, 0)
Info.Size = UDim2.new(1, 0, 0, 30)
Info.Font = Enum.Font.Gotham
Info.Text = "Criado por batata3ftt"
Info.TextColor3 = Color3.fromRGB(150, 150, 150)
Info.TextSize = 10

-- Botão Fechar
local CloseBtn = Instance.new("TextButton")
CloseBtn.Parent = Frame
CloseBtn.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
CloseBtn.BorderSizePixel = 0
CloseBtn.Position = UDim2.new(1, -35, 0, 10)
CloseBtn.Size = UDim2.new(0, 25, 0, 25)
CloseBtn.Font = Enum.Font.GothamBold
CloseBtn.Text = "×"
CloseBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseBtn.TextSize = 18

local CloseCorner = Instance.new("UICorner")
CloseCorner.CornerRadius = UDim.new(1, 0)
CloseCorner.Parent = CloseBtn

print("✅ Todos os elementos criados")

-- Função de notificação
local function notify(text, color)
    Status.Text = text
    Status.TextColor3 = color
    Status.TextTransparency = 0
    task.delay(3, function()
        if Status then
            TweenService:Create(Status, TweenInfo.new(0.5), {TextTransparency = 1}):Play()
        end
    end)
end

-- Verificar Key
local function checkKey()
    local input = KeyBox.Text
    
    print("🔍 Verificando key: " .. input)
    
    if input == "" then
        notify("⚠️ Digite uma key!", Color3.fromRGB(255, 200, 0))
        return
    end
    
    if input == KEY_CORRETA then
        notify("✅ KEY CORRETA!", Color3.fromRGB(0, 255, 0))
        print("✅ Key correta! Carregando Spectral Hub...")
        
        -- Salvar key
        if writefile then
            pcall(function() writefile("SpectralKey.txt", input) end)
        end
        
        task.wait(1)
        
        -- Fechar interface
        TweenService:Create(Frame, TweenInfo.new(0.5, Enum.EasingStyle.Back, Enum.EasingDirection.In), {
            Size = UDim2.new(0, 0, 0, 0)
        }):Play()
        
        task.wait(0.6)
        ScreenGui:Destroy()
        
        -- Carregar Spectral Hub
        print("🚀 Executando Spectral Hub...")
        local success, err = pcall(function()
            loadstring(game:HttpGet(SPECTRAL_URL))()
        end)
        
        if not success then
            warn("❌ Erro: " .. tostring(err))
        else
            print("✅ Spectral Hub carregado!")
        end
    else
        notify("❌ KEY INCORRETA!", Color3.fromRGB(255, 0, 0))
        print("❌ Key incorreta!")
        
        -- Shake
        local pos = Frame.Position
        for i = 1, 5 do
            Frame.Position = UDim2.new(pos.X.Scale, pos.X.Offset + math.random(-5, 5), pos.Y.Scale, pos.Y.Offset + math.random(-5, 5))
            task.wait(0.05)
        end
        Frame.Position = pos
    end
end

-- Eventos
VerifyBtn.MouseButton1Click:Connect(checkKey)
CloseBtn.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
    print("❌ Interface fechada pelo usuário")
end)

-- REMOVIDO: Verificação automática ao pressionar Enter
-- Agora APENAS o botão verifica a key

-- Animação de entrada
Frame.Size = UDim2.new(0, 0, 0, 0)
TweenService:Create(Frame, TweenInfo.new(0.5, Enum.EasingStyle.Back, Enum.EasingDirection.Out), {
    Size = UDim2.new(0, 300, 0, 300)
}):Play()

-- Animação da borda
task.spawn(function()
    while Frame.Parent do
        TweenService:Create(Stroke, TweenInfo.new(1.5, Enum.EasingStyle.Sine), {
            Transparency = 0.3,
            Thickness = 4
        }):Play()
        task.wait(1.5)
        if not Frame.Parent then break end
        TweenService:Create(Stroke, TweenInfo.new(1.5, Enum.EasingStyle.Sine), {
            Transparency = 0,
            Thickness = 3
        }):Play()
        task.wait(1.5)
    end
end)

print("=" .. string.rep("=", 50))
print("✅ INTERFACE CARREGADA COM SUCESSO!")
print("🔑 Key: " .. KEY_CORRETA)
print("=" .. string.rep("=", 50))
