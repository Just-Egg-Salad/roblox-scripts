-- Non-Synapse Users
if not pcall(function() return syn.protect_gui end) then
    syn = {}
    syn.protect_gui = function(egg)
        egg.Parent = game.CoreGui
    end
end

-- Globals
Enabled = false
Buso = false
LastBuso = tick()
Enemy = "Thug"
Weapon = "Combat"
Distance = -9
Skills = {
    Z = false,
    X = false,
    C = false,
    V = false
}

-- Variable
local player = game.Players.LocalPlayer
local stats = player.PlayerStats
local vim = game:GetService("VirtualInputManager")
local enemies = {}
local tools = {}

-- Camera Stuff
player.DevCameraOcclusionMode = "Invisicam"

-- Grab Enemies
for i,v in pairs(workspace.Mob:GetChildren()) do
    if not table.find(enemies,v.Name) then
        table.insert(enemies,v.Name)
    end
end
for i,v in pairs(game.ReplicatedStorage.Storage:GetChildren()) do
    if v:IsA("Model") and v:FindFirstChild("Humanoid") and not table.find(enemies,v.Name) then
        table.insert(enemies,v.Name)
    end
end

-- Grab Weapons
for i,v in pairs(player.Backpack:GetChildren()) do
    table.insert(tools,v.Name)
end
local tool = player.Character:FindFirstChildOfClass("Tool")
if tool then
    table.insert(tools,tool.Name)
end

-- Quest
local quests = {
    Thug = "Chris",
    Monkey = "MonkeyQuest",
}

-- UI Library
local library = loadstring(game:HttpGetAsync('https://pastebin.com/raw/edJT9EGX'))()
local window = library:CreateWindow("cock piece 😳")
window:AddLabel({text="Made by egg salad#3112"})
window:AddToggle({text='Enabled',callback=function(a)Enabled=a;end})
window:AddList({text='Target',values=enemies,callback=function(a)Enemy=a;end})
window:AddList({text='Weapon',values=tools,callback=function(a)Weapon=a;end})
window:AddSlider({text='Distance',min=-9,max=9,callback=function(a)Distance=a;end})
local folder = window:AddFolder("Skills")
for i,v in pairs(Skills) do
    folder:AddToggle({text=i,callback=function(a)Skills[i]=a;end})
end
folder:AddToggle({text="Buso",callback=function(a)Buso=a;end})
library:Init()

-- Get Enemy
function enemy()
    if workspace.Mob:FindFirstChild(Enemy) then
        local shit = workspace.Mob:GetChildren()
        for i = 1, #shit do local v = shit[i]
            if v.Name == Enemy and v:IsA("Model") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 then
                return v
            end
        end
    end
    return game.ReplicatedStorage.Storage:FindFirstChild(Enemy)
end

-- Equip
function equip()
    local tool = player.Character and player.Character:FindFirstChildOfClass("Tool") or player:FindFirstChild("Backpack") and player.Backpack:FindFirstChild(Weapon)
    pcall(function()
        tool.Parent = player.Character
        tool:Activate()
        wait()
        tool.Script.Anim04:Destroy()
    end)
    return tool
end

-- Quest
player.PlayerGui.ChildAdded:Connect(function(v)
    wait()
    if v.Name == "Talk" and Enabled then
        game.ReplicatedStorage.Remote.Talk:FireServer(true,{Name=Enemy})
    end
end)

-- NoClip
game:GetService("RunService").Stepped:Connect(function()
    if Enabled then
        player.Character.Humanoid:ChangeState(11)
    end
end)

-- Skeet
while true do
    -- Get Enemy
    local v = enemy()
    if Enabled and typeof(v) == "Instance" then
        -- Quest Check
        if not player:FindFirstChild("Quest") or not player.Quest:FindFirstChild(Enemy) and player.Character and player.Character:FindFirstChild("HumanoidRootPart") and quests[Enemy] and workspace.NPC:FindFirstChild(quests[Enemy]) then
            game.ReplicatedStorage.Remote.Talk:FireServer(false)
            player.Character.HumanoidRootPart.CFrame = workspace.NPC[quests[Enemy]].Head.CFrame - Vector3.new(0,8,0)
            wait(.3)
            fireclickdetector(workspace.NPC[quests[Enemy]].ClickDetector, 1)
        end
        -- Kill Enemy
        repeat
            -- Teleport
            pcall(function()
                player.Character.HumanoidRootPart.CFrame = CFrame.new(v.HumanoidRootPart.Position) * CFrame.Angles(math.rad(Distance < 0 and 90 or -90), 0, 0) + Vector3.new(0, Distance, 0)
            end)
            wait()
            -- Buso
            if Buso and tick()-LastBuso > 1 and player.Character and player.Character:FindFirstChild("Buso") and not player.Character:FindFirstChild("BHaki") and player.Character.Buso.Value == player.Character.Buso.MaxValue then
                pcall(function()
                    player.Character.Move.Haki:FireServer("Buso")
                    LastBuso = tick()
                end)
            end
            -- Use Weapon
            local wep = equip()
            for i,bool in pairs(Skills) do
                if wep and bool and Enabled and wep:FindFirstChild(i) then
                    pcall(function()
                        wep[i]:FireServer(v.HumanoidRootPart.Position)
                        wait()
                        wep[i]:FireServer(v.HumanoidRootPart.Position,false)
                    end)
                end
            end
        until not Enabled or Enemy ~= v.Name or not v.Parent or not v:FindFirstChild("Humanoid") or v.Humanoid.Health <= 0
    elseif Enabled then
        pcall(function()
            player.Character.HumanoidRootPart.CFrame = CFrame.new(math.random(1000,9999),1000,math.random(1000,9999))
        end)
    end
    wait(.2)
end
