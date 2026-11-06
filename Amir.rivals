-- Servicios necesarios
local Players = game:GetService("Players")
local RunService = game:GetService("RunService")
local UserInputService = game:GetService("UserInputService")
local CoreGui = game:GetService("CoreGui")

local localPlayer = Players.LocalPlayer
local camera = workspace.CurrentCamera

-- Configuración del Aimbot
local AimbotEnabled = false -- Empieza desactivado hasta que uses el menú
local Sensitivity = 0.25 

-- Crear la Interfaz Gráfica (GUI) del Menú
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "AimbotMenu"
-- Usar CoreGui si el ejecutor lo permite, de lo contrario PlayerGui
pcall(function()
    screenGui.Parent = CoreGui
end)
if not screenGui.Parent then
    screenGui.Parent = localPlayer:WaitForChild("PlayerGui")
end

-- Botón flotante principal
local toggleButton = Instance.new("TextButton")
toggleButton.Name = "ToggleButton"
toggleButton.Parent = screenGui
toggleButton.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
toggleButton.Position = UDim2.new(0, 50, 0, 50) -- Esquina superior izquierda
toggleButton.Size = UDim2.new(0, 160, 0, 50)
toggleButton.Font = Enum.Font.SourceSansBold
toggleButton.Text = "Aimbot: OFF"
toggleButton.TextColor3 = Color3.fromRGB(255, 75, 75)
toggleButton.TextSize = 18

-- Esquinas redondeadas para que se vea mejor
local uiCorner = Instance.new("UICorner")
uiCorner.CornerRadius = UDim.new(0, 8)
uiCorner.Parent = toggleButton

-- Función para alternar el estado con el botón
toggleButton.MouseButton1Click:Connect(function()
    AimbotEnabled = not AimbotEnabled
    if AimbotEnabled then
        toggleButton.Text = "Aimbot: ON"
        toggleButton.TextColor3 = Color3.fromRGB(75, 255, 75)
        toggleButton.BackgroundColor3 = Color3.fromRGB(45, 45, 45)
    else
        toggleButton.Text = "Aimbot: OFF"
        toggleButton.TextColor3 = Color3.fromRGB(255, 75, 75)
        toggleButton.BackgroundColor3 = Color3.fromRGB(35, 35, 35)
    end
end)

-- Función para encontrar al jugador enemigo más cercano
local function getClosestPlayer()
    local closestPlayer = nil
    local shortestDistance = math.huge

    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= localPlayer and player.Character and player.Character:FindFirstChild("Humanoid") and player.Character.Humanoid.Health > 0 then
            local character = player.Character
            local head = character:FindFirstChild("Head")

            local sameTeam = false
            if localPlayer.Team and player.Team and localPlayer.Team == player.Team then
                sameTeam = true
            end

            if head and not sameTeam then
                local screenPoint, onScreen = camera:WorldToViewportPoint(head.Position)

                if onScreen then
                    local mouseLocation = UserInputService:GetMouseLocation()
