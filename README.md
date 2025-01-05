local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local ESP = {}

function ESP:CreateESP(player)
    if player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
        local highlight = Instance.new("Highlight")
        highlight.Parent = player.Character
        highlight.FillColor = Color3.new(1, 0, 0) -- Red color for ESP
        highlight.OutlineColor = Color3.new(1, 1, 1) -- White outline
        highlight.Adornee = player.Character
    end
end

-- Create ESP for existing players
for _, player in pairs(Players:GetPlayers()) do
    if player ~= LocalPlayer then
        ESP:CreateESP(player)
    end
end

-- Create ESP for players that join later
Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function()
        ESP:CreateESP(player)
    end)
end)

-- Update ESP when a player's character is added
Players.PlayerRemoving:Connect(function(player)
    if player.Character then
        local highlight = player.Character:FindFirstChildOfClass("Highlight")
        if highlight then
            highlight:Destroy()
        end
    end
end)
