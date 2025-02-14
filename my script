local player = game.Players.LocalPlayer
local character = player.Character or player.CharacterAdded:Wait()
local hrp = character:WaitForChild("HumanoidRootPart")
local distance = 60
local orbitSpeed = 4
local RunService = game:GetService("RunService")

local function isValidObject(obj)
    return obj:IsA("BasePart") and not obj.Anchored and not obj:IsDescendantOf(character) and not obj.Parent:FindFirstChildOfClass("Humanoid")
end

local function orbitObject(obj)
    local bp = Instance.new("BodyPosition", obj)
    bp.MaxForce = Vector3.new(1e9, 1e9, 1e9)
    bp.P = 1e7
    local angle = math.random() * math.pi * 2
    local connection
    connection = RunService.Stepped:Connect(function(_, dt)
        angle = angle + dt * orbitSpeed
        local targetPosition = hrp.Position + Vector3.new(math.cos(angle) * distance, 0, math.sin(angle) * distance)
        bp.Position = targetPosition
        if not hrp or not hrp.Parent or not obj or not obj.Parent then
            connection:Disconnect()
        end
    end)
end

for _, obj in pairs(workspace:GetDescendants()) do
    if isValidObject(obj) then
        orbitObject(obj)
    end
end
