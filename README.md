-- LocalScript

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")

-- Function to create a highlight for a character
local function createHighlight(character)
    -- Check if the character already has a highlight
    if not character:FindFirstChild("Highlight") then
        local highlight = Instance.new("Highlight")
        highlight.Parent = character
        highlight.FillColor = Color3.new(1, 0, 0) -- Red color
        highlight.FillTransparency = 0.5 -- 50% transparent
        highlight.OutlineColor = Color3.new(1, 1, 0) -- Yellow outline
        highlight.OutlineTransparency = 0 -- No transparency for outline
    end
end

-- Function to remove highlight from a character
local function removeHighlight(character)
    local highlight = character:FindFirstChild("Highlight")
    if highlight then
        highlight:Destroy()
    end
end

-- Function to update highlights for all players
local function updateHighlights()
    for _, player in ipairs(Players:GetPlayers()) do
        if player.Character then
            createHighlight(player.Character)
        end
    end
end

-- Connect to PlayerAdded and PlayerRemoving events
Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function(character)
        createHighlight(character)
    end)
end)

Players.PlayerRemoving:Connect(function(player)
    if player.Character then
        removeHighlight(player.Character)
    end
end)

-- Update highlights for existing players
updateHighlights()

-- Update highlights on character added
Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function(character)
        createHighlight(character)
    end)
end)

-- Update highlights on character added for existing players
for _, player in ipairs(Players:GetPlayers()) do
    if player.Character then
        createHighlight(player.Character)
    end
end
