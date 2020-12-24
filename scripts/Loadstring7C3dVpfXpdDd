local camera = game:GetService("Workspace").CurrentCamera
local RunService = game:GetService("RunService")
local Players = game:GetService("Players")
local LocalPlayer = game:GetService("Players").LocalPlayer
local mouse = game:GetService("Players").LocalPlayer:GetMouse()
local Paused = false

TaggedPlayers = { }
LinedPlayers = { }
PlayerNames = { }

function WorldToScreen(part, idx)
if part ~= nil then
RootPos = part.position
scr, vis = camera:WorldToScreenPoint(RootPos)
if vis then
TaggedPlayers[idx].Visible = true
LinedPlayers[idx].Visible = true
return Vector2.new(scr.x, scr.y)
else
TaggedPlayers[idx].Visible = false
LinedPlayers[idx].Visible = false
return Vector2.new(0, 0)
end
else
TaggedPlayers[idx].Visible = false
LinedPlayers[idx].Visible = false
return Vector2.new(0, 0)
end
end

local function has_value (tab, val)
   for index, value in ipairs(tab) do
       if value == val then
           return true
       end
   end
   return false
end

local function cleartb(t)
for k in pairs (t) do
t [k] = nil
end
end

local function removeESP(t)
for k in pairs (t) do
t[k].Remove(t[k])
end
end

function Init()
Paused = true
removeESP(TaggedPlayers)
removeESP(LinedPlayers)
cleartb(LinedPlayers)
cleartb(TaggedPlayers)
cleartb(PlayerNames)

   watermark = Drawing.new("Text")
watermark.Text = "Indica's ESP v1.0"
watermark.Color = Color3.new(153/255,5/255,204/255)
watermark.Position = Vector2.new(camera.ViewportSize.X - 160, camera.ViewportSize.Y - 25)
watermark.Size = 24.0
watermark.Outline = true
watermark.Visible = true
Wait(1)
Paused = false
end

function LoadESP()
for i,v in pairs(game:GetService("Players"):GetChildren()) do
if game:GetService("Workspace"):FindFirstChild(v.Name) ~= nil then
if not has_value(PlayerNames, v.Name) then
table.insert(LinedPlayers, Drawing.new("Line"))
table.insert(TaggedPlayers, Drawing.new("Text"))
table.insert(PlayerNames, v.Name)
if v.Name ~= LocalPlayer.Name then
TaggedPlayers[i].Text = v.Name
TaggedPlayers[i].Size = 14.0
TaggedPlayers[i].Color = v.TeamColor.Color
TaggedPlayers[i].Outline = true
TaggedPlayers[i].Center = true

LinedPlayers[i].Thickness = 1.6
LinedPlayers[i].Color = v.TeamColor.Color

Loc = WorldToScreen(v.Character:FindFirstChild("HumanoidRootPart"), i)

LinedPlayers[i].From = Vector2.new(camera.ViewportSize.X / 2, camera.ViewportSize.Y - 2)
LinedPlayers[i].To = Loc
TaggedPlayers[i].Position = Loc
end
else
Loc = WorldToScreen(v.Character:FindFirstChild("HumanoidRootPart"), i)
LinedPlayers[i].From = Vector2.new(camera.ViewportSize.X / 2, camera.ViewportSize.Y - 2)
LinedPlayers[i].To = Loc
TaggedPlayers[i].Position = Loc
end
end
end
end

Init()

Players.PlayerAdded:connect(function(player)
Paused = true
removeESP(TaggedPlayers)
removeESP(LinedPlayers)
cleartb(LinedPlayers)
cleartb(TaggedPlayers)
cleartb(PlayerNames)
Paused = false
end)

Players.PlayerRemoving:connect(function(player)
Paused = true
removeESP(TaggedPlayers)
removeESP(LinedPlayers)
cleartb(LinedPlayers)
cleartb(TaggedPlayers)
cleartb(PlayerNames)
Paused = false
end)

RunService.RenderStepped:connect(function()
if not Paused then
LoadESP()
end
end)