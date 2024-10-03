-- Script para notificar quando uma fruta aparece no servidor
-- Mostra o nome da fruta e a distância em metros

local player = game.Players.LocalPlayer
local fruits = workspace:WaitForChild("Fruits")

-- Função para calcular a distância entre dois pontos
local function calculateDistance(pointA, pointB)
    return (pointA - pointB).Magnitude
end

-- Função para notificar sobre a fruta
local function notifyFruit(fruit)
    local fruitName = fruit.Name
    local distance = calculateDistance(player.Character.HumanoidRootPart.Position, fruit.Position)
    game.StarterGui:SetCore("SendNotification", {
        Title = "Fruta Apareceu!",
        Text = fruitName .. " a " .. math.floor(distance) .. " metros",
        Duration = 5
    })
end

-- Monitorar o aparecimento de frutas
fruits.ChildAdded:Connect(function(fruit)
    notifyFruit(fruit)
end)
