-- Globals
Size = {X=2,Y=2,Z=1}
Trans = 0
Color = Color3.new(1,0,0)

-- Variable
local size = game.StarterPlayer.StarterCharacter.Hitbox.Size

-- UI Library
local library = loadstring(game:HttpGetAsync('https://pastebin.com/raw/edJT9EGX'))()
local window = library:CreateWindow("roblox quake")
window:AddLabel({text = "Made by egg salad"})
-- Color
window:AddColor({text='Color',callback=function(a)Color=a;end})
-- Transparency
window:AddSlider({text='Transparency',min=0,max=1,float=0.01,callback=function(a)Trans=a;end})
-- Size
local sizeF = window:AddFolder("Size")
for i,v in pairs(Size) do
    sizeF:AddSlider({text=i,min=v,max=30,float=0.5,callback=function(a)Size[i]=a;end})
end
library:Init()

-- Bypass
local old;
old = hookfunction(getrawmetatable(game).__index,function(femboy,cock)
    if not checkcaller() and tostring(femboy) == "Hitbox" and cock == "Size" then
        return size
    end
    return old(femboy,cock)
end)

-- Hitbox Expander
game:GetService('RunService').RenderStepped:connect(function()
    local players = game.Players:GetPlayers()
    for i = 2, #players do local v = players[i]
        pcall(function()
            v.Character.Hitbox.Size = Vector3.new(Size.X,Size.Y,Size.Z)
            v.Character.Hitbox.CanCollide = false
            v.Character.Hitbox.Transparency = Trans
            v.Character.Hitbox.Color = Color
            v.Character.Hitbox.Material = "Neon"
            v.Character.Hitbox.Massless = true
        end)
    end
end)
