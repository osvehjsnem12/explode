-- Server Script
local Players = game:GetService("Players")

-- Function to cause explosions and deal damage
local function causeExplosion(executor)
    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= executor and player.Character and player.Character.PrimaryPart then
            local character = player.Character
            local humanoid = character:FindFirstChild("Humanoid")

            -- Create an explosion
            local explosion = Instance.new("Explosion")
            explosion.Position = character.PrimaryPart.Position
            explosion.BlastRadius = 10 -- Explosion radius
            explosion.BlastPressure = 500000 -- Explosion force
            explosion.Parent = workspace

            -- Apply damage
            if humanoid then
                humanoid:TakeDamage(100)
            end

            -- Remove the character
            character:BreakJoints()
        end
    end
end

-- Function to execute the command
local function executeCommand(executor)
    causeExplosion(executor)
end

-- Trigger for testing (e.g., executes under specific conditions)
game:GetService("ReplicatedStorage"):WaitForChild("TriggerExplosion").OnServerEvent:Connect(function(player)
    executeCommand(player)
end)
