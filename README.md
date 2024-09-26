print("Excute")
repeat wait() until game:IsLoaded()
if game.GameId ~= 994732206 then return end

if syn then
	Request_Var = syn.request
else
    Request_Var = request 
end

print("Loading Function")

local res = Request_Var({
    Url = "https://httpbin.org/get",
    Method = "GET"
}).Body;

function Current_Exploit(Exploit)
    local decode = game:GetService('HttpService'):JSONDecode(res)
    if decode.headers['User-Agent'] == Exploit then
        return true
    end
end

-- do -- Crypt
--     base64 = {}
--     function CustomCrypt(t)
--         old = 0 
--         out = {}
--         for a = 1, #(t) do  
--             local byt = string.byte(string.sub(t, a,a))
--             local new = (byt+old)%256
--             if a == 13 then
--                 new2 = 10 ^ (math.abs(new))
--             else
--                 new2 = 10 ^ (math.abs(new)-0xf)
--             end
--             out[a] = new2 + 0x10105
--             old = byt
--         end 
--         return out
--     end
--     function deCustomCrypt(t)
--         local txt = ""
--         local old = 0
--         for i=1,#t do
--             local new2 = t[i] - 0x10105
--             new2 = math.log10(math.abs(new2))
--             local new = (new2-old) % 256 + (i ~= 13 and 0xf or 0)
--             old = new
--             txt = txt .. string.char(new)
--         end
--         return txt
--     end
--     base64.enc = function(data)
--         if not data then return end
--         local b='ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/'
--         return table.concat(CustomCrypt((data:gsub('.', function(x) 
--             local r,b='',x:byte()
--             for i=8,1,-1 do r=r..(b%2^i-b%2^(i-1)>0 and '1' or '0') end
--             return r;
--         end)..'0000'):gsub('%d%d%d?%d?%d?%d?', function(x)
--             if (#x < 6) then return '' end
--             local c=0
--             for i=1,6 do c=c+(x:sub(i,i)=='1' and 2^(6-i) or 0) end
--             return b:sub(c+1,c+1)
--         end)..({ '', '==', '=' })[#data%3+1]),"!")
--     end
--     base64.dec = function(data)
--         if not data then return end
--         local b='ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/'
--         data = string.gsub(deCustomCrypt(data:split("!")), '[^'..b..'=]', '')
--         return (data:gsub('.', function(x)
--             if (x == '=') then return '' end
--             local r,f='',(b:find(x)-1)
--             for i=6,1,-1 do r=r..(f%2^i-f%2^(i-1)>0 and '1' or '0') end
--             return r;
--         end):gsub('%d%d%d?%d?%d?%d?%d?%d?', function(x)
--             if (#x ~= 8) then return '' end
--             local c=0
--             for i=1,8 do c=c+(x:sub(i,i)=='1' and 2^(8-i) or 0) end
--             return string.char(c)
--         end))
--     end
-- end
--[[
-- Package Utilities
tickToDate = function(time)
    local date =  os.date("%Y-%m-%d-%H-%M-%S",time or tick()):split("-")
    for i,v in pairs(date) do
        date[i] = tonumber(v)
    end
    return unpack(date)
end

Utilities = {
    Priority = isfile("Unique Hub File/LocalPriority") and base64.dec(readfile("Unique Hub File/LocalPriority")) or game:HttpGet('https://raw.githubusercontent.com/hajibeza/File/main/Priority.lua');
    Network = isfile("Unique Hub File/LocalNetwork") and base64.dec(readfile("Unique Hub File/LocalNetwork")) or game:HttpGet('https://raw.githubusercontent.com/hajibeza/File/main/Network.lua');
}

for i,v in pairs(Utilities) do
    -- writefile("Unique Hub File/"..i..".dat",base64.enc(v))
    Utilities[i] = loadstring(v)()
end
]]
Players = game.Players
repeat 
    Client = Players.LocalPlayer
    wait()
until Client

do -- Init Script
    local start = Client.PlayerGui:WaitForChild("Main"):WaitForChild("Loading") and tick()
    local Version = Client.PlayerGui:WaitForChild("Main"):WaitForChild("Version"):WaitForChild("Script").Parent
    repeat wait() until Version.Text:find("Version")

    -- Checking is game glitch
    repeat
        wait()
        if tick() - start > 10 then
            game:GetService("TeleportService"):Teleport(game.PlaceId)
            break
        end
    until not Client.PlayerGui:WaitForChild("Main"):WaitForChild("Loading").Visible
    local Success,Result = pcall(require,Client.PlayerScripts.CombatFramework.RigController)
    if not Success then return game:GetService("TeleportService"):Teleport(game.PlaceId) end

    -- Supporting Arceus
    local _env = getgenv()
    _env.getconstant = debug.getconstant
    _env.getconstants = debug.getconstants
    _env.getupvalue = debug.getupvalue
    _env.getupvalues = debug.getupvalues
    _env.getgc = _env.getgc or debug.getregistry

    FormatEnemyName = function(name)
        local strings = name:split(" ")
        for i = #strings,1,-1 do
            if strings[i]:sub(1,1) == "[" then
                table.remove(strings,i)
                table.remove(strings,i)
            end
        end
        return table.concat(strings," ")
    end

    -- Noclip

    if not IsValyse then
        setfflag("HumanoidParallelRemoveNoPhysics", "False")
        setfflag("HumanoidParallelRemoveNoPhysicsNoSimulate2", "False")
    end
end

do -- table
    setreadonly(table,false)
    table.new = function(t)
        return setmetatable(t or {},{__index=table})
    end
    table.combine = function(...)
        local list = {...}
        local new = {}
        for i=1,#list do
            table.move(list[i], 1, #list[i], #new+1, new)
        end
        return new
    end
    table.toString = convert
    setreadonly(table,true)
    CanTeleport = {
        {
            ["Sky3"] = Vector3.new(-7894, 5547, -380),
            ["Sky3Exit"] = Vector3.new(-4607, 874, -1667),
            ["UnderWater"] = Vector3.new(61163, 11, 1819),
            ["UnderwaterExit"] = Vector3.new(4050, -1, -1814),
        },
        {
            ["Swan Mansion"] = Vector3.new(-390, 332, 673),
            ["Swan Room"] = Vector3.new(2285, 15, 905),
            ["Cursed Ship"] = Vector3.new(923, 126, 32852),
        },
        {
            ["Floating Turtle"] = Vector3.new(-12462, 375, -7552),
            ["Hydra Island"] = Vector3.new(5745, 610, -267),
            ["Mansion"] = Vector3.new(-12462, 375, -7552),
            ["Castle"] = Vector3.new(-5036, 315, -3179),
        }
    }
    Step = {
        Vector3.new(0,60,0),
        Vector3.new(0,0,60),
        Vector3.new(0,0,-60),
        Vector3.new(60,0,0),
        Vector3.new(-60,0,0),
        Vector3.new(0,-60,0),
    }
    Chest = {}
    MasteryData = {}
    CollectedFruit = {}
    ItemsData = {
        Sword = {},
        Material = {},
    }
    Finished = {}
    MeleeCanSkip = setmetatable({},{
        __index = function(t,k)
            return Finished[k] or not Settings[k]
        end,
    })
end

do -- Team Script
    repeat 
        ChooseTeam = game:GetService("Players").LocalPlayer.PlayerGui:FindFirstChild("ChooseTeam",true)
        UIController = game:GetService("Players").LocalPlayer.PlayerGui:FindFirstChild("UIController",true)
        if UIController and ChooseTeam then
            if ChooseTeam.Visible then
                for i,v in pairs(getgc()) do
                    if type(v) == "function" and getfenv(v).script == UIController then
                        local constant = getconstants(v)
                        pcall(function()
                            if constant[1] == "Pirates" and #constant == 1 then
                                v(shared.Team or "Pirates")
                            end
                        end)
                    end
                end
            end
        end
        wait(1)
    until game.Players.LocalPlayer.Team
    repeat wait() until Client.Character
    -- Loading Drawing Library
end

do -- Instance
    Map = workspace:WaitForChild("Map")
    MainUI = Client.PlayerGui:WaitForChild("Main")
    WorldData = workspace._WorldOrigin
    Locations = WorldData.Locations
    Char = Client.Character
    Backpack = Client.Backpack
    ClientData = Client.Data
end

do -- Services
    UserInputService = game:GetService("UserInputService")
    RunService = game:GetService("RunService")
    vim = game:GetService('VirtualInputManager')
    CollectionService = game:GetService("CollectionService")
    CoreGui = game:GetService("CoreGui")
end

do -- Module Requiring
    Util = require(game:GetService("ReplicatedStorage").Util)
    Quest = require(game:GetService("ReplicatedStorage").Quests)
    Queue = require(game:GetService("ReplicatedStorage").Queue)
    dialogues = require(game:GetService("ReplicatedStorage").DialoguesList)
    -- CameraShaker = require(Client.PlayerScripts.CombatFramework.CameraShaker.CameraShakeInstance)
    PC = require(Client.PlayerScripts.CombatFramework.Particle)
    RL = require(game:GetService("ReplicatedStorage").CombatFramework.RigLib)
    Noti = require(game:GetService("ReplicatedStorage").Notification)
    DMG = require(Client.PlayerScripts.CombatFramework.Particle.Damage)
    Guide = require(game:GetService("ReplicatedStorage").GuideModule)
    AllRaidShip = require(game:GetService("ReplicatedStorage").Raids)
    Exp_Calc = require(game.ReplicatedStorage.EXPFunction)
    Inv = require(MainUI.UIController.Inventory)
    Sprite = require(MainUI.UIController.Inventory.Spritesheets)
    itemList = getupvalue(Inv.UpdateSort,2)
    tier = getupvalue(Inv.UpdateSelected,7)
    RigC = getupvalue(require(Client.PlayerScripts.CombatFramework.RigController),2)
    Combat =  getupvalue(require(Client.PlayerScripts.CombatFramework),2)
    NPCList = getupvalue(Queue.new,1)[1].NPCDialogueEnabler.bin
    RaidMicroship = table.clone(AllRaidShip.raids)
    table.insert(RaidMicroship,"CurrentFruit")
end

do -- Variable From Function
    WebScrap = game:HttpGet(("https://www.roblox.com/games/2753915549/UPDATE-Blox-Fruits")) or '<meta name="description" content=: 2300/>'
    MaxedLevel = WebScrap:split('<meta name="description" content=')[2]:split("/>")[1]:split(": ")[2]:split("\n")[1]
    AllFruits = network:Send("CommF_","GetFruits")
    MAXLEVEL = MaxLevel or tonumber(MaxedLevel)
    task.spawn(function()
        LocationTag = Client:WaitForChild("LocationTag")
    end)
end

-- local IslandSpawn = function(v)
--     if Client.Data.Level.Value >= 10 then return true end ;
--     local vv = game:GetService("Workspace")["_WorldOrigin"].Locations["Pirate Starter"] ;
--     if Distance(v.Position) > tonumber(tonumber(tostring(vv.Mesh.Scale):split(",")[1])/2) then 
--         return false ;
--     else
--         print("no ok")
--     end ; 
--     return true ;
-- end ;

local Char = Client.Character
local Root = Char.HumanoidRootPart

do -- Quest + MobData
    for I,Data in pairs(Guide.Data.NPCList) do
        for Index,Level in pairs(Data.Levels) do
            if not MaxLevelOfSea or Level > MaxLevelOfSea then
                MaxLevelOfSea = Level
            end
            if not MinLevelOfSea or Level < MinLevelOfSea then
                MinLevelOfSea = Level
            end
        end
    end

    EnemyRegions = WorldData.EnemyRegions:GetChildren()
    EnemySpawns = WorldData.EnemySpawns:GetChildren()
    Enemy = {
        Region = {},
        Spawn = {},
    }
    BlacklistBoss = {
        "Ice Admiral [Lv. 700] [Boss]",
        "Longma [Lv. 2000] [Boss]",
        "rip_indra [Lv. 1500] [Boss]",
        "Cake Prince [Lv. 2300] [Raid Boss]",
        "Order [Lv. 1250] [Raid Boss]",
        "Don Swan [Lv. 1000] [Boss]",
        "Saber Expert [Lv. 200] [Boss]",
    }

    for i,v in pairs(EnemyRegions) do
        for a,b in pairs(EnemySpawns) do
            if (b.Position - v.Position).Magnitude <= v.Mesh.Scale.X/2 then
                local npcName = FormatEnemyName(b.Name)
                Enemy.Region[v.Name] = Enemy.Region[v.Name] or {}
                Enemy.Spawn[npcName] = Enemy.Spawn[npcName] or {}
                table.insert(Enemy.Region[v.Name],b)
                table.insert(Enemy.Spawn[npcName],v)
            end
        end
    end
end

do -- Teleporting Server Stuff Function
    local Locations = "any" -- Singapore / United States / Japan / Etc / Any;
    local History;
    local HttpService = game:GetService("HttpService");

    (function()
        if not isfolder("Unique hub Premium/BloxFruit") then makefolder("Unique hub Premium/BloxFruit") end
        if not isfile("Unique hub Premium/BloxFruit/History.json") then writefile("Unique hub Premium/BloxFruit/History.json", HttpService:JSONEncode({})) end

        History = HttpService:JSONDecode(readfile("Unique hub Premium/BloxFruit/History.json"));
    end)()

    local function LogHistory(serverId)
        History[serverId] = tick();
        writefile("Unique hub Premium/BloxFruit/History.json", HttpService:JSONEncode(History))
    end

    local function CheckServer(serverId)
        for JobId, Time in pairs(History) do
            if JobId == serverId and math.abs(Time - tick()) < 3600 then 
                return false
            end
        end
        return true
    end

    local function RequestTeleport(JobId,reason)
        if JobId then
            game:GetService("ReplicatedStorage").__ServerBrowser:InvokeServer("teleport", JobId)
            local Connection
            Connection = game:GetService("Players").LocalPlayer.OnTeleport:Connect(function(State)
                if State == Enum.TeleportState.Failed then
                    Connection:Disconnect()
                    if workspace:FindFirstChild("Message") then
                        workspace.Message:Destroy()
                    end
                    wait(1)
                    Serverhop(reason)
                end
            end)
        end
    end

    Serverhop = function(reason)
        if Settings.DisableServerhop then return end
        if DoNotHop or workspace:FindFirstChild("Message") then return end
        local Message = Instance.new("Message",workspace)
        Message.Text = "Hopping Server for "..(reason or "Unkown reason")
        local Request = ("https://games.roblox.com/v1/games/%s/servers/Public?sortOrder=%s&excludeFullGames=true&limit=100&cursor="):format(game.PlaceId,Settings.LowServerhop and "Asc" or "Desc")
        local Success,Content,cursor = nil,nil,""
        repeat
            repeat 
                Success,Content = pcall(game.HttpGet,game,Request..cursor)
                wait()
            until Success
            local Servers = HttpService:JSONDecode(Content)
            cursor = Servers.nextPageCursor
            if not cursor then cursor = "" end
            for i,v in pairs(Servers.data) do
                if v.playing > 0 and CheckServer(v.id) then
                    LogHistory(v.id);
                    return RequestTeleport(v.id,reason)
                end
            end
            wait(1)
        until not cursor
        
        if BreakHop and workspace:FindFirstChild("Message") then
            workspace.Message:Destroy()
        end
    end
end

do -- Settings Initializer
    local path = "Unique hub Premium/BloxFruit"
    if not isfolder(path) then makefolder(path) end
    DefaultConfigName = path.."/Default-config.json"
    ConfigName = path.."/"..Client.UserId.."-config.json"
    Settings = isfile(ConfigName) and readfile(ConfigName)
    getIndentity = getthreadidentity or syn.get_thread_identity
    setIdentity = setidentity or syn.set_thread_identity
    DefaultSettings = isfile(DefaultConfigName) and readfile(DefaultConfigName)
    if DefaultSettings then
        if type(DefaultSettings) == "string" and DefaultSettings:find"{" then
            local Success,Result
            task.spawn(function()
                Success,Result = pcall(function()
                    return game:GetService("HttpService"):JSONDecode(DefaultSettings)
                end)
            end)
            wait(0.1)
            if Success then
                DefaultSettings = Result
            else
                DefaultSettings = nil
            end
        end
    end
    if Settings then
        if type(Settings) == "string" and Settings:find"{" then
            local Success,Result
            task.spawn(function()
                Success,Result = pcall(function()
                    return game:GetService("HttpService"):JSONDecode(Settings)
                end)
            end)
            wait(0.1)
            if Success then
                Settings = Result
            else
                Settings = {}
            end
        else
            Settings = {}
        end
    else
        Settings = {}
    end

    for i,v in pairs(DefaultSettings or {
        IslandTP = true,
        DoubleQuest = true,
        CustomLevelFarmValue = 2450,
        -- SkipTweenIslandFruit = true,
        KillAura = true,
        AimbotTarget = {Player = true},
        AimbotFov = 200,
        AutoStats = {},
        SkylandKill = true,
        PlayerHunt = true,
        HealthMob = 20,
        EspName = true,
        EspBox = true,
        EspTracers = true,
        AutoSetSpawn = true,
        NoCameraShake = true,
        NoAttackAnimation = true,
        FastAttack = true,
        AutoRaidHop = true,
        NewFastAttack = true,
        -- ReduceOnMinimize = true
    }) do 
        if Settings[i] == nil then
            Settings[i] = v
        end
    end
    if getgenv().Config then
        Settings = getgenv().Config
    end
end

do -- Config Function
    function saveConfig()
        if not isfolder("Unique") then
            makefolder("Unique")
        end
        writefile(ConfigName,game:GetService("HttpService"):JSONEncode(Settings))
    end
    function setDefaultConfig()
        if not isfolder("Unique") then
            makefolder("Unique")
        end
        writefile(DefaultConfigName,game:GetService("HttpService"):JSONEncode(Settings))
    end
end

FirstSea = game.PlaceId == 2753915549
SecondSea = game.PlaceId == 4442272183
ThirdSea = game.PlaceId == 7449423635
SeaIndex = ThirdSea and 3 or SecondSea and 2 or FirstSea and 1 or Client:Kick("Didn't update this Sea")

dialogues.KilledIndraBoss = nil
dialogues.KilledIceBoss = nil
dialogues.KilledSpringBoss = nil
dialogues.KilledCitizenBoss = nil

do
    CurrentAllMob = {}
    recentlySpawn = 0
    StoredSuccessFully = 0
    canHits = {}
    RecentCollected = 0
    FruitInServer = {}
    RecentlyLocationSet = 0
    lastequip = tick()
end

do
    UpdateQuestData = function(LEVEL,PreviousQuest)
        task.desynchronize()
        local Lvl = math.clamp(LEVEL or Client.Data.Level.Value,MinLevelOfSea,MaxLevelOfSea)
        local less = 1/0
        local AllNearestQuests = {}
        BOSSNAME = nil
        for i,_v in pairs(Quest) do
            for loop = 1,#_v do
                local v = _v[loop]
                if Lvl >= v.LevelReq and not v.MeetsRequirements then
                    if Lvl - v.LevelReq < less then
                        if v.Task[table.foreach(v.Task,tostring)] ~= 1 then
                            QUESTNAME = tostring(i)
                            QUESTNUMBER = tonumber(loop)
                            MONNAME = (table.foreach(v.Task,tostring))
                            QUESTLEVEL = v.LevelReq
                            less = Lvl - v.LevelReq
                            table.insert(AllNearestQuests,1,{
                                name = tostring(i),
                                num = tonumber(loop),
                                mon = (table.foreach(v.Task,tostring)),
                                lvl = v.LevelReq,
                            })
                        end
                    end
                end
            end
        end
        if Lvl < 5000 then
            for i,v in pairs(Quest[QUESTNAME]) do
                if Lvl >= v.LevelReq and not v.MeetsRequirements and v.Task[table.foreach(v.Task,tostring)] == 1 then
                    BOSSQUESTNAME = QUESTNAME
                    BOSSQUESTNUMBER = tonumber(i)
                    BOSSNAME = (table.foreach(v.Task,tostring))
                    BOSSLEVEL = v.LevelReq
                end
            end
        end
        for I,Data in pairs(Guide.Data.NPCList) do
            for Index,Level in pairs(Data.Levels) do
                if Level == QUESTLEVEL then
                    QUESTMOB = Data.NPCName
                    QUESTPOS = CFrame.new(Data.Position)
                end
                if Level == BOSSLEVEL then
                    BOSSMOB = Data.NPCName
                    BOSSPOS = CFrame.new(Data.Position)
                end
                if AllNearestQuests[2] and Level == AllNearestQuests[2].lvl then
                    AllNearestQuests[2].Pos = CFrame.new(Data.Position)
                    AllNearestQuests[2].QuestNPC = Data.NPCName
                end
            end
        end
        if PreviousQuest then
            if AllNearestQuests[2] and QUESTMOB == AllNearestQuests[2].QuestNPC then
                QUESTNAME = AllNearestQuests[2].name
                QUESTNUMBER = AllNearestQuests[2].num
                MONNAME = AllNearestQuests[2].mon
                QUESTLEVEL = AllNearestQuests[2].lvl
                QUESTMOB = AllNearestQuests[2].QuestNPC
                QUESTPOS = AllNearestQuests[2].Pos
            end
        end
        if ("Shanda"):find(MONNAME) or MONNAME == "Wysper" then
            QUESTPOS = CFrame.new(-7860, 5545, -380)
        end
        if ("God's Guard"):find(MONNAME) then
            QUESTPOS = CFrame.new(-4723, 845, -1951)
        end
        if MONNAME:sub(1,#MONNAME) == ("Bandit") then
            QUESTPOS = CFrame.new(1060, 16, 1549)
        end
        if MONNAME:sub(1,#MONNAME) == ("Zombie") then
            QUESTPOS = CFrame.new(-5494, 48, -794)
        end
        task.synchronize()
        return AllNearestQuests
    end
    GetMobName = function()
        if game.Players.LocalPlayer.PlayerGui.Main.Quest.Visible then
            local Text = game.Players.LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text:split(" ")
            local RealText = ""
            local List = #Text
            local Is = true
            if Text[List]:find("/1)") then
                Is = false
            end
            table.remove(Text,1)
            if tonumber(Text[1]) then
                table.remove(Text,1)
            end
            table.remove(Text,#Text)
            for i=1,#Text do local v = Text[i]
                RealText = RealText..v
                if #Text ~= i then
                    RealText = RealText.." "
                end
            end
            if Is then
                RealText = RealText:sub(1,#RealText-1)
            end
            return RealText
        end
    end
    _hasTag = function(TAG,OBJ)
        return CollectionService:HasTag(OBJ or game.Players.LocalPlayer.Character,TAG)
    end
    isnetworkowner = isnetworkowner or function(part)
        local Client = game.Players.LocalPlayer
        if typeof(part) == "Instance" and part:IsA("BasePart") then
            local Distance = math.clamp(Client.SimulationRadius,0,1250)
            local MyDist = Client:DistanceFromCharacter(part.Position)
            if MyDist < Distance then
                for i,v in pairs(game.Players:GetPlayers()) do
                    if v:DistanceFromCharacter(part.Position) < MyDist and v ~= Client then
                        return false
                    end
                end
                return true
            end
        end
    end
    InArea = function(Pos,Location)
        task.desynchronize()
        local nearest,scale = nil,0
        if Location then
            if dist(Pos,Location.Position,true) <= (Location.Mesh.Scale.X/2)+500 then
                return Location
            end
        end
        for i,v in pairs(Locations:GetChildren()) do
            if dist(Pos,v.Position,true) <= (v.Mesh.Scale.X/2)+500 then
                if scale < v.Mesh.Scale.X then
                    scale = v.Mesh.Scale.X
                    nearest = v
                end
            end
        end
        task.synchronize()
        return nearest
    end
    dist = function(a,b,noHeight)
        if not b then
            b = Root.Position
        end
        return (Vector3.new(a.X,not noHeight and a.Y,a.Z) - Vector3.new(b.X,not noHeight and b.Y,b.Z)).magnitude
    end
    _hasNonWeapon = function()
        for i,v in pairs(Backpack:GetChildren()) do
            if v:IsA("Tool") and v.ToolTip == "" and not v:FindFirstChildOfClass("RemoteFunction") then
                return true
            end
        end
    end
    _hasItem = function(name)
        if Client.Backpack:FindFirstChild(name) then return true end
        if Client.Character:FindFirstChild(name) then return true end
        for i,v in pairs(_C("getInventoryWeapons") or {}) do
            if v.Name == name then return v end
        end
    end
    _hasFruit = function()
        local Backpack = Client.Backpack:GetChildren()
        for i=1,#Backpack do local v = Backpack[i]
            if v.Name:lower():find("fruit") then
                return true
            end
        end
        local Character = Client.Character:GetChildren()
        for i=1,#Character do local v = Character[i]
            if v:IsA("Tool") and v.Name:lower():find("fruit") then
                return true
            end
        end
    end
    CollectFruit = function()
        local CollectValue = Priority:get("CollectFruit")
        if not CollectValue:check() then return end
        local Char = Client.Character
        if not Client.Team then _C("SetTeam",Client.Team.Name) end
        if not Char then return end
        if not Char:FindFirstChild("Humanoid") then return end
        if Char:FindFirstChild("Humanoid").Health <= 0 then return end
        if not Root then return end
        if #FruitInServer <= 0 then return end
        -- LeaveSpecificPlace("Cursed Ship")
        local CollectValue = Priority:get("CollectFruit")
        local function Collect(v,CanTween)
            if v.Name == "Fruit " then
                CollectValue:set()
                if Char:FindFirstChild("Humanoid").Health <= 0 or not v:FindFirstChild("Handle") then return end
                repeat
                    CollectValue:set()
                    Root.CFrame = CFrame.new(v:WaitForChild("Handle").Position + Vector3.new(math.random(-3,3),math.random(-5,5),math.random(-3,3)))
                    firetouchinterest(v.Handle,Root,0)
                    task.wait()
                    firetouchinterest(v.Handle,Root,1)
                until v.Parent ~= workspace
                CollectValue:clear()
            end
            if v:IsA("Tool") and v:FindFirstChild("Handle") then
                if dist(v.Handle.Position) <= 5000 then
                    if tick() - RecentCollected < 15 then return end
                    RecentCollected = tick()
                    firetouchinterest(v.Handle,Char.HumanoidRootPart,0)
                    firetouchinterest(v.Handle,Char.HumanoidRootPart,1)
                end
            end
        end
        for i,v in pairs(FruitInServer) do
            if v then
                Collect(v)
                if v.Name == "Fruit " or v:IsA("Tool") then
                    break
                end
            end
        end
        CollectValue:clear()
    end
    FullyBringFruit = function(hop)
        repeat wait() until game.Players.LocalPlayer.Character
        repeat wait() until not CollectFruit()
        wait()
        StoreFruit()
        wait(5)
        if hop then
            Serverhop("Auto Collect Fruit")
        end
    end
    IsCombat = function()
        return Client.PlayerGui.Main.InCombat.Visible
    end
    _hasChip = function()
        local Backpack = Client.Backpack:GetChildren()
        for i=1,#Backpack do local v = Backpack[i]
            if v.Name:lower():find("microchip") then
                return true
            end
        end
        local Character = Client.Character:GetChildren()
        for i=1,#Character do local v = Character[i]
            if v:IsA("Tool") and v.Name:lower():find("microchip") then
                return true
            end
        end
    end
    getFruitDrop = function()
        local fruits = {}
        for i,v in pairs(workspace:GetChildren()) do
            if v:IsA("Tool") or v.Name:find("Fruit") then
                fruits[#fruits+1] = v
            end
        end
        return fruits
    end
    function toServerFruit(Text)
        local Slice = Text:split(":")
        return (Slice[1].."-"..Slice[1]..((Slice[2] and ":"..Slice[2]) or "")):gsub(" Fruit","")
    end
    StoreFruit = function()
        if not DoNotStore then
            local Stored = 0
            local Pattern = "<Color=Green>Collected<Color=/> and <Color=Yellow>stored<Color=/> <Color=Blue>%s<Color=/>"
            local MyFruit = _C("getInventoryFruits")
            for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
                if v.Name:find("Fruit") and not table.find(CollectedFruit,v.Name) then
                    local Name = toServerFruit(v.Name)
                    Noti.new(Pattern:format(v.Name)):Display()
                    _C("StoreFruit",Name,v)
                    Stored = Stored + 1
                    table.insert(CollectedFruit,v.Name)
                end
            end
            for i,v in pairs(game.Players.LocalPlayer.Character:GetChildren()) do
                if v.Name:find("Fruit") and not table.find(CollectedFruit,v.Name) then
                    local Name = toServerFruit(v.Name)
                    Noti.new(Pattern:format(v.Name)):Display()
                    _C("StoreFruit",Name,v)
                    Stored = Stored + 1
                    table.insert(CollectedFruit,v.Name)
                end
            end
            StoredSuccessFully = tick()
        end
    end
    RaidInfo = function()
        local Info = {}
        local Locations = workspace._WorldOrigin.Locations
        local Client = game.Players.LocalPlayer
        local Character = Client.Character
        for i,v in pairs(Locations:GetChildren()) do
            if v.Name:sub(1,6) == "Island" then
                local Distance = (Vector3.new(v.Position.X,0,v.Position.Z) - Vector3.new(Char.HumanoidRootPart.Position.X,0,Char.HumanoidRootPart.Position.Z)).magnitude
                if Distance <= 2000 then
                    Info.ID = v:FindFirstChildOfClass("Folder").Name
                    Info._ID = v:FindFirstChildOfClass("Folder")
                    Info.LastestIsland = v
                    Info.Number = 1
                    break
                end
            end
        end
        function Info.new(INDEX)
            if not Info.ID then return end
            for Do=1,5,1 do
                for i,v in pairs(Locations:GetChildren()) do
                    if v.Name:find(("Island %s"):format(Do)) then
                        if v:FindFirstChild(Info.ID) then
                            Info.LastestIsland = v
                            Info.Number = Do
                        end
                    end
                end
            end
            if not IsRaiding() then
                Info.Ended = true
            end
            return Info
        end
        return Info
    end
    LeaveSpecificPlace = function(name)
        if FirstSea then
            if name == "Skylands" and dist(workspace.Map.SkyArea2.PathwayHouse.Exit.Position) <= 800 then
                
                _C("requestEntrance", workspace.Map.SkyArea1.PathwayTemple.ExitPoint.Position);
            end
            if name == "Underwater City" and dist(workspace.Map.Fishmen.Entrance.Position) <= 5000 then
                
                _C("requestEntrance",Vector3.new(3864.6884765625, 6.736950397491455, -1926.214111328125))
            end
        end
        if SecondSea then
            if name == "Cursed Ship" and dist(workspace.Map.GhostShipInterior["Meshes/BoatFlower_FlowerBoat_05"].Position) <= 5500 then
                
                _C("requestEntrance",Vector3.new(-6508.55810546875, 89.03499603271484, -132.83953857421875))
            end
        end
    end
    tp = function(target,statement,disableIslandSkip,fromRaid,CallingFrom)
        if not Root then return end
        if IsRaiding() and not fromRaid then return end
        if tweenPause then return end
        task.desynchronize()
        local thisId
        local s,e = pcall(function()
            local Dista,distm,middle = dist(target,nil,true),1/0
            if Char and Root and Dista >= 2000 and tick() - recentlySpawn > 5 then
                for i,v in pairs(CanTeleport[SeaIndex]) do
                    local distance = dist(v,target,true)
                    if distance < dist(target,nil,true) and distance < distm then
                        distm,middle = distance,v
                    end
                end
                task.synchronize()
                if middle and InArea(Root.Position) ~= InArea(middle) and not IsRaiding() then
                    -- print(Root.Position,"\n",target.p)
                    -- print(Dista,distm,CurrentArea,InArea(middle))
                    print(CallingFrom)
                    _C("requestEntrance",middle)
                end
                if not disableIslandSkip and Settings.IslandTP then
                    if not IsCombat() and not _hasNonWeapon() and Root and not _hasChip() and (not _hasFruit()) and not IsRaiding() then
                        local Area = InArea(target.p)
                        local MyArea = InArea(Char.HumanoidRootPart.Position)
                        local SpawnPoint = workspace["_WorldOrigin"].PlayerSpawns[Client.Team.Name]:GetChildren()
                        local dista,distm,charDist,nearest = 2000,9000
                        for i,v in pairs(SpawnPoint) do
                            local Position = v:GetPivot().p
                            local distance = dist(target.p,Position,true)
                            if distance <= dista then
                                charDist = dist(Position,nil,true)
                                dista,nearest = distance,v
                            end
                        end
                        if nearest and (charDist <= 8700) then
                            if not Char:FindFirstChild("Humanoid") then return end
                            if not Char:FindFirstChild("HumanoidRootPart") then return end
                            if Char.HumanoidRootPart:FindFirstChild("Died") then
                                Char.HumanoidRootPart.Died:Destroy()
                            end
                            repeat wait()
                                pcall(task.spawn,_C,"SetLastSpawnPoint",nearest.Name)
                            until ClientData.LastSpawnPoint.Value == nearest.Name
                            pcall(function()
                                if Current_Exploit("Fluxus") or Current_Exploit("Comat") or IsValyse then
                                    Char.Humanoid:ChangeState(15)
                                else
                                    Root:Destroy()
                                end
                            end)
                            repeat wait(.1) until Root.Parent
                        end
                    end
                end
                task.desynchronize()
            end
            if tweenActive and lastTweenTarget and (dist(target, lastTweenTarget) < 10 or dist(lastTweenTarget) >= 10) then
                return
            end
            tweenid = (tweenid or 0) + 1 
            lastTweenTarget = target
            statement = statement or function() end
            local Char = Client.Character
            local Root = Char.HumanoidRootPart
            thisId = tweenid
            if Util.FPSTracker.FPS > 60 then
                setfpscap(60)
            end
            task.spawn(pcall,function()
                lastPos = {tick(),target}
                task.synchronize()
                local currentState = statement()
                local currentDistance = dist(Root.Position, target, true)
                local oldDistance = currentDistance
                Char.Humanoid:SetStateEnabled(13,false)
                while Root and currentDistance > 75 and currentState and thisId == tweenid and Char.Humanoid.Health > 0 do
                    local Percent = (58/math.clamp(Util.FPSTracker.FPS,0,60))
                    local Speed = 6*Percent
                    local Current = Root.Position
                    local Dift = Vector3.new(target.X,0,target.Z) - Vector3.new(Current.X,0,Current.Z)
                    local Sx =  (Dift.X < 0 and -1 or 1)*Speed
                    local Sz =  (Dift.Z < 0 and -1 or 1)*Speed
                    local SpeedX = math.abs(Dift.X) < Sx and Dift.X or Sx
                    local SpeedZ = math.abs(Dift.Z) < Sz and Dift.Z or Sz
                    task.spawn(function()
                        currentDistance = dist(Root.Position, target, true)
                        currentState = statement()
                        if currentDistance > oldDistance+10 then
                            tweenid = -1
                            tweenPause = true
                            Root.Anchored = true
                            wait(1)
                            tweenPause = false
                            Root.Anchored = false
                        end
                        oldDistance = currentDistance
                    end)
                    Root.CFrame = Root.CFrame + Vector3.new(math.abs(SpeedZ) < (5*Percent) and SpeedX or SpeedX/1.5, 0, math.abs(SpeedX) < (5*Percent) and SpeedZ or SpeedZ/1.5)
                    Root.CFrame = CFrame.new(Root.CFrame.X,target.Y,Root.CFrame.Z)
                    Char.Humanoid:ChangeState(11)
                    tweenActive = true
                    task.wait(0.001)
                end
                Char.Humanoid:SetStateEnabled(13,true)
                tweenActive = false
                if currentDistance <= 100 and currentState and thisId == tweenid then
                    Root.CFrame = target
                end
            end)
        end)
        if not s then print(e) end
        task.synchronize()
        return thisId
    end
    stoptp = function()
        tweenid = -1
    end
    RaidFruitName = function(txt)
        if txt == "" then
            return "Fruitless"
        end
        local compile = string.match(txt, "%-(.+)")
        if compile then
            return compile
        end
        return txt
    end
    ac_lvl = function()
        task.desynchronize()
        local Level = Client.Data.Level.Value
        local Exp = Client.Data.Exp.Value
        while true do
            local _EXP = Exp_Calc(Level)
            if Exp >= _EXP then
                Level = Level + 1
                Exp = Exp - _EXP
            else
                break
            end
        end
        task.synchronize()
        return math.clamp(Level,0,MAXLEVEL)
    end
    IsRaiding = function()
        return Client.PlayerGui.Main.Timer.Visible or JustStarted
    end
    IsSameName = function(full,sub)
        return full:lower():sub(1,#sub) == sub:lower()
    end
    purchaseCombat = function(name,tf)
        local success,data
        if name == "DragonClaw" then
            success,data = pcall(_C,"BlackbeardReward","DragonClaw","2")
        else
            success,data = pcall(_C,"Buy"..name,tf)
        end
        return success and (data == 1 or data == 2)
    end
    checkIsAvailable = function(name,mastery)
        local CompatibilityName = {
            ElectricClaw = "Electric Claw",
            BlackLeg = "Black Leg",
            DragonClaw = "Dragon Claw",
            FishmanKarate = "Fishman Karate",
            DragonTalon = "Dragon Talon",
            SharkmanKarate = "Sharkman Karate",
            DeathStep = "Death Step",
        }
        if not MasteryData[name] or MasteryData[name] < mastery then
            if purchaseCombat(name) then
                wait(.5)
                pcall(function()
                    MasteryData[name] = GetToolFromTip(CompatibilityName[name] or name,true).Level.Value
                end)
            end
            return
        end
        return true
    end

    -- Char Function
    ModAbility = function()
        for i,v in pairs(getgc()) do
            if type(v) == "function" then
                local Script = getfenv(v).script
                if Script and Script.Parent == Char then
                    for _,data in pairs(getupvalues(v)) do
                        if type(data) == "table" and rawget(data,"LastUse") then
                            if Script.Name == "Dodge" and RunnedOn ~= Char then
                                RunnedOn = Char
                                debug.setconstant(v,143,math.clamp(0,-0.2,1.4))
                            end
                            data.LastAfter = nil
                            data.LastUse = nil
                            setmetatable(data,{
                                __index = function(self,key)
                                    return 0
                                end,
                                __newindex = function(self,key,value)
                                    return
                                end
                            })
                        end
                    end
                end
            end
        end
    end
    function DestroyBusy(v)
        if v.Name:find("Body") and not v:IsA("BodyVelocity") and not v:IsA("BodyGyro") and Settings.NoStun then
            game.Debris:AddItem(v,0)
        end
        if v.Name == "KenDisabled" then
            wait()
            game.Debris:AddItem(v,0)
        end
        if v.Name == "GeppoCount" then
            wait()
            game.Debris:AddItem(v,0)
        end
        if v.Name == "Cooldown" and gun_cd_obj ~= v then
            gun_cd_obj = v
            v.Value = 0.15
        end
    end
    function OnChar(Char)
        Root = Char:WaitForChild("HumanoidRootPart")
        Char:WaitForChild("Energy").Changed:Connect(function()
            if Settings.InfStam then
                -- changeValue(Char.Energy,"Value",Char.Energy.MaxValue)
                Char.Energy.Value = Char.Energy.MaxValue
            end
        end)
        Char:WaitForChild("Busy").Changed:Connect(function()
            if Settings.NoStun and Char.Busy.Value then
                Char.Busy.Value = false
            end
        end)
        for i,v in pairs({"Soru","Geppo","KenUpgrade","Buso"}) do
            if Settings["Semi"..v] then
                CollectionService:AddTag(Char,v)
            end
        end
        Char:WaitForChild("Humanoid").HealthChanged:Connect(function()
            if Settings.NoBountyLoss then
                local MaxHealth = Char.Humanoid.MaxHealth
                local OldChar = Char
                if Char.Humanoid.Health > 0 and Char.Humanoid.Health <= MaxHealth*(Settings.NoBountyLossHealth/100) then
                    if OldChar == Char then
                        if not _C("SetTeam",Client.Team.Name) then
                            Char.Head:Destroy()
                        end
                    end
                end
            end
        end)
        if Settings.Invisible then pcall(invisible) end
    end
    CheckBackpack = function(name)
        return Client.Backpack:FindFirstChild(name)
    end
    function GetMaterial(MartialName)
        for i,v in pairs(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("getInventory")) do
            if type(v) == "table" then
                if v.Type == "Material" then
                    if v.Name == MartialName then
                        return v.Count
                    end
                end
            end
        end
        return 0
    end
    function EquipBest()
        -- if Settings.AutoElectricClaw and Finished.ElecticClaw then
        --     _C("BuyElectricClaw")
        -- elseif Settings.AutoSuperhuman and Finished.Superhuman then
        --     _C("BuySuperhuman")
        -- elseif Settings.AutoDeathStep and Finished.DeathStep then
        --     _C("BuyDeathStep")
        -- elseif Settings.AutoSharkmanKarate and Finished.SharkmanKarate then
        --     _C("BuySharkmanKarate")
        -- elseif Settings.AutoDragonTalon and Finished.DragonTalon then
        --     _C("BuyDragonTalon")
        -- else
        --     _C("BuySuperhuman")
        -- end
    end
    GetToolFromTip = function(Tip,findwithname,bp)
        if bp ~= nil then
            if bp then
                for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
                    if v:IsA("Tool") and (v.ToolTip == Tip or (findwithname and v.Name == Tip)) then
                        return v
                    end
                end
            else
                local v = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Tool") do
                    if v and v:IsA("Tool") and (v.ToolTip == Tip or (findwithname and v.Name == Tip)) then
                        return v
                    end
                end
            end
        else
            for i,v in pairs(game.Players.LocalPlayer.Backpack:GetChildren()) do
                if v:IsA("Tool") and (v.ToolTip == Tip or (findwithname and v.Name == Tip)) then
                    return v
                end
            end
            local v = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Tool") do
                if v and v:IsA("Tool") and (v.ToolTip == Tip or (findwithname and v.Name == Tip)) then
                    return v
                end
            end
        end
    end
    Equip = function(tool)
        tool = lockWeapon or tool
        if tick() - recentlySpawn < 0.5 then return end
        if tick() - lastequip < 0.1 then return end
        if not tool then return end
        if not Char then return end
        if type(tool) == "string" then
            tool = Client.Backpack:FindFirstChild(tool)
        end
        if tool and tool.Parent ~= Char then
            local Human = Char:FindFirstChild("Humanoid")
            if Human then
                Char.Humanoid:EquipTool(tool)
            end
            lastequip = tick()
        end
    end
    Unequip = function(tool)
        Client.Character.Humanoid:UnequipTools(tool)
    end
    Buso = function()
        if not Client.Character:FindFirstChild("HasBuso") then
            task.spawn(_C,"Buso")
        end
    end

    -- render
    _getNearest = function(name,custom,ishaki,distance)
        local Player = true
        if name == "NOPLAYER" then
            Player = false
            name = nil
        end
        local LIST = custom or CurrentAllMob
        local dis,health,nearest = distance or 1/0,1/0
        for i=1,#LIST do local v = LIST[i]
            local Human = v:FindFirstChildOfClass("Humanoid")
            if (not name or IsSameName(v.Name,name) or name == "") and (Player or v.Parent ~= workspace.Characters) then
                if Human and Human.Health > 0 then
                    local dist = dist(Human.RootPart.Position)
                    if (dist < dis or (dist - dis < 50 and Human.Health < health)) and (name or not table.find(BlacklistBoss,v.Name)) then
                        if (not ishaki or v:FindFirstChild("LeftHand_BusoLayer1",true)) then
                            dis,health,nearest = dist or dis,Human.Health,v
                        end
                    end
                end
            end
        end
        return nearest
    end
    FindNPC = function(Namelist,statement)
        local names = Namelist
        if type(Namelist) == "string" then names = {Namelist} end
        local result = {}
        for _,name in pairs(names) do
            local v = _getNearest(name)
            local SpawnList = Enemy.Spawn[name]
            if SpawnList then
                for i,SpawnAt in pairs(SpawnList) do
                    result[#result+1] = {
                        Spawned = v,
                        Name = name,
                        dist = v and dist(v.HumanoidRootPart.Position) or 9e9,
                        Spawner = SpawnAt,
                        toSpawn = function(DontSkip)
                            if SpawnAt and not v and (not LocationTag or SpawnAt ~= LocationTag.Value) and statement() then
                                NeedNoclip = true
                                tp(SpawnAt.CFrame + Vector3.new(0,50,0),function()
                                    if tick() - RecentlyLocationSet < 0.5 and SpawnAt ~= LocationTag.Value then
                                        RecentlyLocationSet = tick()
                                        game.ReplicatedStorage.Remotes.Location:FireServer(SpawnAt)
                                    end
                                    return statement() and (not LocationTag or SpawnAt ~= LocationTag.Value)
                                end)
                                NeedNoclip = false
                            elseif v and tick() - RecentlyLocationSet < 0.5 and SpawnAt ~= LocationTag.Value then
                                RecentlyLocationSet = tick()
                                game.ReplicatedStorage.Remotes.Location:FireServer(SpawnAt)
                            end
                        end,
                        InArea = (LocationTag and SpawnAt == LocationTag.Value)
                    }
                end
            end
        end
        table.sort(result,function(x,y)
            return x.dist < y.dist
        end)
        return result
    end
    getHits = function(Size)
        local Hits = {}
        if nearbymon then
            local Enemies = workspace.Enemies:GetChildren()
            local Characters = workspace.Characters:GetChildren()
            for i=1,#Enemies do local v = Enemies[i]
                local Human = v:FindFirstChildOfClass("Humanoid")
                if Human and Human.RootPart and Human.Health > 0 and dist(Human.RootPart.Position) < Size+5 then
                    table.insert(Hits,Human.RootPart)
                end
            end
            for i=1,#Characters do local v = Characters[i]
                if v ~= Client.Character then
                    local Human = v:FindFirstChildOfClass("Humanoid")
                    if Human and Human.RootPart and Human.Health > 0 and dist(Human.RootPart.Position) < Size+5 then
                        table.insert(Hits,Human.RootPart)
                    end
                end
            end
        end
        return Hits
    end
    CheckMobLevel = function(name)
        local Name = name:split("[Lv. ")[2]
        if Name then
            Name = Name:sub(1,#Name-1)
            if Name:find("Boss") then
                Name = Name:sub(1,#Name-7)
            end
        end
        return tonumber(Name) or math.huge
    end
    BringMob = function(mob,limit,AOthersMob)
        local NUMS = 0
        local OthersMob =  0
        AOthersMob = AOthersMob or 10
        limit = limit or 1/0
        local Enemies = workspace.Enemies:GetChildren()
        for i=1,#Enemies do local v = Enemies[i]
            if limit and NUMS >= limit then break end
            if not v:FindFirstChild("HumanoidRootPart") then continue end
            if v:FindFirstChildOfClass("Humanoid") and v.Humanoid.Health > 0  and dist(v.HumanoidRootPart.Position) <= 5000 and not v.Name:lower():find("boss") then
                local IsVaidMob = not mob or (v ~= mob and v.Name == mob.Name)
                if IsVaidMob or CheckMobLevel(v.Name) < CheckMobLevel(mob.Name)+100  then
                    if syn and isnetworkowner(v.HumanoidRootPart) or (v.HumanoidRootPart.Position - Client.Character.HumanoidRootPart.Position).Magnitude <= 300 then
                        if IsVaidMob or OthersMob < AOthersMob then
                            local CFrameTo = mob.HumanoidRootPart.CFrame 
                            v.HumanoidRootPart.CFrame = CFrameTo
                            v.Humanoid.JumpPower = 0
                            v.Humanoid.WalkSpeed = 0
                            v.Humanoid.Sit = true	
                            v.Humanoid.PlatformStand = true			
                            v.Humanoid:ChangeState(11)
                            v.HumanoidRootPart.CanCollide = false
                            if IsVaidMob then
                                NUMS = NUMS + 1
                            elseif OthersMob < AOthersMob then
                                OthersMob = OthersMob + 1
                            end
                        end
                    end
                end
            end
        end
    end
    comma_value = function(Value)
        local Calculated = Value
        while true do
            local Text, Amount = string.gsub(Calculated, "^(-?%d+)(%d%d%d)", "%1,%2")
            Calculated = Text
            if Amount == 0 then break end
        end
        return Calculated
    end
    InSafeZone = function(player)
        local v = player.Character
        if v and v:FindFirstChild("Humanoid") then
            if v.Humanoid.Health > 0 and v.Humanoid.RootPart then
                for _,SafeZone in pairs(WorldData.SafeZones:GetChildren()) do
                    if (v.HumanoidRootPart.Position - SafeZone.Position).magnitude <= SafeZone.Mesh.Scale.X/2 then
                        return true
                    end
                end
            end
        end
    end
    function rejoin()
        game:GetService("TeleportService"):TeleportToPlaceInstance(game.PlaceId,game.JobId,Client)
    end
end

do -- Activities Function
    function m1click(pos) 
        if not mouse then return end
        pos = pos or mouse
        wait()
        vim:SendMouseButtonEvent(pos.X or 10,pos.Y or 10,0,true,game,0)
        vim:SendMouseButtonEvent(pos.X or 10,pos.Y or 10,0,false,game,0)
        wait()
    end
    function click()
        game:GetService("VirtualUser"):ClickButton1(Vector2.new())
    end
    function KeyDown(key)
        vim:SendKeyEvent(true, key, false, game)
    end
    function KeyUp(key)
        vim:SendKeyEvent(false, key, false, game)
    end
    function KeyPress(key,delay,func)
        vim:SendKeyEvent(true, key, false, game)
        if type(delay) == "number" then task.wait(delay) end
        if func then func() end
        vim:SendKeyEvent(false, key, false, game)
    end
    function moveMouse(pos)
        vim:SendMouseMoveEvent(pos.X,pos.Y,game)
    end
    function pK(key)
        vim:SendKeyEvent(true, key, false, game)
    end
    function rK(key)
        vim:SendKeyEvent(false, key, false, game)
    end
end

-- Priority Checker
Priority.new("AutoFarmBoss")
    .new("AutoFarmMastery")
    .new("MobAura")
    .new("AutoDeathStep")
    .new("AutoSharkmanKarate")
    .new("AutoElectricClaw")
    .new("CollectFruit")
    .new("AutoFarmKenStats")
    .new("TeleportIsland")
    .new("AutoKillPlayer")
    .new("TeleporttoPlayer")
    .new("AutoFarmObservation")

if FirstSea then
    Priority.new("AutoSecondSea")
        .new("AutoPoleV1")
        .new("AutoSaber")
        .new("AutoCannon")
        .new("AutoBizentoV2")
elseif SecondSea then
    Priority.new("AutoThirdSea")
        .new("AutoSoulGuitar")
        .new("AutoDragonTrident")
        .new("AutoDarkCoat")
        .new("AutoSwanGlasses")
        .new("AutoDragonTalon")
        .new("AutoElectricClaw")
        .new("AutoRengoku")
        .new("AutoEvoRaceV2")
        .new("AutoBartiloQuest")
        .new("AutoDeathStep")
        .new("AutoSharkmanKarate")
        .new("AutoFactory")
elseif ThirdSea then
    Priority.new("AutoBone")
        .new("AutoSoulGuitar")
        .new("AutoAncientOneQuest")
        .new("AutoCompleteTrial")
        .new("AutoCursedDualKatana")
        .new("AutoDoughV2")
        .new("AutoSerpentBow")
        .new("AutoCakePrince")
        .new("TeleportToGear")
        .new("AutoPirateRaid")
        .new("AutoRainbowHaki")
        .new("TeleportToTrialDoor")
        .new("AutoTwinhook")
        .new("AutoBuddySword")
        .new("AutoPrinceCake")
        .new("AutoCDK")
        .new("AutoTushita")
        .new("AutoEliteHunter")
        .new("AutoBuddy",nil,{"AutoCDK"})
        .new("AutoHallowScythe",nil,{"AutoCDK"})
        .new("AutoCanvander")
        .new("AutoDarkDagger")
    Priority:get("AutoHallowScythe").Skipable = false
    Priority:get("AutoDarkDagger").Skipable = false
end

Priority.new("Raiding",100).Skipable = false
Priority:get("CollectFruit").Skipable = false

local QuestManager = {}

QuestManager.Guide = require(game:GetService("ReplicatedStorage").GuideModule) ; 
QuestManager.AllQuest = require(game:GetService("ReplicatedStorage").Quests) ;

QuestManager.AllQuest = (function() 
   local Data = {} ;
  
    for i ,v in pairs(QuestManager.AllQuest) do 
        Data[i] = {
            Index = i ,
            Value = v    
        }
    end
  
   return Data
end)() 

function QuestManager:FindValue(p1)
	if not p1 then return warn("havenil") end 
	for i ,v in pairs(p1) do 
		return v 
	end
end

function QuestManager:FindIndex(p1,p2) 
    if not p1 then return warn("havenil") end 
   for i ,v in pairs(p1) do 
       return i 
   end
end

function QuestManager:FindData(p1,p2,p3)
    for i, v in pairs(require(game:GetService("ReplicatedStorage").Quests)[p1]) do 
        if v.LevelReq == p2 then 
            return {
                Value = v,
                Index = i ,
            }
        end
    end
end

function QuestManager:Npcs(p1,p2) 
    
    local PositionMon ;
    for i ,v in pairs(game:GetService("Workspace")["_WorldOrigin"].EnemySpawns:GetChildren()) do 
       if v.Name:match(self:FindIndex(p2)) then 
            PositionMon = v 
       end
    end
    
    for i ,v in pairs(self.Guide.Data.NPCList) do 
        for i2 ,v2 in pairs(v.Levels) do 
            if v2 == p1 then 
				return {
                    Index = i , 
                    Value = v ,
                    MonPosition = PositionMon or nil ,
                }
            end
        end
    end
end

QuestManager.QuestBoss = function() 
    local Data , Result = {} , {}  ; 

    for i ,v in pairs(QuestManager.AllQuest) do 
        for i2 ,v2 in pairs(v.Value)do 
            if QuestManager:FindValue(v2.Task) == 1 and game.PlaceId == 2753915549 and v2.LevelReq < 700 then 
                Data[v2.Name] = {
                    Index = i , 
                    Value = v2 ,
                }  
            elseif QuestManager:FindValue(v2.Task) == 1 and game.PlaceId == 4442272183 and v2.LevelReq > 700 and v2.LevelReq < 1500 then 
                 Data[v2.Name] = {
                    Index = i , 
                    Value = v2 ,
                }  
            elseif QuestManager:FindValue(v2.Task) == 1  and game.PlaceId == 7449423635 and v2.LevelReq > 1500 and v2.LevelReq < 2500  then 
                Data[v2.Name] = {
                    Index = i , 
                    Value = v2 ,
                }          
            end
        end
    end
       
    for i ,v in pairs(Data) do 
    	Result[v.Index] = {
		  Mon = QuestManager:FindIndex(v.Value.Task) ,
		  NameQuest = v.Index ,
		  NumberQuest = QuestManager:FindData(v.Index,v.Value.LevelReq).Index,
		  CFrameQuest = QuestManager:Npcs(v.Value.LevelReq,v.Value.Task).Index.CFrame   ,   
	     }
    end
    
    local Mons = {} ;
    
    for i ,v in pairs(Result) do 
        table.insert(Mons,v.Mon) ;
    end
    
    return Result  , Mons 
end

local DataQuest , Mon = QuestManager.QuestBoss()

do -- After Loading Function
    -- Lava Remover
    function IsLava(v)
        if v:IsA("Script") and v.Name == "LavaDamage" then
            task.wait()
            v.Parent:Destroy()
        end
    end
    workspace.DescendantAdded:Connect(IsLava)
    for i,v in pairs(workspace:GetDescendants()) do
        IsLava(v)
    end
    OnChar(Char)
    Char.DescendantAdded:Connect(DestroyBusy)
    Char.ChildAdded:Connect(DestroyBusy)
    Client.CharacterAdded:Connect(function(Chr)
        Priority:get("Raiding"):clear()
        Char = Chr
        recentlySpawn = tick()
        Chr.DescendantAdded:Connect(DestroyBusy)
        Chr.ChildAdded:Connect(DestroyBusy)
        OnChar(Chr)
    end)
    Client:WaitForChild("VisionRadius").Changed:Connect(function()
        if Settings.InfKenRange then
            changeValue(Client.VisionRadius,"Value",math.huge)
        end
    end)
    CoreGui:FindFirstChild("promptOverlay",true).DescendantAdded:Connect(function(v)
        if Settings.AutoOnKickRejoin and not StopAutoRejoin then
            rejoin()
        end
    end)
    game:service("GuiService").UiMessageChanged:Connect(function(v)
        if Settings.AutoOnKickRejoin and not StopAutoRejoin then
            rejoin()
        end
    end)
    for i,v in pairs(workspace:GetChildren()) do
        if v.Name:sub(1,5) == "Chest" and v:IsA("BasePart") then
            Chest[#Chest+1] = v
        end
    end
    for i,v in pairs(workspace.Map:GetChildren()) do
        if v:FindFirstChild("IslandModel") then
            for i,v in pairs(v.IslandModel:GetChildren()) do
                if v.Name:sub(1,5) == "Chest" and v:IsA("BasePart") then
                    Chest[#Chest+1] = v
                end
            end
        end
    end
    workspace.DescendantAdded:Connect(function(v)
        if v.Name:sub(1,5) == "Chest" and v:IsA("BasePart") then
            Chest[#Chest+1] = v
        end
    end)
end

do
    _C = function(...)
        local ARGS = {...}
        local Data = network:Send("CommF_",...)
        if ARGS[1] == "requestEntrance" then
            CollectionService:AddTag(Client,"Teleporting")
            task.delay(3,function()
                CollectionService:RemoveTag(Client,"Teleporting")
            end)
            wait(.25)
        end
        return Data
    end
    _E = function(...)
        local ARGS = {...}
        local Data = network:Send("CommE",...)
        return Data
    end
    cancelQuest = function()
        _C("AbandonQuest")
    end
    Buso = function()
        if not Client.Character:FindFirstChild("HasBuso") then
            task.spawn(_C,"Buso")
        end
    end
    function _stat(stat,point)
        _C("AddPoint",stat,point)
    end
end

do -- Quest thing
    UpdateQuestData()
    QuestData = Client.PlayerGui.Main.Quest.Visible
    ReadyToComplete = false
    QuestTargetName = GetMobName()
    network.cache.connections:clear()
    network:Retrieve("QuestUpdate",function(Data)
        QuestData = Data
        ReadyToComplete,QuestTargetName,QuestKillAmount,QuestKilled,CorrectQuest,TargetIsPlayer = nil
        if Data then
            for Target,KillAmount in pairs(Data.Progress) do
                ReadyToComplete = Data.Info.Task[Target] == KillAmount+1
                QuestTargetName = Target
                QuestKillAmount = Data.Info.Task[Target]
                QuestKilled = KillAmount
                TargetIsPlayer = workspace.Characters:FindFirstChild(QuestTargetName)
                CorrectQuest = (MONNAME == Target or BOSSNAME == Target) or KillAmount >= Data.Info.Task[Target]-2 or (AvailablePlayer[Target] and Settings.PlayerHunt)
            end
        elseif ReadyToComplete then
            SecondQuest = not SecondQuest
        end
    end)
    QuestNpc = {}
    for i,v in pairs(NPCList) do
        local Model = v.Model
        if Model:FindFirstChild("QuestFloor",true) then
            QuestNpc[Model.Name] = v
            QuestNpc[Model.Name].lowername = Model.Name:lower()
        end
    end
    computed_quest = {}
    quest_fordropdown = {}
    for i,v in pairs(QuestNpc) do
        computed_quest[v.Model.Name] = v.Model.Head.CFrame
    end
    for i,v in pairs(computed_quest) do
        table.insert(quest_fordropdown,i)
    end
end

do -- Skill Function
    CheckCooldown = function(Name,Skill)
        if Name then
            local Skills = Client.PlayerGui.Main.Skills
            local Weapon = Skills:FindFirstChild(tostring(Name))
            local Skill = Weapon and Weapon:FindFirstChild(Skill)
            return Skill and Skill.Cooldown.AbsoluteSize.X ~= 0
        end
    end
    SkillCheck = function()
        local skillcorrect = {}
        for i,v in pairs(Client.PlayerGui.Main.Skills[game.Players.LocalPlayer.Character:FindFirstChildOfClass("Tool").Name]:GetDescendants()) do
            if v.ClassName == "TextLabel" then
                if v.Name == "Title" then
                    if v.TextColor3 == Color3.fromRGB(255, 255, 255) and v.Parent.Name ~= "Template" then
                        if not table.find(skillcorrect,v.Parent.Name) then
                            table.insert(skillcorrect,v.Parent.Name) 
                        end
                    else
                        if table.find(skillcorrect,v.Parent.Name) then
                            table.remove(skillcorrect,v.Parent.Name)
                        end
                    end
                end
            end
        end
        return skillcorrect
    end
    GetUsingTool = function()
        return Char:FindFirstChildOfClass("Tool")
    end
end

-- Auto Saber Inits
task.spawn(function(InitializeService)
    local Data = _C("ProQuestProgress")
    local Jungle = Map:WaitForChild("Jungle",10)
    if not Jungle then return end
    local QuestPlates = Jungle:WaitForChild("QuestPlates")
    local Press = Data.Plates
    
    for i=1,#Press do
        if not Press[i] then
            _C("ProQuestProgress","Plate",i)
        end
    end
    if not Data.UsedTorch then
        repeat 
            _C("ProQuestProgress","GetTorch")
            wait() 
        until Client.Backpack:FindFirstChild("Torch") 
        repeat
            _C("ProQuestProgress","DestroyTorch")
            wait()
        until not Client.Backpack:FindFirstChild("Torch")
    end
    if not Data.UsedCup then
        repeat
            _C("ProQuestProgress","GetCup")
            wait()
        until Client.Backpack:FindFirstChild("Cup")
        _C("ProQuestProgress","FillCup",Client.Backpack.Cup)
        repeat
            _C("ProQuestProgress","SickMan")
            wait()
        until not Client.Backpack:FindFirstChild("Cup")
    end
    if not Data.TalkedSon then
        _C("ProQuestProgress","RichSon")
    end
end)


-- Blox Fruit Utility
local Entity = {}
Entity.__index = Entity
Entity.IsAlive = function(model)
    if not model then return end
    local Humanoid = model:FindFirstChild("Humanoid")
    return Humanoid and Humanoid.Health > 0 and Humanoid
end
Entity.Attack = function(v,PriorityObject,Expression,Data)
    local Expression = Expression or function() return true end
    local Data = Data or {}
    if not PriorityObject and Priority.Activity then return end
    task.synchronize()
    local pcd = tick()
    local Human = v.Humanoid
    local Success,Error = pcall(function()
        local FlyUp = nil
        local CS = 1
        local CSStart = tick()
        repeat
            if Data.yield then Data.yield(v) end
            local CalcuLevel = FORCE_LEVEL or ac_lvl()
            if Data.Quest then
                if not FORCE_LEVEL and LastLevel ~= CalcuLevel then
                    LastLevel = CalcuLevel
                    UpdateQuestData(CalcuLevel,SecondQuest)
                end
            end
            Targetting = v
            if PriorityObject then PriorityObject:set() end
            NeedNoclip = true
            NeedAttacking = true
            NeedAimbot = true
            Buso()
            local HowFar = FlyUp and Vector3.new(0,FlyUp,0) or (Settings.PositionRotate and Step[CS] or Vector3.new(0,50,0))
            if math.abs(Human.RootPart.Position.X - 1000) < 25 then
                local a = Human.RootPart.Position + HowFar + Vector3.new(math.random(-1,1)/4,0,math.random(-1,1)/4),Human.RootPart.Position
                print(math.floor(a.X),math.floor(a.X),math.floor(a.Z))
            end
            tp(CFrame.new(Human.RootPart.Position + HowFar),function()
                return Expression() and not IsRaiding() and (not PriorityObject or PriorityObject:isActive()) and  (PriorityObject and Settings[PriorityObject.Class] or not PriorityObject and Settings.AutoFarm)
            end,Data.DontSkip,false,PriorityObject)
            if isnetworkowner(Human.RootPart) then
                Human.RootPart.CFrame = Human.RootPart.CFrame
            end
            if tick() - CSStart > 0.2 then
                CSStart = tick()
                CS = CS + 1
                if CS > #Step then
                    CS = 1
                end
            end
            local Tool = GetUsingTool()
            if Tool and ((Tool.Name == "Black Leg" and Tool.Level.Value >= 150) or (Tool.Name == "Death Step" and Tool.Level.Value >= 400)) then
                pK("V")
                rK("V")
            end
            if Settings.Weapon == "Gun" then
                click()
            end
            lastmonPos = Human.RootPart.CFrame
            Human.JumpPower = 0
            Human.WalkSpeed = 0
            Human.Sit = true			
            Human.RootPart.CanCollide = false
            Human:ChangeState(11)
            Char.Humanoid:ChangeState(11)
            if PriorityObject then
                BringMob(v)
            else
                if Settings.DoubleQuest and ClientData.Level.Value > 10 then
                    BringMob(v,nil,0)
                else
                    BringMob(v,QuestKillAmount-1)
                end
            end
            Equip(GetToolFromTip(Data.Weapon or Settings.Weapon))
            task.wait(0.02)
        until not v.Parent or Human.Health <= 1 or not Expression() or ((QuestData or not CorrectQuest) and Data.Quest) or not (not PriorityObject or PriorityObject:isActive()) or IsRaiding() or (PriorityObject and not Settings[PriorityObject.Class] or not PriorityObject and not Settings.AutoFarm)
    end)
    if not Success then warn("Attack Function Error : ",Error) end
    Targetting = nil
    NeedAttacking = false
    NeedAimbot = false
    NeedNoclip = false
    if PriorityObject then PriorityObject:clear() end
end

function CheckBossName()
	if Settings.SelectBoss == "The Gorilla King" then
		NameBoss = "The Gorilla King [Lv. 25] [Boss]"
	elseif Settings.SelectBoss == "Bobby" then
		NameBoss = "Bobby [Lv. 55] [Boss]"
	elseif Settings.SelectBoss == "Yeti" then
		NameBoss = "Yeti [Lv. 110] [Boss]"
	elseif Settings.SelectBoss == "Vice Admiral" then
		NameBoss = "Vice Admiral [Lv. 130] [Boss]"
	elseif Settings.SelectBoss == "Warden" then
		NameBoss = "Warden [Lv. 175] [Boss]"
	elseif Settings.SelectBoss == "Chief Warden" then
		NameBoss = "Chief Warden [Lv. 200] [Boss]"
	elseif Settings.SelectBoss == "Magma Admiral" then
		NameBoss = "Magma Admiral [Lv. 350] [Boss]"
	elseif Settings.SelectBoss == "Fishman Lord" then
		NameBoss = "Fishman Lord [Lv. 425] [Boss]"
	elseif Settings.SelectBoss == "Wysper" then
		NameBoss = "Wysper [Lv. 500] [Boss]"
	elseif Settings.SelectBoss == "Thunder God" then
		NameBoss = "Thunder God [Lv. 575] [Boss]"
	elseif Settings.SelectBoss == "Cyborg" then
		NameBoss = "Cyborg [Lv. 675] [Boss]"
		--World 2 
	elseif Settings.SelectBoss == "Diamond" then
		NameBoss = "Diamond [Lv. 750] [Boss]"
	elseif Settings.SelectBoss == "Jeremy" then
		NameBoss = "Jeremy [Lv. 850] [Boss]"
	elseif Settings.SelectBoss == "Fajita" then
		NameBoss = "Fajita [Lv. 925] [Boss]"
	elseif Settings.SelectBoss == "Smoke Admiral" then
		NameBoss = "Smoke Admiral [Lv. 1150] [Boss]"
	elseif Settings.SelectBoss == "Awakened Ice Admiral" then
		NameBoss = "Awakened Ice Admiral [Lv. 1400] [Boss]"
	elseif Settings.SelectBoss == "Tide Keeper" then
		NameBoss = "Tide Keeper [Lv. 1475] [Boss]"
		--World 3
	elseif Settings.SelectBoss == "Stone" then
		NameBoss = "Stone [Lv. 1550] [Boss]"
	elseif Settings.SelectBoss == "Island Empress" then
		NameBoss = "Island Empress [Lv. 1675] [Boss]"
	elseif Settings.SelectBoss == "Kilo Admiral" then
		NameBoss = "Kilo Admiral [Lv. 1750] [Boss]"
	elseif Settings.SelectBoss == "Captain Elephant" then
		NameBoss = "Captain Elephant [Lv. 1875] [Boss]"
	elseif Settings.SelectBoss == "Beautiful Pirate" then
		NameBoss = "Beautiful Pirate [Lv. 1950] [Boss]"
	elseif Settings.SelectBoss == "Cake Queen" then
		NameBoss = "Cake Queen [Lv. 2175] [Boss]"
	end
end

-- Simulation Radius Initialize

setscriptable(Client,"SimulationRadius",true)
task.spawn(function()
    while game:GetService("RunService").Stepped:Wait() do
        Client.SimulationRadius = math.huge
    end
end)

RealFuncs = {}
funcName = {
    -- [CollectFruit] = "CollectFruit",
    -- [FindNPC] = "FindNPC",
}
Funcs = setmetatable({},{
    __index = function(self,k)
        return rawget(RealFuncs,k)
    end,
    __newindex = function(self,k,v)
        funcName[v] = k
        return rawset(RealFuncs,k,v)
    end,
})
do -- Starter Thread
    task.spawn(function()
        local stacking = 0
        local printCooldown = 0
        local OldPriority = Priority.Recently
        while wait(.075) do
            -- Attackable NPC Finder
            nearbymon = false
            table.clear(CurrentAllMob)
            table.clear(canHits)
            local mobs = CollectionService:GetTagged("ActiveRig")
            for i=1,#mobs do local v = mobs[i]
                local Human = v:FindFirstChildOfClass("Humanoid")
                if Human and Human.Health > 0 and Human.RootPart and v ~= Char then
                    local IsPlayer = game.Players:GetPlayerFromCharacter(v)
                    local IsAlly = IsPlayer and CollectionService:HasTag(IsPlayer,"Ally"..Client.Name)
                    if not IsAlly then
                        CurrentAllMob[#CurrentAllMob + 1] = v
                        if not nearbymon and dist(Human.RootPart.Position) < 65 then
                            nearbymon = true
                        end
                    end
                end
            end

            if nearbymon then
                local Enemies = workspace.Enemies:GetChildren()
                local Players = Players:GetPlayers()
                for i=1,#Enemies do local v = Enemies[i]
                    local Human = v:FindFirstChildOfClass("Humanoid")
                    if Human and Human.RootPart and Human.Health > 0 and dist(Human.RootPart.Position) < 65 then
                        canHits[#canHits+1] = Human.RootPart
                    end
                end
                for i=1,#Players do local v = Players[i].Character
                    if not Players[i]:GetAttribute("PvpDisabled") and v and v ~= Client.Character then
                        local Human = v:FindFirstChildOfClass("Humanoid")
                        if Human and Human.RootPart and Human.Health > 0 and dist(Human.RootPart.Position) < 65 then
                            canHits[#canHits+1] = Human.RootPart
                        end
                    end
                end
            end

            -- Priority Debugging
            if OldPriority ~= Priority.Recently then
                -- warn("PriorityChanged :",OldPriority,"-=>",Priority.Recently)
                OldPriority = Priority.Recently
                stacking = tick()
            end
            if tick() - stacking > 60 and OldPriority and OldPriority.Class == Priority.Class then
                Priority:clear()
            elseif tick() - printCooldown > 5 then
                -- warn("Currently","-=>",Priority.Activity and Priority.Recently)
                printCooldown = tick()
            end
        end
    end)

    -- Auto Rengoku/DragonTalon Buyer
    task.spawn(function()
        local RengokuOpened = _C("BuyDragonTalon",true),_C("OpenRengoku")
        FireES = _C("BuyDragonTalon",true)
        FireES = FireES == 1 or FireES == 2 or FireES == 3
        while wait(.5) do
            if not RengokuOpened and Client.Backpack:FindFirstChild("Hidden Key") then
                FoundRengokuKey = _C("OpenRengoku")
                RengokuOpened = true
                Priority:clear("AutoRengoku")
            end
            if _hasItem("Water Key") then
                _C("BuySharkmanKarate",true)
                Priority:get("AutoSharkmanKarate"):clear()
            end
            if _hasItem("Library Key") then
                DeathStepBossAttacked = _C("OpenLibrary")
                Priority:get("AutoDeathStep"):clear()
            end
            if _hasItem("Fire Essence") then
                _C("BuyDragonTalon",1)
            end
        end
    end)

    -- 0.5sec Thread Speed
    task.spawn(function()
        local Part = Instance.new("Part",workspace)
        Part.Transparency = 1
        Part.Anchored = true
        Part.CanCollide = true
        Part.Size = Vector3.new(2500,100,2500)
        while task.wait(0.5) do
            -- Water Walker
            if Settings.WaterWalk and Char and Root then
                Part.Position = Vector3.new(Root.Position.X,-((Part.Size.Y/2)+4),Root.Position.Z)
            end

            -- Auto Activte Ken
            if (not Settings.AutoCDK or _hasItem("Cursed Dual Katana") or not ThirdSea) then
                if OM then
                    if (Settings.AutoActiveKen or Settings.AutoFarmKenStats) and left then
                        _E("Ken",true)
                    end
                else
                    OM = getrenv()._G.OM
                end
            end

            -- Auto Awaken
            if workspace.NPCs:FindFirstChild("Mysterious Entity") then
                local Fruit = ClientData.DevilFruit.Value
                if Settings.AutoAwaken and Fruit ~= "" and table.find(RaidMicroship,RaidFruitName(Fruit)) and (Finished.DragonTalon or not Settings.AutoDragonTalon) and (Finished.TrueSharkmanKarate or not Settings.AutoSharkmanKarate) and (Finished.Superhuman or not Settings.AutoSuperhuman) and (Finished.DeathStep or not Settings.AutoDeathStep) and (Finished.ElecticClaw or not Settings.AutoElectricClaw) then
                    _C("Awakener","Awaken")
                else
                    _C("Awakener","Teleport")
                end
            end

            -- CharacterPartAdding Service
            AllCharacterPart = {}
            if Char then
                for i,v in pairs(Char:GetChildren()) do
                    if v:IsA("BasePart") then
                        table.insert(AllCharacterPart,v)
                    end
                end
            end

        end
    end)
    -- 0.25sec Thread Speed
    task.spawn(function()
        while wait(0.25) do
            -- Item Indentifier
            table.clear(ItemsData.Sword)
            table.clear(ItemsData.Material)
            for i,v in pairs(itemList) do
                if v.details.Type == "Sword" then
                    ItemsData.Sword[v.details.Name] = v.details
                end
                if v.details.Type == "Material" then
                    ItemsData.Material[v.details.Name] = v.details
                end
            end

            -- Bone Count Text
            local Bone = ItemsData.Material.Bones
            if Bone then
                CurrentBone = Bone.Count
                if BoneCount then
                    BoneCount.Text = "Bones : "..CurrentBone
                end
            end

            -- Logia Check
            IsLogia = false
            if Backpack:FindFirstChild("Logia",true) then
                IsLogia = true
            elseif Char and Char:FindFirstChild("Logia",true) then
                IsLogia = true
            end

        end
    end)
    -- Auto Drop Fruit
    task.spawn(function()
        while wait(.75) do
            if Settings.AutoStoreFruit then
                if not DoNotStore or Char.Humanoid.Health <= 0 then
                    StoreFruit()
                end
            end
            if Settings.AutoDropFruit then
                for i,v in pairs(Settings.DropFruit or {}) do
                    if v then
                        for _,Fruit in pairs(Client.Backpack:GetChildren()) do
                            if Fruit.ToolTip ~= "Blox Fruit" and Fruit.Name:lower():find(i:lower()) and Fruit.Name:lower():find("fruit") then
                                pcall(function()
                                    Equip(Fruit)
                                    wait(.1)
                                    Fruit:FindFirstChild("EatRemote"):InvokeServer("Drop")
                                    wait(.1)
                                    Fruit.Parent = game
                                    delay(60,function()
                                        if Fruit.Parent == game then
                                            Fruit.Parent = workspace
                                        end
                                    end)
                                end)
                            end
                        end
                    end
                end
            end
        end
    end)
    -- PlayerHunt Available Check
    task.spawn(function()
        AvailablePlayer = {}
        if not FirstSea then return end
        while wait(.75) do
            if Settings.PlayerHunt and ClientData.Level.Value > 20 and ClientData.Level.Value < 1000 then
                IsPlayerHuntAvailable = false
                table.clear(AvailablePlayer)
                for i,v in pairs(game.Players:GetPlayers()) do
                    local Human = v.Character and v.Character:FindFirstChild("Humanoid")
                    if v ~= Client and Human and Human and Human.Health > 0 and not InSafeZone(v) and not CollectionService:HasTag(v,"Ally"..Client.Name) and (Settings.Weapon == "Melee" and v.Data.DevilFruit.Value ~= "Rubber-Rubber" or Settings.Weapon == "Sword" and v.Data.DevilFruit.Value ~= "Chop-Chop") then
                        if v.Data.Level.Value > 20 and math.abs(v.Data.Level.Value - ClientData.Level.Value) < 100 then
                            IsPlayerHuntAvailable = true
                            AvailablePlayer[v.Name] = true
                        end
                    end
                end
            end
        end
    end)
    -- 1sec Thread Speed
    task.spawn(function()
        while wait(1) do
            if breaker then break end
            -- Auto Save
            saveConfig()

            -- Check Is Fruit in Sever
            FruitInServer = getFruitDrop()
        end
    end)
    -- Auto Drop Fruit
    task.spawn(function()
        while wait(.75) do
            if Settings.AutoStoreFruit then
                if not DoNotStore or Char.Humanoid.Health <= 0 then
                    StoreFruit()
                end
            end
            if Settings.AutoDropFruit then
                for i,v in pairs(Settings.DropFruit or {}) do
                    if v then
                        for _,Fruit in pairs(Client.Backpack:GetChildren()) do
                            if Fruit.ToolTip ~= "Blox Fruit" and Fruit.Name:lower():find(i:lower()) and Fruit.Name:lower():find("fruit") then
                                pcall(function()
                                    Equip(Fruit)
                                    wait(.1)
                                    Fruit:FindFirstChild("EatRemote"):InvokeServer("Drop")
                                    wait(.1)
                                    Fruit.Parent = game
                                    delay(60,function()
                                        if Fruit.Parent == game then
                                            Fruit.Parent = workspace
                                        end
                                    end)
                                end)
                            end
                        end
                    end
                end
            end
        end
    end)
    -- Anti AFK
    task.spawn(function(InitializeService)
        for i,v in pairs(getconnections(Client.Idled)) do
            v:Disable() 
        end
        Client.Idled:connect(function()
            game:GetService("VirtualUser"):Button2Down(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
            wait(1)
            game:GetService("VirtualUser"):Button2Up(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
        end)
        while wait(300) do
            game:GetService("VirtualUser"):Button2Down(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
            wait(1)
            game:GetService("VirtualUser"):Button2Up(Vector2.new(0,0),workspace.CurrentCamera.CFrame)
        end
    end)
    -- Initialize Fast Attack .
    task.spawn(function()
        local Data = Combat
        local Blank = function() end
        local RigEvent = game:GetService("ReplicatedStorage").RigControllerEvent
        local Animation = Instance.new("Animation")
        local RecentlyFired = 0
        local AttackCD = 0
        local Controller
        local lastFireValid = 0
        local MaxLag = 350
        fucker = 0.07
        TryLag = 0
        local resetCD = function()
            local WeaponName = Controller.currentWeaponModel.Name
            local Cooldown = {
                combat = 0.07
            }
            AttackCD = tick() + (fucker and Cooldown[WeaponName:lower()] or fucker or 0.285) + ((TryLag/MaxLag)*0.3)
            RigEvent.FireServer(RigEvent,"weaponChange",WeaponName)
            TryLag += 1
            task.delay((fucker or 0.285) + (TryLag+0.5/MaxLag)*0.3,function()
                TryLag -= 1
            end)
        end

        if not shared.orl then shared.orl = RL.wrapAttackAnimationAsync end
        if not shared.cpc then shared.cpc = PC.play end
        if not shared.dnew then shared.dnew = DMG.new end
        if not shared.attack then shared.attack = RigC.attack end
        RL.wrapAttackAnimationAsync = function(a,b,c,d,func)
            if not Settings.NoAttackAnimation and not NeedAttacking then
                PC.play = shared.cpc
                return shared.orl(a,b,c,65,func)
            end
            local Radius = (Settings.DamageAura and Settings.DamageAuraRadius) or 65
            if canHits and #canHits > 0 then
                PC.play = function() end
                a:Play(0.00075,0.01,0.01)
                func(canHits)
                wait(a.length * 0.5)
                a:Stop()
            end
        end

        while RunService.Stepped:Wait() do
            if #canHits > 0 then
                Controller = Data.activeController
                if NormalClick then
                    pcall(task.spawn,Controller.attack,Controller)
                    continue
                end
                if Controller and Controller.equipped and (not Char.Busy.Value or Client.PlayerGui.Main.Dialogue.Visible) and Char.Stun.Value < 1 and Controller.currentWeaponModel then
                    if (NeedAttacking or Settings.DamageAura) then
                        if Settings.NewFastAttack and tick() > AttackCD and not DisableFastAttack then
                            resetCD()
                        end
                        if tick() - lastFireValid > 0.5 or not Settings.FastAttack then
                            Controller.timeToNextAttack = 0
                            Controller.hitboxMagnitude = 65
                            pcall(task.spawn,Controller.attack,Controller)
                            lastFireValid = tick()
                            continue
                        end
                        local AID3 = Controller.anims.basic[3]
                        local AID2 = Controller.anims.basic[2]
                        local ID = AID3 or AID2
                        Animation.AnimationId = ID
                        local Playing = Controller.humanoid:LoadAnimation(Animation)
                        Playing:Play(0.00075,0.01,0.01)
                        RigEvent.FireServer(RigEvent,"hit",canHits,AID3 and 3 or 2,"")
                        -- AttackSignal:Fire()
                        delay(.5,function()
                            Playing:Stop()
                        end)
                    end
                end
            end
        end
    end)
    -- Noclip - Frame to Frame Thread Speed
    task.spawn(function()
        AllCharacterPart = {}
        while game:GetService("RunService").Stepped:Wait() do
            if not a and (Settings.AutoFarm or Priority.Activity or NeedNoclip) and Char and Char:FindFirstChild("Humanoid") and #AllCharacterPart > 0 then
                if Current_Exploit("Electron") or IsValyse then
                    for i,v in pairs(AllCharacterPart) do
                        v.CanCollide = false
                    end
                    if not game.Players.LocalPlayer.Character.HumanoidRootPart:FindFirstChild("BodyClip") then
						local Noclip = Instance.new("BodyVelocity")
						Noclip.Name = "BodyClip"
						Noclip.Parent = game.Players.LocalPlayer.Character.HumanoidRootPart
						Noclip.MaxForce = Vector3.new(100000,100000,100000)
						Noclip.Velocity = Vector3.new(0,0,0)
					end
                else
                    -- workspace.Gravity = 0
                    Char.Humanoid.Sit = false
                    Char.Humanoid:ChangeState(11)
                    for i,v in pairs(AllCharacterPart) do
                        v.CanCollide = false
                    end
                end
            end
            if not Settings.AutoFarm or SKIPTP then

                -- workspace.Gravity = 196.19999694824
            end
        end
    end)
    -- Auto Stats
    task.spawn(function()
        if not Settings.AutoStats then Settings.AutoStats = {} end
        while wait(.1) do
            local KaitanIsEnable = Settings.KaitanSword or Settings.KaitanGun or Settings.KaitanFruit
            if Client.Data.Points.Value >= 1 then
                if (Settings.AutoStats.Melee or KaitanIsEnable) and Client.Data.Stats.Melee.Level.Value < MAXLEVEL  then
                    _stat("Melee",Client.Data.Points.Value)
                    continue
                end
                if (Settings.AutoStats.Defense or KaitanIsEnable) and Client.Data.Stats.Defense.Level.Value < MAXLEVEL then
                    _stat("Defense",Client.Data.Points.Value)
                    continue
                end
                if (Settings.AutoStats.Sword or Settings.KaitanSword) and Client.Data.Stats.Sword.Level.Value < MAXLEVEL then
                    _stat("Sword",Client.Data.Points.Value)
                    continue
                end
                if (Settings.AutoStats.Fruit or Settings.KaitanFruit) and Client.Data.Stats["Demon Fruit"].Level.Value < MAXLEVEL then
                    _stat("Demon Fruit",Client.Data.Points.Value)
                    continue
                end
                if (Settings.AutoStats.Gun or Settings.KaitanGun) and Client.Data.Stats.Gun.Level.Value < MAXLEVEL then
                    _stat("Gun",Client.Data.Points.Value)
                end
            end
        end
    end)

    -- Auto Buy Items
    task.spawn(function()
        while wait(1) do
            if Settings.AutoLegendarySword and SecondSea then
                _C("LegendarySwordDealer","2")
            end
            if Settings.AutoHakiColors and not FirstSea then
                _C("ColorsDealer","2")
            end
            if Settings.AutoRandomFruit then
                _C("Cousin","Buy")
            end
            if Settings.AutoBuySoru and not _hasTag("Soru") and (not Settings.AutoFarm or ClientData.Level.Value >= 1800) then
                _C("BuyHaki","Soru")
            end
            if Settings.AutoBuyBuso and not _hasTag("Buso") and (not Settings.AutoFarm or ClientData.Level.Value >= 1800) then
                _C("BuyHaki","Buso")
            end
            if Settings.AutoBuyGeppo and not _hasTag("Geppo") and (not Settings.AutoFarm or ClientData.Level.Value >= 1800) then
                _C("BuyHaki","Geppo")
            end
            if Settings.AutoBuyKen and not _hasTag("Ken") and (not Settings.AutoFarm or ClientData.Level.Value >= 1800) then
                _C("KenTalk","Buy")
            end
            if Settings.AutoKabucha and not _hasItem("Kabuca") and (ClientData.Fragments.Value >= 1500) and (not Settings.AutoFarm or ClientData.Level.Value >= 1800) and not SecondSea then
                _C("BlackbeardReward","Slingshot","2")
            end
            if Settings.AutoBuyBone and (not Settings.AutoCDK or _hasItem("Cursed Dual Katana")) then
                _C("Bones","Buy",1,1)
            end
            if Settings.AutoTryLuck then
                _C("gravestoneEvent",1)
            end
        end
    end)
end


-- Auto Raid
task.spawn(function()
    if FirstSea then return end
    local RaidID
    local RaidValue = Priority:get("Raiding")
    JustStarted = false
    while wait(1) do
        if FirstSea then break end
        if ClientData.Level.Value < 1100 then continue end
        if not Char or not Root or not Char:FindFirstChild("Humanoid") then continue end
        if Char.Humanoid.Health < 1 then continue end
        if not RaidValue:check() then continue end
        if (Settings.LockFragments and Client.Data.Fragments.Value >= Settings.LockFragmentsAmount) and not ForceRaid then
            if Settings.LockFragmentsKick then
                StopAutoRejoin = true
                Client:Kick("Fragments Reached")
            end
            continue
        end
        if (Settings.AutoStartRaid or ForceRaid) and not IsRaiding() then
            local AvailableFruit = tick() - StoredSuccessFully > 0.5 and _hasFruit()
            if Client.Data.Level.Value < math.clamp(Settings.AutoStartRaidLevel or 1100,1100,1/0) and not AvailableFruit then DoNotStore = false continue end
            if RaidValue:check() and not workspace:FindFirstChild("Message") then	
                DoNotStore = true
                if not Char or not Root or Char.Humanoid.Health < 1 then continue end
                if not AvailableFruit and not _hasChip() then
                    if not _hasFruit() then
                        for i,v in pairs(game:GetChildren()) do
                            if v:IsA("Tool") then
                                v.Parent = workspace
                            end
                        end
                        if not CollectFruit() then
                            if _C("Cousin","Buy") ~= 1 then
                                local Fruits = _C("getInventoryFruits")
                                local Cheapest = {Price = 1/0}
                                for i,v in pairs(Fruits or {}) do
                                    if v.Price < (tonumber(Settings.FruitPrice) or 1000000) and v.Price < Cheapest.Price then
                                        Cheapest = v
                                    end
                                end
                                if Cheapest.Name then
                                    _C("LoadFruit",Cheapest.Name)
                                end
                            end
                        end
                    end
                end
                wait(0.75)
                local Data
                if not Char or not Root or Char.Humanoid.Health < 1 then continue end
                if not _hasChip() and not IsRaiding() and RaidValue:check() then
                    if Client.Data.DevilFruit.Value ~= "" then
                        local FruitName = RaidFruitName(Client.Data.DevilFruit.Value)
                        Data = _C("RaidsNpc","Select",(Settings.RaidMicroship == "CurrentFruit" and Client.Data.DevilFruit.Value ~= "" and table.find(RaidMicroship,FruitName) and FruitName) or RaidFruitName(Settings.RaidMicroship ~= "CurrentFruit" and Settings.RaidMicroship or "Dark"))
                    else
                        Data = _C("RaidsNpc","Select","Dark")
                    end
                    StartFragments = ClientData.Fragments.Value
                    RaidValue:set(true)
                end
                wait(1)
                if not Char or not Root or Char.Humanoid.Health < 1 then continue end
                DoNotStore = false
                if _hasChip() and not IsRaiding() and RaidValue:check() then
                    RaidValue:set(true)
                    
                    fireclickdetector(workspace.Map:FindFirstChild("RaidSummon2",true).Button.Main.ClickDetector)
                    local ID = game:GetService("HttpService"):GenerateGUID()
                    RaidID = ID
                    JustStarted = true 
                    task.delay(60,function()
                        if RaidID == ID then
                            JustStarted = false
                        end
                    end)
                end
                if (Settings.AutoStartRaid or ForceRaid) and not IsRaiding() and not JustStarted then
                    wait(.25)
                    if not AvailableFruit and Data ~= 1 and not (type(Data) == "string" and Data:find("already")) and not JustStarted and not IsRaiding() and Settings.AutoRaidHop and not _hasChip() and not _hasFruit() and RaidValue:check() then Serverhop("Auto Raid") continue end
                end
            end
        end
        if (Settings.AutoRaid or ForceRaid) and IsRaiding() then
            RaidValue:set()
            
            local Rif = RaidInfo()
            repeat
                Rif = RaidInfo()
                RaidValue:set()
                
                task.wait(0.02)
            until Rif.ID or not (Settings.AutoRaid or ForceRaid) or not IsRaiding()
            wait(1)
            if not (Settings.AutoRaid or ForceRaid) then
                RaidValue:clear()
                continue
            end
            local Success,Error = pcall(function()
                repeat
                    NeedNoclip = true
                    Rif.new()
                    RaidValue:set()
                    if Rif.LastestIsland then
                        tp(Rif.LastestIsland.CFrame * CFrame.new(0,50,25),function()
                            return (Settings.AutoRaid or ForceRaid) and RaidValue:isActive()
                        end,true,true,RaidValue)
                        for i,v in pairs(workspace.Enemies:GetChildren()) do
                            local Human = v:FindFirstChildOfClass("Humanoid")
                            if Human and Human.Health > 0 and Human.RootPart then
                                if not Settings.KillAura or (not isnetworkowner(Human.RootPart) and dist(Human.RootPart.Position) <= 1000) then
                                    repeat
                                        RaidValue:set()
                                        Buso()
                                        local POS = Human.RootPart.CFrame
                                        tp(CFrame.new(POS.X,math.clamp(POS.Y,0,1/0),POS.Z) * CFrame.new(math.random(-2,2),40,math.random(-2,2)),function()
                                            return (Settings.AutoRaid or ForceRaid) and IsRaiding() and Client.Character.Humanoid.Health > 0 and RaidValue:isActive()
                                        end,true,true,RaidValue)
                                        NeedAttacking = true
                                        Equip(GetToolFromTip(Settings.Weapon))
                                        task.wait(0.02)
                                    until not Human or v.Parent ~= workspace.Enemies or (isnetworkowner(Human.RootPart) and Settings.KillAura) or not RaidValue:isActive()
                                    
                                    NeedAttacking = false
                                end
                            end
                        end
                    end
                    task.wait(0.02)
                until not (Settings.AutoRaid or ForceRaid) or not IsRaiding() or Client.Character.Humanoid.Health <= 0 or not RaidValue:isActive()
            end)
            if not Success then
                warn("Raid Error Send this yellow message to mexuaita\n",Error)
            end
            repeat Rif.new() wait() until not Rif.ID or not Rif.ID.Parent or not IsRaiding()
            local Area = InArea(Root.Position)
            repeat
                Area = InArea(Root.Position)
                RaidValue:set()
                wait(.2)
            until Area and not Area.Name:find("Island") or not IsRaiding()
            workspace.NPCs:WaitForChild("Mysterious Entity",2)
            repeat wait() until not workspace.NPCs:FindFirstChild("Mysterious Entity")
            NeedNoclip = false
            JustStarted = false
            RaidValue:clear()
        end
    end
end)

task.spawn(function()
    ClientData.Level.Changed:Connect(function()
        if (Settings.AutoRedeemCodeOnLevel or 100) <= ClientData.Level.Value and not Redeemed then
            if ClientData.Level.Value > (Settings.LockLevel and Settings.LockLevelValue or MAXLEVEL)-50 then return end
            local function UseCode(Text)
                game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(Text)
            end
            for i,v in pairs({
                "GAMERROBOT_YT",
                "EXP_5B",
                "kittgaming",
                "Enyu_is_Pro",
                "Sub2Fer999",
                "THEGREATACE",
                "SUB2GAMERROBOT_EXP1",
                "Sub2OfficialNoobie",
                "StrawHatMaine",
                "SUB2NOOBMASTER123",
                "Sub2Daigrock",
                "Axiore",
                "TantaiGaming",
                "STRAWHATMAINE",
                "JCWK",
                "Magicbus",
                "Starcodeheo",
                "Bluxxy",
            }) do
                task.spawn(UseCode,v)
            end
            Redeemed = true
        end
    end)
    Funcs.KillAura = function()
        task.spawn(function()
            if FirstSea then return end
            while Settings.KillAura and wait() do
                if IsRaiding() then
                    for i,v in pairs(workspace.Enemies:GetChildren()) do
                        local Human = v:FindFirstChildOfClass("Humanoid")
                        if Human and Human.Health > 0 and Human.RootPart then
                            if isnetworkowner(Human.RootPart) then
                                Human.Health = 1
                                Human.Health = 0
                            end
                        end
                    end
                end
            end
        end)
    end
    Funcs.AutoFarm = function()
        local function levelFarm(NoPredict)
            return FORCE_LEVEL or Settings.CustomLevelFarm and math.clamp(Settings.CustomLevelFarmValue,MinLevelOfSea,NoPredict and ClientData.Level.Value or ac_lvl()) or NoPredict and ClientData.Level.Value or ac_lvl()
        end
        local function Expression()
            return not Priority.Activity and Settings.AutoFarm and not IsRaiding() and not AvailablePlayer[QuestTargetName]
        end
        local PlayerHuntCooldown = 0
        local PlayerHuntQuestCooldown = 0
        task.spawn(function()
            while Settings.AutoFarm do task.wait()
                pcall(function()
                    if not Priority.Activity and not IsRaiding() and Char and Root then
                        if (not QuestData or not CorrectQuest) and (not IsPlayerHuntAvailable or tick() - PlayerHuntQuestCooldown < 60) then
                            cancelQuest()
                            local level = levelFarm()
                            local ExpTime = tick()
                            local ExpNow = Client.Data.Exp.Value
                            local CalcuLevel = FORCE_LEVEL or level
                            repeat 
                                local rate = tick() - ExpTime > 1.75
                                if rate and ClientData.Exp.Value == ExpNow and ClientData.Exp.Value >= Exp_Calc(ClientData.Level.Value) then
                                    CalcuLevel = levelFarm(true)
                                    UpdateQuestData(CalcuLevel,SecondQuest)
                                end
                                if not rate and (FORCE_LEVEL or level) ~= CalcuLevel then 
                                    task.wait()
                                    continue
                                end
                                if (QuestData and not CorrectQuest) then
                                    UpdateQuestData(CalcuLevel,SecondQuest)
                                    cancelQuest()
                                end
                                local v = _getNearest(QuestTargetName)
                                if v == "Bandit" then
                                    QUESTPOS = CFrame.new(1059.37195, 15.4495068, 1550.4231, 0.939700544, -0, -0.341998369, 0, 1, -0, 0.341998369, 0, 0.939700544)
                                    tp(QUESTPOS,Expression,nil,nil,"AutoFarm")
                                else
                                    tp(QUESTPOS,Expression,nil,nil,"AutoFarm")
                                end
                                if dist(QUESTPOS.p) <= 50 and Char and Root then
                                    if BOSSNAME and _getNearest(BOSSNAME,nil,nil,1750) then
                                        _C("StartQuest",BOSSQUESTNAME,BOSSQUESTNUMBER)
                                    else
                                        _C("StartQuest",QUESTNAME,QUESTNUMBER)
                                    end
                                end
                                wait()
                            until not Settings.AutoFarm or QuestData or (IsPlayerHuntAvailable and tick() - PlayerHuntQuestCooldown >= 60) or Priority.Activity or IsRaiding()
                        elseif ClientData.Level.Value > 75 or not Settings.SkylandKill or ClientData.Level.Value <= 20 then
                            if ClientData.Level.Value >= 1000 or not Settings.PlayerHunt or ((not IsPlayerHuntAvailable or tick() - PlayerHuntQuestCooldown < 60) and not TargetIsPlayer) then
                                local v = _getNearest(QuestTargetName)
                                print("QuestTargetName",QuestTargetName)
                                if not v then
                                    for _,NPC in pairs(FindNPC(QuestTargetName,Expression)) do
                                        v = NPC.Spawned
                                        if v then break end
                                        if not NPC.InArea then
                                            NPC.toSpawn()
                                            break
                                        end
                                    end
                                end
                                if Entity.IsAlive(v) then
                                    print("v",v)
                                    Entity.Attack(v,nil,Expression,{
                                        Quest = true
                                    })
                                else
                                    if Client.Data.Level.Value > 10 then 
                                        for i,Value in pairs(workspace["_WorldOrigin"].EnemySpawns:GetChildren()) do
                                            if Value.Name == QuestTargetName or Value.Name:match(QuestTargetName) then 
                                                repeat wait() 
                                                    if not Settings.AutoFarm then
                                                        break
                                                    end
                                                    tp(Value.CFrame * CFrame.new(0,50,0),Expression,nil,nil,"AutoFarm")
                                                until Entity.IsAlive(v) or (Value.CFrame.Position - game:GetService("Players").LocalPlayer.Character:WaitForChild("HumanoidRootPart").Position).magnitude <= 70
                                            end
                                        end
                                    end
                                end
                            else
                                if QuestData and AvailablePlayer[QuestTargetName] then
                                    local v = Players[QuestTargetName].Character
                                    local Human = Entity.IsAlive(v)
                                    local CS = 1
                                    local CSStart = 0
                                    if Human then
                                        pcall(function()
                                            local Expression = function()
                                                return not Human.Parent or Human.Health <= 0 or Priority.Activity or not Settings.AutoFarm or IsRaiding() or not AvailablePlayer[QuestTargetName] and QuestData
                                            end
                                            repeat 
                                                NeedAttacking = true
                                                if Client:GetAttribute("PvpDisabled") then
                                                    _C("EnablePvp")
                                                end
                                                tp(CFrame.new(Human.RootPart.Position + Vector3.new(math.random(-3,3),0,math.random(-3,3))),function()
                                                    return not Expression()
                                                end,nil,nil,"AutoFarm")
                                                if tick() - CSStart > 0.25 then
                                                    CSStart = tick()
                                                    CS = CS + 1
                                                    if CS > #Step then
                                                        CS = 1
                                                    end
                                                end
                                                Equip(GetToolFromTip(Settings.Weapon))
                                                Buso()
                                                task.wait()
                                            until Expression()
                                            NeedAttacking = false
                                        end)
                                    end
                                    wait(1)
                                    if ClientData.Exp.Value - Exp_Calc(ClientData.Level.Value) > tonumber("1e+5") then
                                        local v = _getNearest("NOPLAYER")
                                        if Entity.IsAlive(v) then
                                            Entity.Attack(v,nil,Expression)
                                        end
                                    end
                                elseif tick() - PlayerHuntCooldown > 0.15 then
                                    PlayerHuntCooldown = tick()
                                    if (_C("PlayerHunter") or "Come back later."):find("Come back later.") then
                                        PlayerHuntQuestCooldown = tick()
                                    end
                                end
                            end
                        else
                            local NPC,v = FindNPC({"Shanda","Royal Soldier","Royal Squad"},Expression)
                            for _,NPC in pairs(NPC) do
                                v = NPC.Spawned
                                if v then break end
                                if not NPC.InArea then
                                    NPC.toSpawn()
                                    break
                                end
                            end
                            if Entity.IsAlive(v) then
                                Entity.Attack(v,nil,Expression)
                            end
                        end
                    end
                end)
            end
        end)
    end
    Funcs.AutoSnipeFruit = function()
        task.spawn(function()
            while Settings.AutoSnipeFruit and wait(.1) and ClientData.DevilFruit.Value == "" do
                local AvailableFruit = _C("GetFruits")
                for i,v in pairs(Settings.SnipeFruit or {}) do
                    for _,Fruit in pairs(AvailableFruit) do
                        if Fruit.OnSale and ClientData.Beli.Value >= Fruit.Price then
                            if Fruit.Name:lower() == toServerFruit(i):lower() then
                                _C("PurchaseRawFruit",Fruit.Name,false)
                            end
                        end
                    end
                end
            end
        end)
    end
    Funcs.AutoEatFruit = function()
        task.spawn(function()
            if ClientData.DevilFruit.Value == "" then
                while Settings.AutoEatFruit and wait(.1) do
                    if Settings.AutoEatFruit and not AlreadyEat then
                        for i,v in pairs(Settings.EatFruit or {}) do
                            if v then
                                for _,Fruit in pairs(Client.Backpack:GetChildren()) do
                                    if Fruit.ToolTip ~= "Blox Fruit" and Fruit.Name:lower():find(i:lower()) and Fruit.Name:lower():find"fruit" then
                                        Equip(Fruit)
                                        AlreadyEat = true
                                        Fruit:FindFirstChild("EatRemote"):InvokeServer()
                                        break
                                    end
                                end
                                for _,ServerFruit in pairs(_C("getInventoryFruits") or {}) do
                                    if ServerFruit.Name:lower() == toServerFruit(i):lower() then
                                        _C("LoadFruit",ServerFruit.Name)
                                        break
                                    end
                                end
                            end
                        end
                    end
                end
            end
        end)
    end
    Funcs.AutoGodhuman = function()
        task.spawn(function()
            local Success,Data = pcall(_C,"BuyGodhuman",not LaunchedSuccessfully)
            if Data == 1 or Data == 2 then
                wait()
                Finished.Superhuman = true
                return
            end
            while Settings.AutoGodhuman and wait(.5) do
                if Settings.AutoGodhuman and Finished.ElecticClaw and Finished.DragonTalon and Finished.DeathStep and Finished.Superhuman and Finished.SharkmanKarate then
                    if not checkIsAvailable("ElectricClaw",400) then continue end
                    if not checkIsAvailable("DeathStep",400) then continue end
                    if not checkIsAvailable("SharkmanKarate",400) then continue end
                    if not checkIsAvailable("DragonTalon",400) then continue end
                    if not checkIsAvailable("Superhuman",400) then continue end
                    if _C("BuyGodhuman",true) == 0 then
                        if Client.Data.Fragments.Value >= 5000 and not IsRaiding() then
                            if ClientData.Beli.Value >= tonumber("5e+6") then
                                ForceRaid = false
                                if purchaseCombat("Godhuman") then
                                    Finished.Godhuman = true
                                    return
                                end
                            end
                        else
                            ForceRaid = true
                        end
                    end
                end
            end
        end)
    end 
    Funcs.AutoSuperhuman = function()
        task.spawn(function()
            local Success,Data = pcall(_C,"BuySuperhuman",not LaunchedSuccessfully)
            if Data == 1 or Data == 2 then
                Finished.Superhuman = true
                return
            end
            while Settings.AutoSuperhuman and wait(.5) do
                if not checkIsAvailable("Electro",300) then continue end
                if not checkIsAvailable("BlackLeg",300) then continue end
                if not checkIsAvailable("FishmanKarate",300) then continue end
                if not checkIsAvailable("DragonClaw",300) then 
                    ForceRaid = not purchaseCombat("DragonClaw")
                    continue
                end
                ForceRaid = false
                if ClientData.Beli.Value >= tonumber("3e+6") then
                    if purchaseCombat("Superhuman") then
                        Finished.Superhuman = true
                        ForceRaid = false
                        return
                    elseif ClientData.Fragments.Value < 5000 and not Finished.Superhuman then
                        ForceRaid = true
                    end
                end
            end
        end)
    end
    Funcs.AutoSharkmanKarate = function()
        local SharkmanValue = Priority:get("AutoSharkmanKarate")
        task.spawn(function()
            local Success,Data = pcall(_C,"BuySharkmanKarate",not LaunchedSuccessfully)
            if Data == 1 or Data == 2 then
                wait()
                Finished.SharkmanKarate = true 
                Finished.TrueSharkmanKarate = true 
                return
            end
            local UsedKey = Data
            SharkmanBossAttacked = Data == 3
            if not SharkmanBossAttacked and not SecondSea then return end
            while Settings.AutoSharkmanKarate and wait(2) do
                if Finished.TrueSharkmanKarate then break end
                if Settings.AutoSharkmanKarate and (Finished.Superhuman or not Settings.AutoSuperhuman) then
                    UsedKey = _C("BuySharkmanKarate",true)
                    SharkmanBossAttacked = UsedKey == 3
                    if SharkmanValue:check() and not SharkmanBossAttacked and SecondSea then
                        SharkmanValue:clear()
                        local v = _getNearest("Tide Keeper")
                        if (not Settings.AutoFarm and ClientData.Level.Value > 1100 or ClientData.Level.Value >= 1500) and not v and Settings.AutoDeathStep and not Finished.DeathStep and NoDeathStepBoss then -- and Settings.AutoDeathStepHop) then
                            Serverhop("Auto DeathStep")
                        end
                        if ((ClientData.Level.Value > 1100 and not Settings.AutoFarm) or (ClientData.Level.Value >= 1500)) and not v then -- and Settings.AutoSharkmanKarateHop then
                            Serverhop("Auto SharkmanKarate")
                        end
                        if Entity.IsAlive(v) then
                            Entity.Attack(v,SharkmanValue,function()
                                return Settings.AutoSharkmanKarate and not _hasItem("Water Key")
                            end)
                        end
                        if _hasItem("Water Key") then
                            UsedKey = _C("BuySharkmanKarate",true)
                        end
                    elseif SharkmanBossAttacked and (Finished.DeathStep or not Settings.AutoDeathStep) and (Finished.DeathStep or NoDeathStepBoss or DeathStepBossAttacked or not Settings.AutoDeathStep) and (Finished.ElecticClaw or not Settings.AutoElectricClaw or SecondSea) then
                        pcall(function()
                            local Data = MasteryData.SharkmanKarate or _C("BuyFishmanKarate")
                            if SecondSea and Settings.AutoThirdSea and Settings.AutoThirdSeaHop then
                                Finished.SharkmanKarate = true
                            end
                            if type(Data) == "number" and (Data == 1 or Data == 2 or Data > 100) and (MasteryData.SharkmanKarate or GetToolFromTip("Fishman Karate",true):WaitForChild("Level").Value) >= 400 then	
                                MasteryData.SharkmanKarate = 400
                                if Client.Data.Fragments.Value >= 5000 and not IsRaiding()  then
                                    ForceRaid = false
                                    if purchaseCombat("SharkmanKarate") then
                                        Finished.SharkmanKarate = true
                                        Finished.TrueSharkmanKarate = true
                                        wait()
                                        pcall(EquipBest)
                                        SharkmanValue:clear()
                                        return
                                    end
                                else
                                    if not Settings.AutoThirdSea or not SecondSea then
                                        ForceRaid = true
                                    end
                                end
                            end
                        end)
                    end
                end
            end
        end)
    end
    Funcs.AutoDeathStep = function()
        local DeathValue = Priority:get("AutoDeathStep")
        task.spawn(function()
            local UsedKey = _C("OpenLibrary")
            DeathStepBossAttacked = UsedKey
            if not UsedKey and not SecondSea then return end
            local Data = _C("BuyDeathStep",not LaunchedSuccessfully)
            if Data == 1 or Data == 2 then 
                Finished.DeathStep = true
                wait()
                return 
            end
            while Settings.AutoDeathStep and wait(0.75) do
                if Settings.AutoDeathStep then
                    if DeathValue:check() and not UsedKey and SecondSea then
                        DeathValue:clear()
                        UsedKey = _C("OpenLibrary")
                        DeathStepBossAttacked = UsedKey
                        local v = _getNearest("Awakened Ice Admiral")
                        if not v and Settings.AutoSharkmanKarate and not SharkmanBossAttacked then 
                            NoDeathStepBoss = true
                            continue
                        end
                        if ((ClientData.Level.Value > 1100 and not Settings.AutoFarm) or (ClientData.Level.Value >= 1500)) and not v then -- and Settings.AutoDeathStepHop then
                            Serverhop("Auto DeathStep")
                        end
                        if Entity.IsAlive(v) then
                            Entity.Attack(v,DeathValue,function()
                                return Settings.AutoDeathStep and not _hasItem("Library Key")
                            end)
                        end
                        if _hasItem("Library Key") then
                            UsedKey = _C("OpenLibrary")
                        end
                    elseif UsedKey and (Finished.ElecticClaw or not Settings.AutoElectricClaw or SecondSea) and (Finished.Superhuman or not Settings.AutoSuperhuman) then
                        local Success,Data = true
                        if not MasteryData.DeathStep then
                            Success,Data = pcall(_C,"BuyBlackLeg")
                        else
                            Data = MasteryData.DeathStep
                        end
                        if not GetToolFromTip("Black Leg",true) then continue end
                        if type(Data) == "number" and (Data == 1 or Data == 2 or Data > 100) and (MasteryData.DeathStep or GetToolFromTip("Black Leg",true):WaitForChild("Level").Value) >= 400 then	
                            MasteryData.DeathStep = 400
                            if SecondSea and Settings.AutoThirdSea and Settings.AutoThirdSeaHop then
                                Finished.DeathStep = true
                            end
                            if Client.Data.Fragments.Value >= 5000 and not IsRaiding() then
                                ForceRaid = false
                                if purchaseCombat("DeathStep") then
                                    Finished.DeathStep = true
                                    wait()
                                    pcall(EquipBest)
                                    break
                                end
                            elseif not Settings.AutoThirdSea or not SecondSea then
                                ForceRaid = true
                            end
                        end
                    end
                end
            end
        end)
    end
    Funcs.AutoElectricClaw = function()
        local ElecticClawValue = Priority:get("AutoElectricClaw")
        task.spawn(function()
            local Success,Data = pcall(_C,"BuyElectricClaw",not LaunchedSuccessfully)
            if Success then
                if Data == 1 or Data == 2 then 
                    Finished.ElecticClaw = true
                    wait()
                    return 
                end
            end
            while Settings.AutoElectricClaw and wait(0.5) do
                if not ThirdSea then Finished.ElecticClaw = true break end
                if Settings.AutoElectricClaw and (Finished.Superhuman or not Settings.AutoSuperhuman) then
                    if not checkIsAvailable("BuyElectro",400) then continue end
                    local Tool = GetToolFromTip("Electro",true)
                    if Tool and type(Data) == "number" and (MasteryData.Electro or Tool.Level.Value) >= 400 and not IsRaiding() then
                        MasteryData.Electro = 400
                        if not ThirdSea then
                            Finished.ElecticClaw = true
                        end
                        if _C("BuyElectricClaw",true) ~= 4 then
                            if Client.Data.Fragments.Value >= 5000 and not IsRaiding() then
                                if ClientData.Beli.Value >= tonumber"3e+6" then
                                    ForceRaid = false
                                    if purchaseCombat("ElectricClaw") then
                                        if Data == 1 or Data == 2 then
                                            Finished.ElecticClaw = true
                                            wait()
                                            pcall(EquipBest)
                                            break
                                        end
                                    end
                                end
                            else
                                ForceRaid = true
                            end
                        else
                            ElecticClawValue:set()
                            unTP()
                            _C("BuyElectricClaw","Start")
                            _C("requestEntrance",Vector3.new(-12462, 375, -7552))
                            ElecticClawValue:clear()
                        end
                    end
                end
            end
        end)
    end
    Funcs.AutoDragonTalon = function()
        if not ThirdSea then return end
        task.spawn(function()
            BoneBuys = 0
            local Success,Data = pcall(_C,"BuyDragonTalon",not LaunchedSuccessfully)
            if Data == 1 or Data == 2 then
                wait()
                Finished.DragonTalon = true
                return
            end
            while Settings.AutoDragonTalon and wait(0.5) do
                if not ThirdSea then break end
                if Settings.AutoDragonTalon and (Finished.TrueSharkmanKarate or not SharkmanBossAttacked or not Settings.AutoSharkmanKarate) and (Finished.DeathStep or not DeathStepBossAttacked or not Settings.AutoDeathStep) and (Finished.Superhuman or not Settings.AutoSuperhuman) and (Finished.ElecticClaw or not Settings.AutoElectricClaw) then
                    local Success,Data = true
                    if not MasteryData.ElecticClaw then
                        Success,Data = pcall(_C,"BlackbeardReward","DragonClaw","2")
                    else
                        Success = true
                        Data = 1
                    end
                    if not GetToolFromTip("Dragon Claw",true) then continue end
                    if type(Data) == "number" and (Data == 1 or Data == 2 or (Data or 0) > 100) and (MasteryData.DragonClaw or GetToolFromTip("Dragon Claw",true):WaitForChild("Level").Value) >= 400 then
                        MasteryData.DragonClaw = 400
                        if Client.Data.Fragments.Value >= 5000 and not IsRaiding() then
                            ForceRaid = false
                            if FireES then
                                _C("BuyDragonTalon",1)
                                if _C("BuyDragonTalon") == 1 or _C("BuyDragonTalon") == 2 then
                                    _C("BuyDragonTalon")
                                    Finished.DragonTalon = true
                                    wait()
                                    pcall(EquipBest)
                                    break
                                end
                            else
                                _C("Bones","Buy",1,1)
                                BoneBuys = BoneBuys + 1
                            end
                        else
                            ForceRaid = true
                        end
                    end
                end
            end
        end)
    end
    Funcs.AutoBone = function()
        local BoneValue = Priority:get("AutoBone")
        task.spawn(function()
            if not ThirdSea then return end
            while Settings.AutoBone and task.wait(.1) do
                pcall(function()
                    if Settings.AutoBone and not IsRaiding() and BoneValue:check() then
                        NeedNoclip = true
                        local enemyNames = {
                            'Reborn Skeleton [Lv. 1975]',
                            'Living Zombie [Lv. 2000]',
                            'Demonic Soul [Lv. 2025]',
                            'Posessed Mummy [Lv. 2050]'
                        }
                        local foundEnemy = false
                        for _, v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                            if table.find(enemyNames, v.Name) then
                                if Entity.IsAlive(v) then
                                    Entity.Attack(v,BoneValue,nil,{
                                        Mastery = true,
                                    })
                                end
                                foundEnemy = true
                            end
                        end
                        if not foundEnemy then
                            tp(CFrame.new(-9504.8564453125, 172.14292907714844, 6057.259765625),function()
                                return Settings.AutoBone
                            end,false,false,BoneValue)
                        end
                    else
                        NeedNoclip = false
                    end
                end)
            end
            BoneValue:clear()
        end)
    end
    Funcs.AutoSaber = function()
        local SaberValue = Priority:get("AutoSaber")
        task.spawn(function()
            local Data = _C("ProQuestProgress")
            if Data.KilledShanks or not FirstSea then return end
            while Settings.AutoSaber and task.wait(1) do
                local Jungle = Map.Jungle
                if ac_lvl() < 200 or not SaberValue:check() then continue end
                if _hasItem("Saber") then break end
                local Data = _C("ProQuestProgress")
                if Data.KilledShanks then break end
                if not Data.KilledMob then
                    local v = _getNearest("Mob Leader")
                    if Entity.IsAlive(v) then
                        Entity.Attack(v,SaberValue,function()
                            return not _hasItem("Saber")
                        end)
                    end
                end
                if not Data.UsedRelic and Data.KilledMob then
                    repeat
                        _C("ProQuestProgress","RichSon")
                        wait()
                    until _hasItem("Relic")
                    repeat
                        _C("ProQuestProgress","PlaceRelic")
                        wait()
                    until not _hasItem("Relic")
                end
                if not Data.KilledShanks and Data.UsedRelic then
                    local v = _getNearest("Saber Expert")
                    if Entity.IsAlive(v) then
                        Entity.Attack(v,SaberValue,function()
                            return not _hasItem("Saber")
                        end)
                    else
                        Serverhop("Auto Saber")
                    end
                end
                SaberValue:clear()
            end
            SaberValue:clear()
        end)
    end
    Funcs.AutoPoleV1 = function()
        local PoleValue = Priority:get("AutoPoleV1")
        task.spawn(function()
            if _hasItem("Pole (1st Form)") then return end
            if not FirstSea then return end
            while Settings.AutoPoleV1 and task.wait(.5) do
                if Settings.AutoPoleV1 and not IsRaiding() and PoleValue:check() then
                    if ClientData.Level.Value < 475 then continue end
                    pcall(function()
                        local v = _getNearest("Thunder God")
                        if Entity.IsAlive(v) then
                            Entity.Attack(v,PoleValue)
                        else
                            Serverhop("Auto Pole V1")
                        end
                    end)
                    if _hasItem("Pole (1st Form)") then
                        break
                    end
                end
            end
            PoleValue:clear()
        end)
    end
    Funcs.AutoFactory = function()
        local FactoryValue = Priority:get("AutoFactory")
        task.spawn(function()
            if not SecondSea then return end
            while Settings.AutoFactory and task.wait(.5) do
                if Settings.AutoFactory and not IsRaiding() and FactoryValue:check() then
                    pcall(function()
                        local v = _getNearest("Core")
                        if Entity.IsAlive(v) then
                            Entity.Attack(v,FactoryValue)
                        end
                    end)
                end
            end
            FactoryValue:clear()
        end)
    end
    Funcs.AutoSecondSea = function()
        local SecondSea = Priority:get("AutoSecondSea")
        task.spawn(function()
            if not FirstSea then return end
            while Settings.AutoSecondSea and task.wait(.1) do
                repeat wait(1) until ac_lvl() >= 700
                if _C("DressrosaQuestProgress").KilledIceBoss or not FirstSea then break end
                if Settings.AutoSecondSea and not IsRaiding() and SecondSea:check() then
                    local Data = _C("DressrosaQuestProgress")
                    local Success,Error = pcall(function()
                        if not Data.TalkedDetective then
                            repeat 
                                _C("DressrosaQuestProgress","Detective") 
                                wait()
                            until Client.Backpack:FindFirstChild("Key")
                            wait()
                        end
                        if not Data.UsedKey then
                            repeat _C("DressrosaQuestProgress","Detective") 
                                wait()
                            until Client.Backpack:FindFirstChild("Key")
                            repeat _C("DressrosaQuestProgress","UseKey")
                                wait() 
                            until not Client.Backpack:FindFirstChild("Key")
                        end
                        if not Data.KilledIceBoss and Data.UsedKey then
                            local v = _getNearest("Ice Admiral")
                            if Entity.IsAlive(v) then
                                Entity.Attack(v,SecondSea)
                            end
                        end
                        if _C("DressrosaQuestProgress").KilledIceBoss then
                            _C("TravelDressrosa")
                        elseif not _C("DressrosaQuestProgress").KilledIceBoss and Settings.AutoSecondSeaHop then
                            Serverhop("Auto Second Sea")
                        end
                    end)
                    if not Success then
                        warn("Unexpected Error Found! Please send this to Mexuaita#7128\n"..Error)
                    end
                end
            end
            SecondSea:clear()
        end)
    end
    Funcs.AutoCollectFruit = function()
        task.spawn(function()
            while Settings.AutoCollectFruit and wait(.1) do
                if Settings.AutoCollectFruit and not (IsRaiding() or ForceRaid) then
                    FullyBringFruit(Settings.AutoCollectFruitHop)
                end
            end
        end)
    end
    Funcs.AutoBartiloQuest = function()
        local BartiloValue = Priority:get("AutoBartiloQuest")
        task.spawn(function()
            if not SecondSea then return end
            local Data = _C("BartiloQuestProgress")
            if Data.DidPlates or not SecondSea then FinishedBartilo = true return end
            while Settings.AutoBartiloQuest and task.wait(.5) do
                if Settings.AutoBartiloQuest then
                    if ac_lvl() < 850 or not BartiloValue:check() then continue end
                    local Data = _C("BartiloQuestProgress")
                    if Data.DidPlates then FinishedBartilo = true break end
                    if not Data.KilledBandits then
                        BartiloValue:set()
                        if not QuestData or not QuestTargetName:find("Swan") then
                            _C("StartQuest","BartiloQuest",1)
                        end
                        repeat
                            local v = _getNearest("Swan Pirate")
                            if not v then
                                local NPC = FindNPC("Swan Pirate",function()
                                    BartiloValue:set()
                                    return BartiloValue:isActive() and not FinishedBartilo and not IsRaiding()
                                end)[1]
                                v = NPC.Spawned
                                if not v then
                                    BartiloValue:set()
                                    NPC.toSpawn()
                                end
                            end
                            if Entity.IsAlive(v) then
                                Entity.Attack(v,BartiloValue,function()
                                    return QuestData and QuestTargetName:find("Swan")
                                end)
                                if (Data.KilledSpring or not Settings.AutoBartiloQuest) then
                                    BartiloValue:clear()
                                end
                            end
                            BartiloValue:set()
                            task.wait(.2)
                        until not QuestData or QuestTargetName ~= 'Swan Pirate' or not BartiloValue:isActive() or IsRaiding()
                    end
                    if not Data.KilledSpring and Data.KilledBandits then
                        local v = _getNearest("Jeremy [Lv. 850] [Boss]")
                        if Entity.IsAlive(v) then
                            Entity.Attack(v,BartiloValue)
                        else --if Settings.AutoBartiloQuestHop then
                            Serverhop("Auto Bartilo Quest")
                        end
                    end
                    if not Data.DidPlates and Data.KilledSpring then
                        _C("BartiloQuestProgress","DidPlates")
                    end
                end
            end
        end)
    end
    Funcs.AutoMidnightBlade = function()
        task.spawn(function()
            while Settings.AutoMidnightBlade and wait(.1) do
                if not SecondSea then break end
                local Electro = _C("Ectoplasm","Buy",3)
                if Electro == 1 or Electro == 2 then
                    PurchasedMidnightBlade = true
                    break
                end
            end
        end)
    end
    Funcs.AutoEvoRaceV2 = function()
        if not SecondSea then return end
        local EvoRaceValue = Priority:get("AutoEvoRaceV2")
        task.spawn(function()
            while Settings.AutoEvoRaceV2 and task.wait(1) do
                if Settings.AutoEvoRaceV2 then
                    if ac_lvl() < 850 or not EvoRaceValue:check() or ClientData.Race:FindFirstChild("Evolved") or not FinishedBartilo or ClientData.Beli.Value < 500000 or (game.Lighting.ClockTime < 18 and game.Lighting.ClockTime > 5) then continue end
                    local Data = _C("Alchemist","3")
                    if Data and Data:find("don't") then
                        local flower = {
                            workspace:FindFirstChild("Flower1"),
                            workspace:FindFirstChild("Flower2"),
                        }
                        _C("Alchemist","2")
                        if flower[1] and flower[2] and flower[1].Transparency ~= 1 and flower[2].Transparency ~= 1 then
                            DoNotHop = true
                            if _hasItem("Flower 3") then
                                pcall(function()
                                    local expression = function(flowerNum)
                                        return not _hasItem("Flower "..flowerNum) and EvoRaceValue:isActive() and Settings.AutoEvoRaceV2 and flower[flowerNum].Transparency ~= 1 and _hasItem("Flower 3")
                                    end
                                    repeat
                                        EvoRaceValue:set()
                                        tp(flower[1].CFrame,function()
                                            return expression(1)
                                        end,true,false,EvoRaceValue)
                                        if dist(flower[1].Position) < 25 then
                                            firetouchinterest(Root,flower[1],0)
                                        end
                                        wait()
                                        firetouchinterest(Root,flower[1],1)
                                    until not expression(1)
                                    repeat wait()
                                        EvoRaceValue:set()
                                        tp(flower[2].CFrame,function()
                                            return expression(2)
                                        end,true,false,EvoRaceValue)
                                        if dist(flower[2].Position) < 25 then
                                            firetouchinterest(Root,flower[2],0)
                                        end
                                        wait()
                                        firetouchinterest(Root,flower[2],1)
                                    until not expression(2)
                                end)
                                network:Send("CommF_","Alchemist","3")
                            end
                            DoNotHop = false
                        else -- if Settings.AutoEvoRaceV2Hop then
                            Serverhop("Auto Evo Race V2")
                        end
                        EvoRaceValue:clear()
                    end
                end
            end
        end)
    end
    Funcs.AutoRengoku = function()
        local RengokuValue = Priority:get("AutoRengoku")
        if not SecondSea then return end
        task.spawn(function()
            if _C("OpenRengoku") then return end
            while Settings.AutoRengoku and task.wait(.5) do
                if Settings.AutoRengoku and not IsRaiding() and RengokuValue:check() then
                    if ac_lvl() < 1350 then continue end
                    if Settings.AutoFarm and ac_lvl() < 1425 then continue end
                    local NPC,v = FindNPC({"Snow Lurker","Arctic Warrior","Awakened Ice Admiral"},function()
                        RengokuValue:set()
                        return Settings.AutoRengoku and RengokuValue:isActive() and not IsRaiding()
                    end)
                    for _,NPC in pairs(NPC) do
                        v = NPC.Spawned
                        if v then break end
                        if not NPC.InArea then
                            RengokuValue:set()
                            NPC.toSpawn()
                            break
                        end
                    end
                    if Entity.IsAlive(v) then
                        Entity.Attack(v,RengokuValue,function()
                            return not Client.Backpack:FindFirstChild("Hidden Key")
                        end)
                    end
                    if Client.Backpack:FindFirstChild("Hidden Key") then
                        FoundRengokuKey = _C("OpenRengoku")
                        RengokuValue:clear()
                        break
                    else
                        RengokuValue:set()
                    end
                end
            end
            RengokuValue:clear()
        end)
    end
    Funcs.AutoThirdSea = function()
        local ThirdSeaValue = Priority:get("AutoThirdSea")
        task.spawn(function()
            if _C("ZQuestProgress").KilledIndraBoss or not SecondSea then return end
            repeat wait(1) until Client.Data.Level.Value >= 1500
            while Settings.AutoThirdSea and task.wait(2) do
                if ThirdSeaValue:check() then
                    if Settings.AutoThirdSea and not IsRaiding() and (Finished.DeathStep or DeathStepBossAttacked or not Settings.AutoDeathStep) and (Finished.TrueSharkmanKarate or SharkmanBossAttacked or not Settings.AutoSharkmanKarate) then
                        if not _C("GetUnlockables").FlamingoAccess then
                            local Fruits = _C("getInventoryFruits")
                            local Cheapest = {Price = 1/0}
                            for i,v in pairs(Fruits) do
                                if v.Price >= 1000000 and v.Price < Cheapest.Price then
                                    Cheapest = v
                                end
                            end
                            if Cheapest.Name then
                                _C("LoadFruit",Cheapest.Name)
                                _C("TalkTrevor","1")
                                _C("TalkTrevor","2")
                                _C("TalkTrevor","3")
                            else
                                FullyBringFruit()
                            end
                        end
                        if not _C("ZQuestProgress","Check") and _C("GetUnlockables").FlamingoAccess then
                            local v = _getNearest("Don Swan")
                            if Entity.IsAlive(v) then
                                Entity.Attack(v,ThirdSeaValue,nil,{
                                    yield = function(v)
                                        if dist(v.HumanoidRootPart.Position) > 2000 then
                                            _C("requestEntrance",Vector3.new(2285, 15, 905))
                                        end
                                    end,
                                })
                            else
                                Serverhop('Auto Third Sea : Finding Don Swan')
                            end
                        end
                        if _C("ZQuestProgress","Check") then
                            local v = _getNearest("rip_indra [Lv. 1500] [Boss]")
                            if Entity.IsAlive(v) then
                                local Start,Killed = tick(),_C("ZQuestProgress").KilledIndraBoss
                                Entity.Attack(v,ThirdSeaValue,function()
                                    return not Killed
                                end,{
                                    yield = function(v)
                                        if tick() - Start > 0.5 then
                                            Start,Killed = tick(),_C("ZQuestProgress").KilledIndraBoss
                                        end
                                        if dist(v.Humanoid.RootPart.Position) > 2000 then
                                            _C("ZQuestProgress","Begin")
                                        end
                                    end,
                                })
                            end
                        end
                        if _C("ZQuestProgress").KilledIndraBoss then
                            _C("TravelZou")
                        elseif not _C("ZQuestProgress").KilledIndraBoss and Settings.AutoThirdSeaHop then
                            Serverhop("Auto Third Sea")
                        end
                    end
                end
            end
        end)
    end
    Funcs.AutoDarkDagger = function()
        local DarkDaggerValue = Priority:get("AutoDarkDagger")
        task.spawn(function()
            if _hasItem("Dark Dagger") then return end
            if not ThirdSea then return end
            while Settings.AutoDarkDagger and wait(1.5) do
                if ac_lvl() >= 2100 and DarkDaggerValue:check() then
                    if _hasItem("Dark Dagger") then break end
                    if Settings.AutoDarkDagger then
                        if Locations:WaitForChild("Battle of the Gods",1) then
                            if (tick() - recentlySpawn > 1 or MONNAME == "Factory Staff") then
                                local v = _getNearest("rip_indra True Form [Lv. 5000] [Raid Boss]")
                                if Entity.IsAlive(v) then
                                    Entity.Attack(v,DarkDaggerValue)
                                end
                            end
                        elseif Settings.AutoDarkDaggerHop then
                            Serverhop("Auto Dark Dagger")
                        end
                    end
                end
            end
        end)
    end
    Funcs.AutoHallowScythe = function()
        local AutoHallowScythe = Priority:get("AutoHallowScythe")
        task.spawn(function()
            if _hasItem("Hallow Scythe") then return end
            if not ThirdSea then return end
            while Settings.AutoHallowScythe and wait(1.5) do
                if ac_lvl() >= 1800 and AutoHallowScythe:check() and not DisableHallowScythe then
                    if _hasItem("Hallow Scythe") then break end
                    if Settings.AutoHallowScythe and not IsRaiding() then
                        pcall(function()
                            if (tick() - recentlySpawn > 1) and not KillingKatakuri then
                                local v = _getNearest("Soul Reaper")
                                if Entity.IsAlive(v) then
                                    Entity.Attack(v,AutoHallowScythe)
                                elseif not KillingKatakuri then
                                    if _hasItem("Hallow Essence") then
                                        firetouchinterest(Client.Character.Head,workspace.Map["Haunted Castle"].Summoner.Detection,0)
                                        firetouchinterest(Client.Character.Head,workspace.Map["Haunted Castle"].Summoner.Detection,1)
                                    else
                                        _C("Bones","Buy",1,1)
                                    end
                                end
                            end
                        end)
                    end
                end
            end
        end)
    end
    Funcs.AutoEliteHunter = function()
        local EliteHunterValue = Priority:get("AutoEliteHunter")
        task.spawn(function()
            if not ThirdSea then return end
            local Data = _C("EliteHunter","Progress")
            while Settings.AutoEliteHunter and task.wait(2) do
                if (Settings.AutoEliteHunter) and not IsRaiding() and EliteHunterValue:check() then
                    local Data = _C("EliteHunter","Progress")
                    if ((Data or 9999999) < 30 and Settings.AutoYama) or not Settings.AutoYama and not KillingKatakuri then
                        if Client.Backpack:FindFirstChild("God's Chalice") or Client.Character:FindFirstChild("God's Chalice") and Settings.AutoStopWhenUntilGodChalice then

                        else
                            if not (_C("EliteHunter") or "Come back later."):find("Come back later.") then
                                EliteHunterValue:set(true)
                                local v = _getNearest(QuestTargetName)
                                if Entity.IsAlive(v) then
                                    Entity.Attack(v,EliteHunterValue,nil,{
                                        yield = function()
                                            if not QuestData then
                                                _C("EliteHunter")
                                            end
                                        end
                                    })
                                end
                            elseif Settings.AutoEliteHunterHop then
                                Serverhop("Auto Elite Hunter")
                            end
                            EliteHunterValue:clear()
                        end
                    end
                end
            end
            EliteHunterValue:clear()
        end)
    end
    Funcs.AutoBuddy = function()
        local BuddyValue = Priority:get("AutoBuddy")
        task.spawn(function()
            if _hasItem("Buddy Sword") then return end
            if not ThirdSea then return end
            while Settings.AutoBuddy and task.wait(.5) do
                if Settings.AutoBuddy and not IsRaiding() and BuddyValue:check() then
                    if ac_lvl() < 2300 or KillingKatakuri then continue end
                    pcall(function()
                        local v = _getNearest("Cake Queen")
                        if Entity.IsAlive(v) then
                            Entity.Attack(v,BuddyValue)
                        elseif Settings.AutoBuddyHop then
                            -- Serverhop("Auto Buddy Sword")
                        end
                    end)
                    if _hasItem("Buddy Sword") then
                        break
                    end
                end
            end
            BuddyValue:clear()
        end)
    end
    Funcs.AutoCanvander = function()
        local CanvanderValue = Priority:get("AutoCanvander")
        task.spawn(function()
            if _hasItem("Canvander") then return end
            if not ThirdSea then return end
            while Settings.AutoCanvander and task.wait(.5) do
                if Settings.AutoCanvander and not IsRaiding() and CanvanderValue:check() then
                    if ac_lvl() < 2000 or KillingKatakuri then continue end
                    pcall(function()
                        local v = _getNearest("Beautiful Pirate")
                        if Entity.IsAlive(v) then
                            Entity.Attack(v,CanvanderValue)
                        elseif Settings.AutoCanvanderHop then
                            -- Serverhop("Auto Canvander")
                        end
                    end)
                    if _hasItem("Canvander") then
                        break
                    end
                end
            end
            CanvanderValue:clear()
        end)
    end
    Funcs.AutoYama = function()
        task.spawn(function()
            if not ThirdSea then return end
            if _hasItem("Yama") then return end
            while Settings.AutoYama and task.wait(5) do
                if Settings.AutoYama then
                    if _C("EliteHunter","Progress") >= 30 then
                        repeat
                            fireclickdetector(workspace:FindFirstChild("SealedKatana",true).Handle.ClickDetector)
                            wait(.5)
                        until not Settings.AutoYama or Client.Backpack:FindFirstChild("Yama")
                        if Client.Backpack:FindFirstChild("Yama") then break end
                    end
                end
            end
        end)
    end
    Funcs.AutoTushita = function()
        local TushitaValue = Priority:get("AutoTushita")
        task.spawn(function()
            local Data = _C("TushitaProgress")
            if Data.KilledLongma or not ThirdSea then return end
            while Settings.AutoTushita and task.wait(.1) do
                if Settings.AutoTushita and Locations:FindFirstChild("Battle of the Gods") then
                    local Data = _C("TushitaProgress")
                    if Data.KilledLongma then return end
                    pcall(function()
                        if Data.OpenedDoor then
                            local v = _getNearest("Longma")
                            if Entity.IsAlive(v) then
                                Entity.Attack(v,TushitaValue)
                            end
                        else
                            repeat
                                firetouchinterest(Char.HumanoidRootPart,workspace.Map.Waterfall.SecretRoom.Room.Door.Door.Hitbox,0)
                                firetouchinterest(Char.HumanoidRootPart,workspace.Map.Waterfall.SecretRoom.Room.Door.Door.Hitbox,1)
                                wait(.5)
                            until _hasItem("Holy Torch")
                            for i = 1,5 do
                                _C("TushitaProgress","Torch",i)
                            end
                        end
                    end)
                    TushitaValue:clear()
                end
            end
        end)
    end
    Funcs.AutoCannon = function()
        local CanonValue = Priority:get("AutoCannon")
        if not FirstSea then return end
        task.spawn(function()
            if _hasItem("Cannon") then return end
            while Settings.AutoCannon and task.wait(.1) do
                if Settings.AutoCannon and FirstSea then
                    pcall(function()
                        local v = _getNearest("Wysper")
                        if Entity.IsAlive(v) then
                            Entity.Attack(v,CanonValue)
                        end
                    end)
                end
            end
            CanonValue:clear()
        end)
    end
    Funcs.AutoBizentoV2 = function()
        local BizentoV2Value = Priority:get("AutoBizentoV2")
        if not FirstSea then return end
        task.spawn(function()
            while Settings.AutoBizentoV2 and task.wait(.1) do
                if Settings.AutoBizentoV2 and FirstSea then
                    pcall(function()
                        local v = _getNearest("Greybeard")
                        if Entity.IsAlive(v) then
                            Entity.Attack(v,BizentoV2Value)
                        end
                    end)
                end
            end
            BizentoV2Value:clear()
        end)
    end
    Funcs.AutoDragonTrident = function()
        local DragonTridentValue = Priority:get("AutoDragonTrident")
        if not SecondSea then return end
        task.spawn(function()
            if _hasItem("Dragon Trident") then return end
            while Settings.AutoDragonTrident and task.wait(.1) do
                if Settings.AutoDragonTrident and SecondSea then
                    pcall(function()
                        local v = _getNearest("Tide Keeper")
                        if Entity.IsAlive(v) then
                            Entity.Attack(v,DragonTridentValue)
                        end
                    end)
                end
            end
            DragonTridentValue:clear()
        end)
    end
    Funcs.AutoDarkCoat = function()
        local DarkCoatValue = Priority:get("AutoDarkCoat")
        if not SecondSea then return end
        task.spawn(function()
            if _hasItem("Dark Coat") then return end
            while Settings.AutoDarkCoat and task.wait(.1) do
                if Settings.AutoDarkCoat and SecondSea then
                    pcall(function()
                        local v = _getNearest("Darkbeard")
                        if Entity.IsAlive(v) then
                            Entity.Attack(v,DarkCoatValue)
                        end
                    end)
                end
            end
            DarkCoatValue:clear()
        end)
    end
    Funcs.AutoSwanGlasses = function()
        local SwanGlassesValue = Priority:get("AutoSwanGlasses")
        if not SecondSea then return end
        task.spawn(function()
            if _hasItem("Swan Glasses") then return end
            while Settings.AutoSwanGlasses and task.wait(.1) do
                if Settings.AutoSwanGlasses and SecondSea then
                    pcall(function()
                        local v = _getNearest("Don Swan")
                        if Entity.IsAlive(v) then
                            Entity.Attack(v,SwanGlassesValue)
                        end
                    end)
                end
            end
            SwanGlassesValue:clear()
        end)
    end
    Funcs.AutoSerpentBow = function()
        local SerpentBowValue = Priority:get("AutoSerpentBow")
        if not ThirdSea then return end
        task.spawn(function()
            if _hasItem("Serpent Bow") then return end
            while Settings.AutoSerpentBow and task.wait(.1) do
                if Settings.AutoSerpentBow and ThirdSea then
                    pcall(function()
                        local v = _getNearest("Island Empress")
                        if Entity.IsAlive(v) then
                            Entity.Attack(v,SerpentBowValue)
                        end
                    end)
                end
            end
            SerpentBowValue:clear()
        end)
    end
    Funcs.AutoTwinhook = function()
        local TwinhookValue = Priority:get("AutoTwinhook")
        if not ThirdSea then return end
        task.spawn(function()
            if _hasItem("Twin hook") then return end
            while Settings.AutoTwinhook and task.wait(.1) do
                if Settings.AutoTwinhook and ThirdSea then
                    pcall(function()
                        local v = _getNearest("Captain Elephant")
                        if Entity.IsAlive(v) then
                            Entity.Attack(v,TwinhookValue)
                        end
                    end)
                end
            end
            TwinhookValue:clear()
        end)
    end
    Funcs.AutoBuddySword = function()
        local BuddySwordValue = Priority:get("AutoBuddySword")
        if not ThirdSea then return end
        task.spawn(function()
            if _hasItem("Buddy Sword") then return end
            while Settings.AutoBuddySword and task.wait(.1) do
                if Settings.AutoBuddySword and ThirdSea then
                    pcall(function()
                        local v = _getNearest("Cake Queen")
                        if Entity.IsAlive(v) then
                            Entity.Attack(v,BuddySwordValue)
                        end
                    end)
                end
            end
            BuddySwordValue:clear()
        end)
    end
    Funcs.AutoCakePrince = function()
        local CakePrinceValue = Priority:get("AutoCakePrince")
        task.spawn(function()
            if not ThirdSea then return end
            while Settings.AutoCakePrince and task.wait(0.1) do
                pcall(function()
                    if Settings.AutoCakePrince and not IsRaiding() and CakePrinceValue:check() then
                        NeedNoclip = true
                        local nearestEnemy = _getNearest("Cake Prince")
                        if string.find(_C("CakePrinceSpawner"), "Do you want to open the portal now?") then
                            _C("CakePrinceSpawner")
                        end
                        if Entity.IsAlive(nearestEnemy) then
                            Entity.Attack(nearestEnemy, CakePrinceValue)
                        else
                            local enemyNames = {
                                "Cookie Crafter [Lv. 2200]",
                                "Cake Guard [Lv. 2225]",
                                "Baking Staff [Lv. 2250]",
                                "Head Baker [Lv. 2275]"
                            }
                            local enemyFound = false
                            for i,v in ipairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                if table.find(enemyNames, v.Name) then
                                    if Entity.IsAlive(v) then
                                        Entity.Attack(v, CakePrinceValue)
                                        enemyFound = true
                                        break
                                    end
                                end
                            end
                            if not enemyFound then
                                tp(CFrame.new(-2077, 252, -12373), function()
                                    return Settings.AutoCakePrince
                                end, false, false, CakePrinceValue)
                            end
                        end                        
                    else
                        NeedNoclip = false
                    end
                end)
            end
            CakePrinceValue:clear()
        end)
    end
    Funcs.TeleportIsland = function()
        local TeleportIslandValue = Priority:get("TeleportIsland")
        task.spawn(function()
            while Settings.TeleportIsland and task.wait(.1) do
                if Settings.TeleportIsland then
                    pcall(function()
                        for i,v in pairs(game:GetService("Workspace")["_WorldOrigin"].Locations:GetChildren()) do
                            if v.Name == Settings.SelectIsland then
                                tp(v.CFrame * CFrame.new(0,40,0),function()
                                    return Settings.TeleportIsland
                                end,false,false,"TeleportIsland")
                            end
                        end
                    end)
                end
            end
            TeleportIslandValue:clear()
        end)
    end
    Funcs.TeleportToGear = function()
        local TeleportToGearValue = Priority:get("TeleportToGear")
        if not ThirdSea then return end
        task.spawn(function()
            while Settings.TeleportToGear and task.wait(.1) do
                pcall(function()
                    for i,v in pairs(game:GetService("Workspace").Map:FindFirstChild('MysticIsland'):GetChildren()) do
                        if v.Name == 'Part' then
                            if v.ClassName == 'MeshPart' then
                                tp(v.CFrame,function()
                                    return Settings.TeleportToGear
                                end,nil,nil,"TeleportToGear")
                                v.Transparency = 0
                            end
                        end
                    end
                end)
            end
            TeleportToGearValue:clear()
        end)
    end
    Funcs.TeleportToTrialDoor = function()
        local TeleportToTrialDoorValue = Priority:get("TeleportToTrialDoor")
        if not ThirdSea then return end
        task.spawn(function()
            while Settings.TeleportToTrialDoor and task.wait(.1) do
                pcall(function()
                    if game.Players.LocalPlayer.Data.Race.Value == "Mink" then
                        tp(game:GetService("Workspace").Map["Temple of Time"].MinkCorridor.Door.Entrance.CFrame,function()
                            return Settings.TeleportToTrialDoor
                        end,nil,nil,"TeleportToTrialDoor")
                    elseif game.Players.LocalPlayer.Data.Race.Value == "Fishman" then
                        tp(game:GetService("Workspace").Map["Temple of Time"].FishmanCorridor.Door.Entrance.CFrame,function()
                            return Settings.TeleportToTrialDoor
                        end,nil,nil,"TeleportToTrialDoor")
                    elseif game.Players.LocalPlayer.Data.Race.Value == "Skypiea" then
                        tp(game:GetService("Workspace").Map["Temple of Time"].SkyCorridor.Door.Entrance.CFrame,function()
                            return Settings.TeleportToTrialDoor
                        end,nil,nil,"TeleportToTrialDoor")
                    elseif game.Players.LocalPlayer.Data.Race.Value == "Human" then
                        tp(game:GetService("Workspace").Map["Temple of Time"].HumanCorridor.Door.Entrance.CFrame,function()
                            return Settings.TeleportToTrialDoor
                        end,nil,nil,"TeleportToTrialDoor")
                    elseif game.Players.LocalPlayer.Data.Race.Value == "Ghoul" then
                        tp(game:GetService("Workspace").Map["Temple of Time"].GhoulCorridor.Door.Entrance.CFrame,function()
                            return Settings.TeleportToTrialDoor
                        end,nil,nil,"TeleportToTrialDoor")
                    elseif game.Players.LocalPlayer.Data.Race.Value == "Cybrog" then
                        tp(game:GetService("Workspace").Map["Temple of Time"].CybrogCorridor.Door.Entrance.CFrame,function()
                            return Settings.TeleportToTrialDoor
                        end,nil,nil,"TeleportToTrialDoor")
                    end
                end)
            end
            TeleportToTrialDoorValue:clear()
        end)
    end
    Funcs.AutoKillPlayer = function()
        local AutoKillPlayerValue = Priority:get("AutoKillPlayer")
        task.spawn(function()
            while Settings.AutoKillPlayer and task.wait(.1) do
                pcall(function()
                    local selectPlayer = game.Players:FindFirstChild(SelectPlayer)
                    if selectPlayer then
                        for _, character in pairs(game:GetService("Workspace").Characters:GetChildren()) do
                            if Settings.AutoKillPlayer and character.Name == SelectPlayer and character:FindFirstChild("HumanoidRootPart") and character:FindFirstChild("Humanoid") and character.Humanoid.Health > 0 then
                                Equip(GetToolFromTip(Settings.Weapon))
                                tp(character.HumanoidRootPart.CFrame * CFrame.new(0, 0, 10), function()
                                    return Settings.AutoKillPlayer
                                end, nil, nil, AutoKillPlayerValue)
                            end
                        end
                    end
                end)
            end
            AutoKillPlayerValue:clear()
        end)
    end
    Funcs.TeleporttoPlayer = function()
        local TeleporttoPlayerValue = Priority:get("TeleporttoPlayer")
        task.spawn(function()
            while Settings.TeleporttoPlayer and task.wait(.1) do
                pcall(function()
                    if game.Players:FindFirstChild(SelectPlayer) then
                        tp(game.Players[SelectPlayer].Character.HumanoidRootPart.CFrame,function()
                            return Settings.TeleporttoPlayer
                        end,nil,nil,TeleporttoPlayerValue)
                    end
                end)
            end
        end)
        TeleporttoPlayerValue:clear()
    end
    Funcs.AutoFarmBoss = function()
        local AutoFarmBossValue = Priority:get("AutoFarmBoss")
        task.spawn(function()
            while Settings.AutoFarmBoss and task.wait(.1) do
                if Settings.AutoFarmBoss then
                    pcall(function()
                        CheckBossName()
                        for _, questData in pairs(DataQuest) do
                            if questData.Mon == Settings.SelectBoss then
                                if not game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible then
                                    tp(questData.CFrameQuest, function()
                                        return Settings.AutoFarmBoss and not game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible
                                    end, false, false, AutoFarmBossValue)
                                    wait(1)
                                    _C("StartQuest", questData.NameQuest, questData.NumberQuest)
                                    wait(0.5)
                                else
                                    if string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text, questData.Mon) then
                                        local nearestBoss = _getNearest(NameBoss)
                                        if Entity.IsAlive(nearestBoss) then
                                            Entity.Attack(nearestBoss, AutoFarmBossValue)
                                        end
                                    else
                                        _C("AbandonQuest")
                                    end
                                end
                            end
                        end
                    end)
                end
            end
            AutoFarmBossValue:clear()
        end)
    end
    Funcs.MobAura = function()
        local MobAuraValue = Priority:get("MobAura")
        task.spawn(function()
            while Settings.MobAura and task.wait(.1) do
                pcall(function()
                    if Settings.MobAura and MobAuraValue:check() and not IsRaiding() then
                        for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                            if (v.HumanoidRootPart.Position - Client.Character.HumanoidRootPart.Position).Magnitude <= Settings.DistanceMobAura then
                                if Entity.IsAlive(v) then
                                    Entity.Attack(v,MobAuraValue)
                                end
                            end
                        end
                    end
                end)
            end
            MobAuraValue:clear()
        end)
    end
    Funcs.AutoPirateRaid = function()
        local AutoPirateRaidValue = Priority:get("AutoPirateRaid")
        task.spawn(function()
            while Settings.AutoPirateRaid and task.wait(.1) do
                pcall(function()
                    if Settings.AutoPirateRaid and AutoPirateRaidValue:check() and not IsRaiding() then
                        local targetPosition = CFrame.new(-5539.3115234375, 313.800537109375, -2972.372314453125).Position
                        local playerPosition = Client.Character.HumanoidRootPart.Position
                        if (targetPosition - playerPosition).Magnitude <= 500 then
                            for _, enemy in pairs(game.Workspace.Enemies:GetChildren()) do
                                local enemyPosition = enemy.HumanoidRootPart.Position
                                if (enemyPosition - playerPosition).Magnitude <= 1000 then
                                    if Entity.IsAlive(enemy) then
                                        Entity.Attack(enemy, AutoPirateRaidValue)
                                    end
                                end
                            end
                        else
                            tp(CFrame.new(-5545.1240234375, 313.800537109375, -2976.616455078125), function()
                                return Settings.AutoPirateRaid
                            end, false, false, AutoPirateRaidValue)
                        end                        
                    end
                end)
            end
            AutoPirateRaidValue:clear()
        end)
    end
    Funcs.AutoRainbowHaki = function()
        local AutoRainbowHakiValue = Priority:get("AutoRainbowHaki")
        task.spawn(function()
            while Settings.AutoRainbowHaki and task.wait(.1) do
                pcall(function()
                    if Settings.AutoRainbowHaki and AutoRainbowHakiValue:check() and not IsRaiding() then
                        ListBossRainBow = {
                            [1] = "Stone [Lv. 1550] [Boss]",
                            [2] = "Island Empress [Lv. 1675] [Boss]",
                            [3] = "Kilo Admiral [Lv. 1750] [Boss]",
                            [4] = "Captain Elephant [Lv. 1875] [Boss]",
                            [5] = "Beautiful Pirate [Lv. 1950] [Boss]"
                        }
                        if Client.PlayerGui.Main.Quest.Visible == false then
                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("HornedMan","Bet");
                        else
                            if string.find(Client.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text,'Stone') then
                                NameBoss = ListBossRainBow[1]
                            elseif string.find(Client.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text,'Island Empress') then
                                NameBoss = ListBossRainBow[2]
                            elseif string.find(Client.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text,'Kilo Admiral') then
                                NameBoss = ListBossRainBow[3]
                            elseif string.find(Client.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text,'Captain Elephant') then
                                NameBoss = ListBossRainBow[4]
                            elseif string.find(Client.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text,'Beautiful Pirate') then
                                NameBoss = ListBossRainBow[5]
                            end
                        end
                        local v = _getNearest(NameBoss)
                        if Entity.IsAlive(v) then
                            Entity.Attack(v,AutoRainbowHakiValue)
                        end
                    end
                end)
                AutoRainbowHakiValue:clear()
            end
        end)
    end
    Funcs.AutoFarmMastery = function()
        local AutoFarmMasteryValue = Priority:get("AutoFarmMastery")
        task.spawn(function()
            while Settings.AutoFarmMastery and task.wait(.1) do
                pcall(function()
                    if Settings.AutoFarmMastery and AutoFarmMasteryValue:check() and not IsRaiding() then
                        local function levelFarm(NoPredict)
                            return FORCE_LEVEL or Settings.CustomLevelFarm and math.clamp(Settings.CustomLevelFarmValue,MinLevelOfSea,NoPredict and ClientData.Level.Value or ac_lvl()) or NoPredict and ClientData.Level.Value or ac_lvl()
                        end
                        local function Expression()
                            return not Priority.Activity and Settings.AutoFarmMastery and not IsRaiding() and not AvailablePlayer[QuestTargetName]
                        end
                        if (not QuestData or not CorrectQuest) then
                            cancelQuest()
                            local level = levelFarm()
                            local ExpTime = tick()
                            local ExpNow = Client.Data.Exp.Value
                            local CalcuLevel = FORCE_LEVEL or level
                            repeat 
                                local rate=tick() - ExpTime > 1.75
                                if rate and ClientData.Exp.Value == ExpNow and ClientData.Exp.Value >= Exp_Calc(ClientData.Level.Value) then
                                    CalcuLevel = levelFarm(true)
                                    UpdateQuestData(CalcuLevel,SecondQuest)
                                end
                                if not rate and (FORCE_LEVEL or level) ~= CalcuLevel then 
                                    task.wait()
                                    continue
                                end
                                if (QuestData and not CorrectQuest) then
                                    UpdateQuestData(CalcuLevel,SecondQuest)
                                    cancelQuest()
                                end
                                tp(QUESTPOS,Expression,nil,nil,AutoFarmMasteryValue)
                                if dist(QUESTPOS.p) <= 50 and Char and Root then
                                    if BOSSNAME and _getNearest(BOSSNAME,nil,nil,1750) then
                                        _C("StartQuest",BOSSQUESTNAME,BOSSQUESTNUMBER)
                                    else
                                        _C("StartQuest",QUESTNAME,QUESTNUMBER)
                                    end
                                end
                                wait()
                            until not Settings.AutoFarmMastery or QuestData or Priority.Activity or IsRaiding()
                        elseif ClientData.Level.Value > 75 or not Settings.SkylandKill or ClientData.Level.Value <= 20 then
                            if ClientData.Level.Value >= 1000 or not Settings.PlayerHunt then
                                for i,v in pairs(workspace.Enemies:GetChildren()) do 
                                    local v = _getNearest(QuestTargetName)
                                    if not v then
                                        for _,NPC in pairs(FindNPC(QuestTargetName,Expression)) do
                                            v = NPC.Spawned
                                            if v then break end
                                            if not NPC.InArea then
                                                NPC.toSpawn()
                                                break
                                            end
                                        end
                                    end
                                    repeat task.wait()
                                        NeedNoclip = true
                                        HealthMin = v.Humanoid.MaxHealth * Settings.HealthMob/100
                                        print(HealthMin)
                                        if v.Humanoid.Health <= HealthMin then
                                            if Settings.SelectMasteryMode == "Fruit Mastery" then 
                                                Equip(Client.Data.DevilFruit.Value)
                                                tp(v.HumanoidRootPart.CFrame * CFrame.new(0, 40, 10),function()
                                                    return Settings.AutoFarmMastery
                                                end,false,false,AutoFarmMasteryValue)
                                                PositionSkillMasteryDevilFruit = v.HumanoidRootPart.Position
                                                UseSkillMasteryDevilFruit = true
                                                if game:GetService("Players").LocalPlayer.Character:FindFirstChild(Client.Data.DevilFruit.Value) then
                                                    MasteryDevilFruit = require(game:GetService("Players").LocalPlayer.Character[Client.Data.DevilFruit.Value].Data)
                                                    DevilFruitMastery = game:GetService("Players").LocalPlayer.Character[Client.Data.DevilFruit.Value].Level.Value
                                                elseif game:GetService("Players").LocalPlayer.Backpack:FindFirstChild(Client.Data.DevilFruit.Value) then
                                                    MasteryDevilFruit = require(game:GetService("Players").LocalPlayer.Backpack[Client.Data.DevilFruit.Value].Data)
                                                    DevilFruitMastery = game:GetService("Players").LocalPlayer.Backpack[Client.Data.DevilFruit.Value].Level.Value
                                                end
                                                if game:GetService("Players").LocalPlayer.Character:FindFirstChild("Dragon-Dragon") then
                                                    if Settings.SkillZ and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and DevilFruitMastery >= MasteryDevilFruit.Lvl.Z then
                                                        game:service('VirtualInputManager'):SendKeyEvent(true, "Z", false, game)
                                                        wait(.1)
                                                        game:service('VirtualInputManager'):SendKeyEvent(false, "Z", false, game)
                                                    end
                                                    if Settings.SkillX and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and DevilFruitMastery >= MasteryDevilFruit.Lvl.X then
                                                        game:service('VirtualInputManager'):SendKeyEvent(true, "X", false, game)
                                                        wait(.1)
                                                        game:service('VirtualInputManager'):SendKeyEvent(false, "X", false, game)
                                                    end   
                                                elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Human-Human: Buddha") then
                                                    if Settings.SkillZ and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and Client.Character.HumanoidRootPart.Size == Vector3.new(7.6, 7.676, 3.686) and DevilFruitMastery >= MasteryDevilFruit.Lvl.Z then
                                                    else
                                                        game:service('VirtualInputManager'):SendKeyEvent(true, "Z", false, game)
                                                        wait(.1)
                                                        game:service('VirtualInputManager'):SendKeyEvent(false, "Z", false, game)
                                                    end
                                                    if Settings.SkillX and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and DevilFruitMastery >= MasteryDevilFruit.Lvl.X then
                                                        game:service('VirtualInputManager'):SendKeyEvent(true, "X", false, game)
                                                        wait(.1)
                                                        game:service('VirtualInputManager'):SendKeyEvent(false, "X", false, game)
                                                    end
                                                    if Settings.SkillC and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and DevilFruitMastery >= MasteryDevilFruit.Lvl.C then
                                                        game:service('VirtualInputManager'):SendKeyEvent(true, "C", false, game)
                                                        wait(.1)
                                                        game:service('VirtualInputManager'):SendKeyEvent(false, "C", false, game)
                                                    end  
                                                elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild("Venom-Venom") then
                                                    if Settings.SkillZ and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and DevilFruitMastery >= MasteryDevilFruit.Lvl.Z then
                                                        game:service('VirtualInputManager'):SendKeyEvent(true, "Z", false, game)
                                                        wait(4)
                                                        game:service('VirtualInputManager'):SendKeyEvent(false, "Z", false, game)
                                                    end
                                                    if Settings.SkillX and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and DevilFruitMastery >= MasteryDevilFruit.Lvl.X then
                                                        game:service('VirtualInputManager'):SendKeyEvent(true, "X", false, game)
                                                        wait(.1)
                                                        game:service('VirtualInputManager'):SendKeyEvent(false, "X", false, game)
                                                    end
                                                    if Settings.SkillC and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and DevilFruitMastery >= MasteryDevilFruit.Lvl.C then
                                                        game:service('VirtualInputManager'):SendKeyEvent(true, "C", false, game)
                                                        wait(.1)
                                                        game:service('VirtualInputManager'):SendKeyEvent(false, "C", false, game)
                                                    end
                                                elseif game:GetService("Players").LocalPlayer.Character:FindFirstChild(Client.Data.DevilFruit.Value) then
                                                    game:GetService("Players").LocalPlayer.Character:FindFirstChild(Client.Data.DevilFruit.Value).MousePos.Value = v.HumanoidRootPart.Position
                                                    if Settings.SkillZ and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and DevilFruitMastery >= MasteryDevilFruit.Lvl.Z then
                                                        game:service('VirtualInputManager'):SendKeyEvent(true, "Z", false, game)
                                                        wait(.1)
                                                        game:service('VirtualInputManager'):SendKeyEvent(false, "Z", false, game)
                                                    end
                                                    if Settings.SkillX and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and DevilFruitMastery >= MasteryDevilFruit.Lvl.X then
                                                        game:service('VirtualInputManager'):SendKeyEvent(true, "X", false, game)
                                                        wait(.1)
                                                        game:service('VirtualInputManager'):SendKeyEvent(false, "X", false, game)
                                                    end
                                                    if Settings.SkillC and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and DevilFruitMastery >= MasteryDevilFruit.Lvl.C then
                                                        game:service('VirtualInputManager'):SendKeyEvent(true, "C", false, game)
                                                        wait(.1)
                                                        game:service('VirtualInputManager'):SendKeyEvent(false, "C", false, game)
                                                    end
                                                    if Settings.SkillV and v:FindFirstChild("HumanoidRootPart") and v:FindFirstChild("Humanoid") and v.Humanoid.Health > 0 and DevilFruitMastery >= MasteryDevilFruit.Lvl.V then
                                                        game:service('VirtualInputManager'):SendKeyEvent(true, "V", false, game)
                                                        wait(.1)
                                                        game:service('VirtualInputManager'):SendKeyEvent(false, "V", false, game)
                                                    end
                                                end
                                            elseif Settings.SelectMasteryMode == "Gun Mastery" then
                                                Equip(SelectWeaponGun)
                                                UseSkillMasteryGun = true
                                                tp(v.HumanoidRootPart.CFrame * CFrame.new(0, 30, 0),function()
                                                    return Settings.AutoFarmMastery
                                                end,false,false,AutoFarmMasteryValue)
                                                if game:GetService("Players").LocalPlayer.Character:FindFirstChild(SelectWeaponGun) and game:GetService("Players").LocalPlayer.Character:FindFirstChild(SelectWeaponGun):FindFirstChild("RemoteFunctionShoot") then
                                                    Click()
                                                    game:GetService("Players").LocalPlayer.Character[SelectWeaponGun].RemoteFunctionShoot:InvokeServer(v.HumanoidRootPart.Position,v.HumanoidRootPart)
                                                end 
                                            end
                                        else
                                            Equip(GetToolFromTip(Settings.Weapon))
                                            tp(v.HumanoidRootPart.CFrame * CFrame.new(0, 20, 0),function()
                                                return Settings.AutoFarmMastery
                                            end,false,false,AutoFarmMasteryValue)
                                            Click()
                                        end
                                    until not v.Parent or v.Humanoid.Health <= 0 or not Settings.AutoFarmMastery or (not QuestData or not CorrectQuest)
                                    NeedNoclip = false
                                    UseSkillMasteryGun = false
                                    UseSkillMasteryDevilFruit = false
                                end
                            end
                        end
                    end
                end)
            end
            AutoFarmMasteryValue:clear()
        end)
    end
    if FirstSea then
        Mon_Observaion = "Galley Captain [Lv. 650]"
        CFrame_Mon_Observation = CFrame.new(5658.5752, 38.5361786, 4928.93506, -0.996873081, 2.12391046, -0.0790185928, 2.16989656, 1, -4.96097414, 0.0790185928, -6.66008248, -0.996873081)
    elseif SecondSea then
        Mon_Observaion = "Lava Pirate [Lv. 1200]"
        CFrame_Mon_Observation = CFrame.new(-5431.09473, 15.9868021, -5296.53223, 0.831796765, 1.15322464, -0.555080295, -1.10814341, 1, 4.17010995, 0.555080295, 2.68240168, 0.831796765)
    elseif ThirdSea then
        Mon_Observaion = "Giant Islander [Lv. 1650]"
        CFrame_Mon_Observation = CFrame.new(4530.3540039063, 656.75695800781, -131.60952758789)
    end
    Funcs.AutoFarmObservation = function()
        local AutoFarmObservationValue = Priority:get("AutoFarmObservation")
        task.spawn(function()
            while Settings.AutoFarmObservation and task.wait(.1) do
                if Settings.AutoFarmObservation and AutoFarmObservationValue:check() and not IsRaiding() then
                    pcall(function()
                        NeedNoclip = true
                        if Settings.AutoFarmObservation and AutoFarmObservationValue:check() and not IsRaiding() then
                            if game.Workspace.Enemies:FindFirstChild(Mon_Observaion) then
                                local v = _getNearest(Mon_Observaion)
                                repeat task.wait()
                                    if game:GetService("Players").LocalPlayer.PlayerGui.ScreenGui:FindFirstChild("ImageLabel") then
                                        tp(v.HumanoidRootPart.CFrame * CFrame.new(3,0,0),function()
                                            return Settings.AutoFarmObservation
                                        end,false,false,AutoFarmObservationValue)
                                    else
                                        tp(v.HumanoidRootPart.CFrame * CFrame.new(0,50,0),function() 
                                            return Settings.AutoFarmObservation
                                        end,false,false,AutoFarmObservationValue)
                                        game:GetService('VirtualUser'):CaptureController()
                                        game:GetService('VirtualUser'):SetKeyDown('0x65')
                                        wait(2)
                                        game:GetService('VirtualUser'):SetKeyUp('0x65')
                                    end
                                until not Settings.AutoFarmObservation or not game.Workspace.Enemies:FindFirstChild(Mon_Observaion)
                            else
                                tp(CFrame_Mon_Observation,function()
                                    return Settings.AutoFarmObservation
                                end,false,false,AutoFarmObservationValue)
                            end
                        end
                    end)
                end
                AutoFarmObservationValue:clear()
            end
        end)
    end
    Funcs.AutoDoughV2 = function()
        local AutoDoughV2Value = Priority:get("AutoDoughV2") 
        task.spawn(function()
            while Settings.AutoDoughV2 and task.wait(.1) do
                pcall(function()
                    if Settings.AutoDoughV2 and AutoDoughV2Value:check() and not IsRaiding() then
                        NeedNoclip = true
                        if game:GetService("Workspace").Map.CakeLoaf:FindFirstChild("RedDoor") then
                            if Client.Character:FindFirstChild("Red Key") or Client.Backpack:FindFirstChild("Red Key") then
                                tp(CFrame.new(-2681.97998, 64.3921585, -12853.7363, 0.149007782, -1.87902192, 0.98883605, 3.60619588, 1, 1.35681812, -0.98883605, 3.36376011, 0.149007782),function()
                                    return Settings.AutoDoughV2
                                end,false,false,AutoDoughV2Value)
                                wait(0.5)
                                Equip("Red Key")
                                wait(0.5)
                            elseif game.Workspace:FindFirstChild("Enemies"):FindFirstChild("Dough King [Lv. 2300] [Raid Boss]") or game:GetService("ReplicatedStorage"):FindFirstChild("Dough King [Lv. 2300] [Raid Boss]") then
                                if game:GetService("Workspace").Enemies:FindFirstChild("Dough King [Lv. 2300] [Raid Boss]") then
                                    local v = _getNearest("Dough King")
                                    if Entity.IsAlive(v) then
                                        Entity.Attack(v,AutoDoughV2Value)
                                    end
                                else
                                    tp(CFrame.new(-2151.82153, 149.315704, -12404.9053),function()
                                        return Settings.AutoDoughV2
                                    end,false,false,AutoDoughV2Value)
                                end
                            elseif Client.Character:FindFirstChild("Sweet Chalice") or Client.Backpack:FindFirstChild("Sweet Chalice") then
                                if string.find(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner"),"Do you want to open the portal now?") then
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner", true)
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner")
                                else
                                    if game:GetService("Workspace").Enemies:FindFirstChild("Cookie Crafter [Lv. 2200]") or game:GetService("Workspace").Enemies:FindFirstChild("Cake Guard [Lv. 2225]") or game:GetService("Workspace").Enemies:FindFirstChild("Baking Staff [Lv. 2250]") or game:GetService("Workspace").Enemies:FindFirstChild("Head Baker [Lv. 2275]") then
                                        for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                                            if v.Name == "Cookie Crafter [Lv. 2200]" or v.Name == "Cake Guard [Lv. 2225]" or v.Name == "Baking Staff [Lv. 2250]" or v.Name == "Head Baker [Lv. 2275]" then
                                                if Entity.IsAlive(v) then
                                                    Entity.Attack(v,AutoDoughV2Value)
                                                end
                                            end
                                        end
                                    else
                                        tp(CFrame.new(-2077, 252, -12373),function()
                                            return Settings.AutoDoughV2
                                        end,false,false,AutoDoughV2Value)
                                    end
                                end
                            elseif (Client.Backpack:FindFirstChild("God's Chalice") or Client.Character:FindFirstChild("God's Chalice")) and GetMaterial("Conjured Cocoa") >= 10 then
                                game.ReplicatedStorage.Remotes.CommF_:InvokeServer("SweetChaliceNpc")
                            elseif not Client.Backpack:FindFirstChild("God's Chalice") and not Client.Character:FindFirstChild("God's Chalice") and (game.Workspace.Enemies:FindFirstChild("Deandre [Lv. 1750]") or game.Workspace.Enemies:FindFirstChild("Urban [Lv. 1750]") or game.Workspace.Enemies:FindFirstChild("Diablo [Lv. 1750]") or game.ReplicatedStorage:FindFirstChild("Deandre [Lv. 1750]") or game.ReplicatedStorage:FindFirstChild("Urban [Lv. 1750]") or game.ReplicatedStorage:FindFirstChild("Diablo [Lv. 1750]")) then
                                if game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Visible == true then
                                    if string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text,"Diablo") or string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text,"Deandre") or string.find(game:GetService("Players").LocalPlayer.PlayerGui.Main.Quest.Container.QuestTitle.Title.Text,"Urban") then
                                        if game:GetService("Workspace").Enemies:FindFirstChild("Diablo [Lv. 1750]") or game:GetService("Workspace").Enemies:FindFirstChild("Deandre [Lv. 1750]") or game:GetService("Workspace").Enemies:FindFirstChild("Urban [Lv. 1750]") then
                                            for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                                if v.Name == "Diablo [Lv. 1750]" or v.Name == "Deandre [Lv. 1750]" or v.Name == "Urban [Lv. 1750]" then
                                                    if Entity.IsAlive(v) then
                                                        Entity.Attack(v,AutoDoughV2Value)
                                                    end
                                                end
                                            end
                                        else
                                            if game:GetService("ReplicatedStorage"):FindFirstChild("Diablo [Lv. 1750]") then
                                                tp(game:GetService("ReplicatedStorage"):FindFirstChild("Diablo [Lv. 1750]").HumanoidRootPart.CFrame * CFrame.new(0, 30, 0),function()
                                                    return Settings.AutoDoughV2
                                                end,false,false,AutoDoughV2Value)
                                            elseif game:GetService("ReplicatedStorage"):FindFirstChild("Deandre [Lv. 1750]") then
                                                tp(game:GetService("ReplicatedStorage"):FindFirstChild("Deandre [Lv. 1750]").HumanoidRootPart.CFrame * CFrame.new(0, 30, 0),function()
                                                    return Settings.AutoDoughV2
                                                end,false,false,AutoDoughV2Value)
                                            elseif game:GetService("ReplicatedStorage"):FindFirstChild("Urban [Lv. 1750]") then
                                                tp(game:GetService("ReplicatedStorage"):FindFirstChild("Urban [Lv. 1750]").HumanoidRootPart.CFrame * CFrame.new(0, 30, 0),function()
                                                    return Settings.AutoDoughV2
                                                end,false,false,AutoDoughV2Value)
                                            end
                                        end                    
                                    end
                                else
                                    wait(0.5)
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("EliteHunter")
                                end
                            else
                                if game:GetService("Workspace").Enemies:FindFirstChild("Candy Rebel [Lv. 2375]") or game:GetService("Workspace").Enemies:FindFirstChild("Sweet Thief [Lv. 2350]") or game:GetService("Workspace").Enemies:FindFirstChild("Chocolate Bar Battler [Lv. 2325]") or game:GetService("Workspace").Enemies:FindFirstChild("Cocoa Warrior [Lv. 2300]") then
                                    for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                                        if v.Name == "Candy Rebel [Lv. 2375]" or v.Name == "Sweet Thief [Lv. 2350]" or v.Name == "Chocolate Bar Battler [Lv. 2325]" or v.Name == "Cocoa Warrior [Lv. 2300]" then
                                            if Entity.IsAlive(v) then
                                                Entity.Attack(v,AutoDoughV2Value)
                                            end
                                        end
                                    end
                                else
                                    tp(CFrame.new(620.6344604492188, 78.93644714355469, -12581.369140625),function()
                                        return Settings.AutoDoughV2
                                    end,false,false,AutoDoughV2Value)
                                end
                            end
                        end
                    else
                        NeedNoclip = false
                    end
                end)
                AutoDoughV2Value:clear()
            end
        end)
    end
    task.spawn(function()
        while wait() do
            if StartSoulGuitarMagnt then 
                pcall(function() 
                    for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                        if v.Name == "Living Zombie [Lv. 2000]" then 
                            v.HumanoidRootPart.CFrame = CFrame.new(-10138.3974609375, 138.6524658203125, 5902.89208984375)
                            v.Head.CanCollide = false
                            v.Humanoid.Sit = false
                            v.HumanoidRootPart.CanCollide = false
                            v.Humanoid.JumpPower = 0
                            v.Humanoid.WalkSpeed = 0
                            if v.Humanoid:FindFirstChild('Animator') then
                                v.Humanoid:FindFirstChild('Animator'):Destroy() 
                            end
                        end
                    end    
                end)
            end
        end
    end)
    Funcs.AutoSoulGuitar = function()
        local AutoSoulGuitarValue = Priority:get("AutoSoulGuitar")
        task.spawn(function()
            while Settings.AutoSoulGuitar and task.wait(.1) do
                pcall(function()
                    if Settings.AutoSoulGuitar and AutoSoulGuitarValue:check() and not IsRaiding() then
                        NeedNoclip = true
                        if GetMaterial("Bones") >= 500 and GetMaterial("Ectoplasm") >= 250 and GetMaterial("Dark Fragment") >= 1 then
                            if (CFrame.new(-9681.458984375, 6.139880657196045, 6341.3720703125).Position - game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).Magnitude <= 3000 then
                                if game:GetService("Workspace").Map["Haunted Castle"].Candle1.Transparency == 0 then
                                    local Remotes = game.ReplicatedStorage:WaitForChild("Remotes");
                                    local __CommF = Remotes:WaitForChild("CommF_");
                                    local GuitarProgress = __CommF:InvokeServer("GuitarPuzzleProgress", "Check");
                                    if not GuitarProgress then 
                                        local gravestoneEvent = game.ReplicatedStorage.Remotes.CommF_:InvokeServer("gravestoneEvent", 2);
                                        if gravestoneEvent == true then
                                            __CommF:InvokeServer("gravestoneEvent", 2, true);
                                        else 
                                            -- if _G.Hopper then
                                            --     Fast_Hop()
                                            -- end
                                        end;
                                    end
                                    if GuitarProgress then 
                                        local Swamp = GuitarProgress.Swamp;
                                        local Gravestones = GuitarProgress.Gravestones;
                                        local Ghost = GuitarProgress.Ghost;
                                        local Trophies = GuitarProgress.Trophies;
                                        local Pipes = GuitarProgress.Pipes;
                                        local CraftedOnce = GuitarProgress.CraftedOnce;
                                        if Swamp and Gravestones and Ghost and Trophies and Pipes then 
                                            Settings.AutoSoulGuitar = false
                                        end
                                        if not Swamp then 
                                            repeat wait() 
                                                Tween(CFrame.new(-10141.462890625, 138.6524658203125, 5935.06298828125) * CFrame.new(0,30,0))
                                            until Client:DistanceFromCharacter(Vector3.new(-10141.462890625, 138.6524658203125, 5935.06298828125)) <= 100
                                            for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                                                if v.Name == "Living Zombie [Lv. 2000]" then
                                                    if v:FindFirstChild('Humanoid') and v:FindFirstChild('HumanoidRootPart') and v.Humanoid.Health > 0 then 
                                                        if Client:DistanceFromCharacter(v.HumanoidRootPart.Position) <= 2000 then 
                                                            repeat wait()
                                                                Equip(GetToolFromTip(Settings.Weapon))
                                                                tp(v.HumanoidRootPart.CFrame * CFrame.new(0,20,0),function()
                                                                    return Settings.AutoSoulGuitar
                                                                end,false,false,AutoSoulGuitarValue)
                                                                StartSoulGuitarMagnt = true
                                                                Click()
                                                            until not v.Parent or v.Humanoid.Health <= 0 or not  v:FindFirstChild('HumanoidRootPart') or not v:FindFirstChild('Humanoid') or not _G.Settings.Main["Auto Quest Soul Guitar"]
                                                            StartSoulGuitarMagnt = false
                                                        end
                                                    end
                                                end
                                            end   
                                        end
                                        wait(1)
                                        if Swamp and not Gravestones then 
                                            __CommF:InvokeServer("GuitarPuzzleProgress", "Gravestones");
                                        end
                                        wait(1)
                                        if Swamp and  Gravestones and not Ghost then 
                                            __CommF:InvokeServer("GuitarPuzzleProgress", "Ghost");
                                        end 
                                        wait(1)
                                        if  Swamp and  Gravestones and Ghost and not Trophies then 
                                            __CommF:InvokeServer("GuitarPuzzleProgress", "Trophies");
                                        end
                                        wait(1)
                                        if  Swamp and  Gravestones and Ghost and Trophies and not Pipes then 
                                            __CommF:InvokeServer("GuitarPuzzleProgress", "Pipes");
                                        end
                                    end
                                else
                                    if string.find(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("gravestoneEvent",2), "Error") then
                                        tp(CFrame.new(-8653.2060546875, 140.98487854003906, 6160.033203125),function()
                                            return Settings.AutoSoulGuitar
                                        end,false,false,AutoSoulGuitarValue)
                                    elseif string.find(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("gravestoneEvent",2), "Nothing") then
                                        --print("Wait Next Night")
                                    else
                                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("gravestoneEvent",2,true)
                                    end
                                end
                            else
                                tp(CFrame.new(-8653.2060546875, 140.98487854003906, 6160.033203125),function()
                                    return Settings.AutoSoulGuitar
                                end,false,false,AutoSoulGuitarValue)
                            end
                        else
                            if GetMaterial("Ectoplasm") <= 250 then
                                if World2 then
                                    if game:GetService("Workspace").Enemies:FindFirstChild("Ship Deckhand [Lv. 1250]") or game:GetService("Workspace").Enemies:FindFirstChild("Ship Engineer [Lv. 1275]") or game:GetService("Workspace").Enemies:FindFirstChild("Ship Steward [Lv. 1300]") or game:GetService("Workspace").Enemies:FindFirstChild("Ship Officer [Lv. 1325]") or game:GetService("Workspace").Enemies:FindFirstChild("Arctic Warrior [Lv. 1350]") then
                                        for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                            if v.Name == "Ship Deckhand [Lv. 1250]" or v.Name == "Ship Engineer [Lv. 1275]" or v.Name == "Ship Steward [Lv. 1300]" or v.Name == "Ship Officer [Lv. 1325]" or v.Name == "Arctic Warrior [Lv. 1350]" then
                                                if Entity.IsAlive(v) then
                                                    Entity.Attack(v,AutoSoulGuitarValue)
                                                end
                                            end
                                        end
                                    else
                                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("requestEntrance",Vector3.new(923.21252441406, 126.9760055542, 32852.83203125))
                                    end
                                else
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelDressrosa")
                                end
                            elseif GetMaterial("Dark Fragment") < 1 then
                                if World2 then
                                    if game.ReplicatedStorage:FindFirstChild("Darkbeard [Lv. 1000] [Raid Boss]") or game:GetService("Workspace").Enemies:FindFirstChild("Darkbeard [Lv. 1000] [Raid Boss]") then
                                        for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                                            if v.Name == "Darkbeard [Lv. 1000] [Raid Boss]" then
                                                if Entity.IsAlive(v) then
                                                    Entity.Attack(v,AutoSoulGuitarValue)
                                                end
                                            end
                                        end
                                    else
                                        tp(CFrame.new(3798.4575195313, 13.826690673828, -3399.806640625),function()
                                            return Settings.AutoSoulGuitar
                                        end,false,false,AutoSoulGuitarValue)
                                    end
                                else
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelDressrosa")
                                end
                            elseif GetMaterial("Bones") <= 500 then
                                if World3 then
                                    if game:GetService("Workspace").Enemies:FindFirstChild("Reborn Skeleton [Lv. 1975]") or game:GetService("Workspace").Enemies:FindFirstChild("Living Zombie [Lv. 2000]") or game:GetService("Workspace").Enemies:FindFirstChild("Demonic Soul [Lv. 2025]") or game:GetService("Workspace").Enemies:FindFirstChild("Posessed Mummy [Lv. 2050]") then
                                        for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                            if v.Name == "Reborn Skeleton [Lv. 1975]" or v.Name == "Living Zombie [Lv. 2000]" or v.Name == "Demonic Soul [Lv. 2025]" or v.Name == "Posessed Mummy [Lv. 2050]" then
                                                if Entity.IsAlive(v) then
                                                    Entity.Attack(v,AutoSoulGuitarValue)
                                                end
                                            end
                                        end
                                    else
                                        tp(CFrame.new(-9504.8564453125, 172.14292907714844, 6057.259765625),function()
                                            return Settings.AutoSoulGuitar
                                        end,false,false,AutoSoulGuitarValue)
                                    end
                                else
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelZou")
                                end
                            end 
                        end
                    else
                        NeedNoclip = false
                    end
                end)
                AutoSoulGuitarValue:clear()
            end
        end)
    end
    local function StartTrial(Trial)
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","Progress")
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","StartTrial",Trial)
    end
    local function CDKQuestCheck()
        local CDK_TABLE = {}
        local CDK_Process = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","Progress")
        for indexx,valuee in pairs(CDK_Process) do
            table.insert(CDK_TABLE,valuee)
        end
        return CDK_TABLE
    end
    function Mon_Haze()
        for i,v in pairs(game:GetService("Players").LocalPlayer.QuestHaze:GetChildren()) do 
            if v.Value > 0 then
                return v.Name
            end
        end
    end
    local function Check_Mastery_Weapon(Weapon_Name)
        for i,v in pairs(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("getInventory")) do
            if v.Name == Weapon_Name then
                return v.Mastery
            end
        end
    end 
    Funcs.AutoCursedDualKatana = function()
        local AutoCursedDualKatanaValue = Priority:get("AutoCursedDualKatana")
        task.spawn(function()
            while Settings.AutoCursedDualKatana and task.wait(.1) do
                -- pcall(function()
                    if Settings.AutoCursedDualKatana and AutoCursedDualKatanaValue:check() and not IsRaiding() then
                        if _hasItem("Cursed Dual Katana") then return end
                        if Check_Mastery_Weapon("Tushita") <= 350 then
                            local hasTushita = Client.Character:FindFirstChild("Tushita") or Client.Backpack:FindFirstChild("Tushita")
                            if hasTushita then
                                Settings.Weapon = "Sword"
                                for _,v in pairs(Client.Character:GetChildren()) do
                                    NeedNoclip = true
                                    local enemyTypes = {
                                        'Reborn Skeleton [Lv. 1975]',
                                        'Living Zombie [Lv. 2000]',
                                        'Demonic Soul [Lv. 2025]',
                                        'Posessed Mummy [Lv. 2050]'
                                    }
                                    local foundEnemies = false
                                    for _, enemy in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                        if table.find(enemyTypes, enemy.Name) and Entity.IsAlive(enemy) then
                                            Entity.Attack(enemy, AutoCursedDualKatanaValue)
                                            foundEnemies = true
                                        end
                                    end
                                    if not foundEnemies then
                                        tp(CFrame.new(-9504.8564453125, 172.14292907714844, 6057.259765625), function()
                                            return Settings.AutoCursedDualKatana
                                        end, false, false, AutoCursedDualKatanaValue)
                                    end
                                end
                            else
                                _C("LoadItem", "Tushita")
                            end
                        end
                        if Check_Mastery_Weapon("Yama") <= 350 and Check_Mastery_Weapon("Tushita") >= 350 then
                            local hasYama = Client.Character:FindFirstChild("Yama") or Client.Backpack:FindFirstChild("Yama")
                            if hasYama then
                                Settings.Weapon = "Sword"
                                for _,v in pairs(Client.Character:GetChildren()) do
                                    NeedNoclip = true
                                    local enemyTypes = {
                                        'Reborn Skeleton [Lv. 1975]',
                                        'Living Zombie [Lv. 2000]',
                                        'Demonic Soul [Lv. 2025]',
                                        'Posessed Mummy [Lv. 2050]'
                                    }
                                    local foundEnemies = false
                                    for _, enemy in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                        if table.find(enemyTypes, enemy.Name) and Entity.IsAlive(enemy) then
                                            Entity.Attack(enemy, AutoCursedDualKatanaValue)
                                            foundEnemies = true
                                        end
                                    end
                                    if not foundEnemies then
                                        tp(CFrame.new(-9504.8564453125, 172.14292907714844, 6057.259765625), function()
                                            return Settings.AutoCursedDualKatana
                                        end, false, false, AutoCursedDualKatanaValue)
                                    end
                                end
                            else
                                _C("LoadItem", "Yama")
                            end
                        end
                        if Check_Mastery_Weapon("Yama") >= 350 and Check_Mastery_Weapon("Tushita") >= 350 then
                            if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","OpenDoor") == "can" then
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest","OpenDoor",true)
                            end
                            if CDKQuestCheck()[2] == 0 then
                                print("GetQuest")
                                StartTrial('Evil')
                            end   
                            if CDKQuestCheck()[2] == true then
                                local enemies = game:GetService("Workspace").Enemies
                                if enemies:FindFirstChild("Cursed Skeleton Boss [Lv. 2025] [Boss]") or game:GetService("Workspace").ReplicatedStorage:FindFirstChild("Cursed Skeleton Boss [Lv. 2025] [Boss]") then
                                    for _, enemy in pairs(enemies:GetChildren()) do
                                        local enemyName = enemy.Name
                                        if enemyName == "Cursed Skeleton Boss [Lv. 2025] [Boss]" or enemyName == "Cursed Skeleton [Lv. 2200]" then
                                            if Entity.IsAlive(enemy) then
                                                Entity.Attack(enemy, AutoCursedDualKatanaValue)
                                            end
                                        end
                                    end
                                else
                                    local targetPosition = CFrame.new(-12361.7060546875, 603.3547973632812, -6550.5341796875).Position
                                    local characterPosition = Client.Character.HumanoidRootPart.Position
                                    local distance = (targetPosition - characterPosition).Magnitude                                
                                    if distance <= 100 then
                                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest", "Progress", "Good")
                                        wait(1)
                                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest", "Progress", "Evil")
                                        wait(1)
                                        tp(CFrame.new(-12361.7060546875, 603.3547973632812, -6550.5341796875), function()
                                            return Settings.AutoCursedDualKatana
                                        end, false, false, AutoCursedDualKatanaValue)
                                        wait(1.5)
                                        game:GetService("VirtualInputManager"):SendKeyEvent(true, "E", false, game)
                                        wait(1.5)
                                        tp(CFrame.new(-12253.5419921875, 598.8999633789062, -6546.8388671875), function()
                                            return Settings.AutoCursedDualKatana
                                        end, false, false, AutoCursedDualKatanaValue)
                                    else
                                        tp(CFrame.new(-12361.7060546875, 603.3547973632812, -6550.5341796875), function()
                                            return Settings.AutoCursedDualKatana
                                        end, false, false, AutoCursedDualKatanaValue)
                                    end
                                end 
                            end
                            if CDKQuestCheck()[3] ~= 4 then
                                StartTrial('Evil')
                                if CDKQuestCheck()[3] == -5 then
                                    StartTrial('Evil')
                                    local map = game:GetService("Workspace").Map
                                    local enemies = game:GetService("Workspace").Enemies                                       
                                    local mon = {
                                        "Cursed Skeleton [Lv. 2200]",
                                        "Cursed Skeleton [Lv. 2200] [Boss]",
                                        "Hell's Messenger [Lv. 2200] [Boss]"
                                    }                                        
                                    if map:FindFirstChild("HellDimension") then
                                        local foundEnemies = false                                       
                                        for _, enemyName in ipairs(mon) do
                                            if enemies:FindFirstChild(enemyName) then
                                                for _, enemy in pairs(enemies:GetChildren()) do
                                                    if enemy.Name == enemyName and Entity.IsAlive(enemy) then
                                                        Entity.Attack(enemy, AutoCursedDualKatanaValue)
                                                        foundEnemies = true
                                                    end
                                                end
                                            end
                                        end                                        
                                        if not foundEnemies then
                                            local torches = {
                                                map.HellDimension.Torch1,
                                                map.HellDimension.Torch2,
                                                map.HellDimension.Torch3
                                            }                                        
                                            for _, torch in pairs(torches) do
                                                tp(torch.CFrame, function()
                                                    return Settings.AutoCursedDualKatana and CDKQuestCheck()[3] == -5
                                                end, false, false, AutoCursedDualKatanaValue)
                                                wait(.5)
                                                fireproximityprompt(torch.ProximityPrompt, math.huge)
                                                wait(.5)
                                            end                                       
                                            tp(map.HellDimension.Exit.CFrame, function()
                                                return Settings.AutoCursedDualKatana and CDKQuestCheck()[3] == -5
                                            end, false, false, AutoCursedDualKatanaValue)
                                        end
                                    else
                                        local soulReaperBossName = "Soul Reaper [Lv. 2100] [Raid Boss]"                                       
                                        if game.ReplicatedStorage:FindFirstChild(soulReaperBossName) or enemies:FindFirstChild(soulReaperBossName) then
                                            if enemies:FindFirstChild(soulReaperBossName) then
                                                for _, enemy in pairs(enemies:GetChildren()) do
                                                    if enemy.Name == soulReaperBossName then
                                                        tp(enemy.HumanoidRootPart.CFrame * CFrame.new(0, 0, -2), function()
                                                            return Settings.AutoCursedDualKatana and CDKQuestCheck()[3] == -5
                                                        end, nil, nil, AutoCursedDualKatanaValue)
                                                    end
                                                end
                                            else
                                                tp(CFrame.new(-9570.033203125, 315.9346923828125, 6726.89306640625), function()
                                                    return Settings.AutoCursedDualKatana
                                                end, false, false, AutoCursedDualKatanaValue)
                                            end
                                        elseif _hasItem("Hallow Essence") then
                                            Equip("Hallow Essence")
                                            firetouchinterest(Client.Character.Head, map["Haunted Castle"].Summoner.Detection, 0)
                                            firetouchinterest(Client.Character.Head, map["Haunted Castle"].Summoner.Detection, 1)
                                        else
                                            game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Bones", "Buy", 1, 1)
                                        end
                                    end
                                elseif CDKQuestCheck()[3] == -4 then
                                    StartTrial('Evil')
                                    print("Yama Quest 2")
                                    local Mon , Vmon = _getNearest(Mon_Haze()) , Mon_Haze() ;
                                    if not Mon then 
                                        for i2 ,v2 in pairs(workspace._WorldOrigin.EnemySpawns:GetChildren()) do 
                                            if v2.Name == Vmon or v2.Name:match(Vmon) then 
                                                tp(v2.CFrame * CFrame.new(0,50,0),function()
                                                    return Settings.AutoCursedDualKatana and CDKQuestCheck()[3] == -4
                                                end,nil,nil,AutoCursedDualKatanaValue)
                                            end ;
                                        end ;
                                    else
                                        Entity.Attack(Mon,AutoCursedDualKatanaValue)
                                    end;
                                elseif CDKQuestCheck()[3] == -3 then
                                    StartTrial('Evil')
                                    print("Yama Quest 1")
                                    if game:GetService("Workspace").Enemies:FindFirstChild("Mythological Pirate [Lv. 1850]") then
                                        for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                            if v.Name == "Mythological Pirate [Lv. 1850]" then
                                                tp(v.HumanoidRootPart.CFrame * CFrame.new(0,0,-2),function()
                                                    return Settings.AutoCursedDualKatana and CDKQuestCheck()[3] == -3
                                                end,false,false,AutoCursedDualKatanaValue)
                                            end
                                        end
                                    else
                                        tp(CFrame.new(-13451.46484375, 543.712890625, -6961.0029296875),function()
                                            return Settings.AutoCursedDualKatana and CDKQuestCheck()[3] == -3
                                        end,false,false,AutoCursedDualKatanaValue)
                                    end
                                end
                            else 
                                if CDKQuestCheck()[1] == -4 then
                                    local map = game:GetService("Workspace").Map
                                    local enemies = game:GetService("Workspace").Enemies                                        
                                    if map:FindFirstChild("HeavenlyDimension") then
                                        local enemyNames = {
                                            "Cursed Skeleton [Lv. 2200]",
                                            "Cursed Skeleton [Lv. 2200] [Boss]",
                                            "Heaven's Guardian [Lv. 2200] [Boss]"
                                        }                                           
                                        local foundEnemies = false                                            
                                        for _, enemyName in ipairs(enemyNames) do
                                            if enemies:FindFirstChild(enemyName) then
                                                for _, enemy in pairs(enemies:GetChildren()) do
                                                    if enemy.Name == enemyName and Entity.IsAlive(enemy) then
                                                        Entity.Attack(enemy, AutoCursedDualKatanaValue)
                                                        foundEnemies = true
                                                    end
                                                end
                                            end
                                        end                                            
                                        if not foundEnemies then
                                            local torches = {
                                                map.HeavenlyDimension.Torch1,
                                                map.HeavenlyDimension.Torch2,
                                                map.HeavenlyDimension.Torch3
                                            }                                               
                                            for _, torch in pairs(torches) do
                                                tp(torch.CFrame, function()
                                                    return Settings.AutoCursedDualKatana and CDKQuestCheck()[1] == -4
                                                end, false, false, AutoCursedDualKatanaValue)
                                                wait(.5)
                                                fireproximityprompt(torch.ProximityPrompt, math.huge)
                                                wait(.5)
                                            end                                               
                                            tp(map.HeavenlyDimension.Exit.CFrame, function()
                                                return Settings.AutoCursedDualKatana and CDKQuestCheck()[1] == -4
                                            end, false, false, AutoCursedDualKatanaValue)
                                        end
                                    else
                                        local bossName = "Cake Queen [Lv. 2175] [Boss]"                                           
                                        if enemies:FindFirstChild(bossName) or game.ReplicatedStorage:FindFirstChild(bossName) then
                                            for _, enemy in pairs(enemies:GetChildren()) do
                                                if enemy.Name == bossName and Entity.IsAlive(enemy) then
                                                    Entity.Attack(enemy, AutoCursedDualKatanaValue)
                                                end
                                            end
                                        else
                                            tp(CFrame.new(-709.3132934570312, 381.6005859375, -11011.396484375), function()
                                                return Settings.AutoCursedDualKatana and CDKQuestCheck()[1] == -4
                                            end, false, false, AutoCursedDualKatanaValue)
                                        end
                                    end                                        
                                elseif CDKQuestCheck()[1] == -3 then
                                    if (CFrame.new(-5539.3115234375, 313.800537109375, -2972.372314453125).Position - Client.Character.HumanoidRootPart.Position).Magnitude <= 500 then
                                        for i,v in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                            if (v.HumanoidRootPart.Position - Client.Character.HumanoidRootPart.Position).Magnitude < 2000 then
                                                if Entity.IsAlive(v) then
                                                    Entity.Attack(v,AutoCursedDualKatanaValue)
                                                end
                                            end
                                        end
                                    else
                                        tp(CFrame.new(-5545.1240234375, 313.800537109375, -2976.616455078125),function()
                                            return Settings.AutoCursedDualKatana and CDKQuestCheck()[1] == -3
                                        end,false,false,AutoCursedDualKatanaValue)
                                    end
                                elseif CDKQuestCheck()[1] == -2 then
                                    tp(CFrame.new(-9546.990234375, 21.139892578125, 4686.1142578125), function()
                                        return Settings.AutoCursedDualKatana and CDKQuestCheck()[1] == -2
                                    end, false, false, AutoCursedDualKatanaValue)
                                    wait(0.5)
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest", "BoatQuest", workspace.NPCs:FindFirstChild("Luxury Boat Dealer"))
                                    wait(0.5)
                                    tp(CFrame.new(-6120.0576171875, 16.455780029296875, -2250.697265625), function()
                                        return Settings.AutoCursedDualKatana and CDKQuestCheck()[1] == -2
                                    end, false, false, AutoCursedDualKatanaValue)
                                    wait(0.5)
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest", "BoatQuest", workspace.NPCs:FindFirstChild("Luxury Boat Dealer"))
                                    wait(0.5)
                                    tp(CFrame.new(-9533.2392578125, 7.254445552825928, -8372.69921875), function()
                                        return Settings.AutoCursedDualKatana and CDKQuestCheck()[1] == -2
                                    end, false, false, AutoCursedDualKatanaValue)
                                    wait(0.5)
                                    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CDKQuest", "BoatQuest", workspace.NPCs:FindFirstChild("Luxury Boat Dealer"))
                                    wait(0.5)                                        
                                end
                            end                            
                        end
                    end
                -- end)
                AutoCursedDualKatanaValue:clear()
            end
        end)
    end
    Funcs.AutoAncientOneQuest = function()
        local AutoAncientOneQuestValue = Priority:get("AutoAncientOneQuest")
        task.spawn(function()
            while Settings.AutoAncientOneQuest and task.wait(.1) do
                pcall(function()
                    if Settings.AutoAncientOneQuest and AutoAncientOneQuestValue:check() and not IsRaiding() then
                        local raceUpgradeResult = game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("UpgradeRace", "Buy")
                        if raceUpgradeResult ~= true then
                            local raceEnergy = Client.Character:FindFirstChild("RaceEnergy")
                            local raceTransformed = Client.Character:FindFirstChild("RaceTransformed")
                            if raceEnergy.Value < 1 and not raceTransformed.Value then
                                if game:GetService("Workspace").Enemies:FindFirstChild('Reborn Skeleton [Lv. 1975]') or game:GetService("Workspace").Enemies:FindFirstChild('Living Zombie [Lv. 2000]') or game:GetService("Workspace").Enemies:FindFirstChild('Demonic Soul [Lv. 2025]') or game:GetService("Workspace").Enemies:FindFirstChild('Posessed Mummy [Lv. 2050]') then
                                    for _, enemy in pairs(game:GetService("Workspace").Enemies:GetChildren()) do
                                        if enemy.Name == 'Reborn Skeleton [Lv. 1975]' or enemy.Name == 'Living Zombie [Lv. 2000]' or enemy.Name == 'Demonic Soul [Lv. 2025]' or enemy.Name == 'Posessed Mummy [Lv. 2050]' then
                                            if Entity.IsAlive(enemy) then
                                                Entity.Attack(enemy, AutoAncientOneQuestValue)
                                            end
                                        end
                                    end
                                else
                                    tp(CFrame.new(-9479.2168, 200.215088, 5577.09277, 0, 0, 1, 0, 1, -0, -1, 0, 0), function()
                                        return Settings.AutoAncientOneQuest
                                    end, false, false, AutoAncientOneQuestValue)
                                end
                            else
                                game:GetService("VirtualInputManager"):SendKeyEvent(true, "Y", false, game)
                                task.wait()
                                game:GetService("VirtualInputManager"):SendKeyEvent(false, "Y", false, game)
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("UpgradeRace", "Check")
                                game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("UpgradeRace", "Buy")
                            end
                        end                        
                    end
                end) 
                AutoAncientOneQuestValue:clear()
            end
        end)
    end
    Funcs.AutoCompleteTrial = function()
        local AutoCompleteTrialValue = Priority:get("AutoCompleteTrial")
        task.spawn(function()
            while Settings.AutoCompleteTrial and task.wait(.1) do
                pcall(function()
                    if Settings.AutoCompleteTrial and AutoCompleteTrialValue:clear() and IsRaiding() then
                        if Client.Data.Race.Value == "Mink" then	
                            if game:GetService("Workspace").Map:FindFirstChild("MinkTrial") then
                                if (game:GetService("Workspace").Map.MinkTrial.Ceiling.CFrame - Client.Character.HumanoidRootPart.Position).Magnitude <= 200 then
                                    tp(game:GetService("Workspace").Map.MinkTrial.Ceiling.CFrame * CFrame.new(0,-20,0),function()
                                        return Settings.AutoCompleteTrial
                                    end,false,false,AutoCompleteTrialValue)
                                end
                            end
                        elseif Client.Data.Race.Value == "Human" then
                            if game:GetService("Workspace").Map:FindFirstChild("HumanTrial") then
                                for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                                    if (v.HumanoidRootPart.Position-game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 400 then
                                        if Entity.IsAlive(v) then
                                            Entity.Attack(v,AutoCompleteTrialValue)
                                        end
                                    end
                                end
                            end
                        elseif Client.Data.Race.Value == "Cyborg" then
                            if game:GetService("Workspace").Map:FindFirstChild("CybrogTrial") then
                                tp(game:GetService("Workspace").Map.CyborgTrial.Floor.CFrame*CFrame.new(0,500,0),function()
                                    return Settings.AutoCompleteTrial
                                end,false,false,AutoCompleteTrialValue)
                            end
                        elseif Client.Data.Race.Value == "Skypiea" then
                            if game:GetService("Workspace").Map:FindFirstChild("SkyTrial") then
                                if (game:GetService("Workspace").Map.SkyTrial.Model.FinishPart.CFrame-Client.Character.HumanoidRootPart.Position).Magnitude <= 750 then
                                    tp(game:GetService("Workspace").Map.SkyTrial.Model.FinishPart.CFrame,function()
                                        return Settings.AutoCompleteTrial
                                    end,false,false,AutoCompleteTrialValue)
                                end
                            end
                        elseif Client.Data.Race.Value == "Ghoul" then
                            if game:GetService("Workspace").Map:FindFirstChild("GhoulTrial") then 
                                for i,v in pairs(game.Workspace.Enemies:GetChildren()) do
                                    if (v.HumanoidRootPart.Position-game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.Position).magnitude <= 400 then
                                        if Entity.IsAlive(v) then
                                            Entity.Attack(v,AutoCompleteTrialValue)
                                        end
                                    end
                                end
                            end
                        elseif Client.Data.Race.Value == "Fishman" then
                            if game:GetService("Workspace").Map:FindFirstChild("FishTrial") then
                                if (game:GetService("Workspace").Map:FindFirstChild("FishTrial").Part.Position-Client.Character.HumanoidRootPart.Position).Magnitude <= 500 then
                                    tp(CFrame.new(25032.043, 75.04647064, 12619.5967),function()
                                        return Settings.AutoCompleteTrial
                                    end,false,false,AutoCompleteTrialValue)
                                    local DevilFruit = Client.Data.DevilFruit.Value
                                    Equip(DevilFruit)
                                    game:GetService("VirtualInputManager"):SendKeyEvent(true,"Z",false,game)
                                    task.wait()
                                    game:GetService("VirtualInputManager"):SendKeyEvent(false,"Z",false,game)
                                    task.wait(2)
                                    game:GetService("VirtualInputManager"):SendKeyEvent(true,"X",false,game)
                                    task.wait()
                                    game:GetService("VirtualInputManager"):SendKeyEvent(false,"X",false,game)
                                    task.wait(2)
                                    game:GetService("VirtualInputManager"):SendKeyEvent(true,"C",false,game)
                                    task.wait()
                                    game:GetService("VirtualInputManager"):SendKeyEvent(false,"C",false,game)
                                    task.wait(2)
                                    game:GetService("VirtualInputManager"):SendKeyEvent(true,"V",false,game)
                                    task.wait()
                                    game:GetService("VirtualInputManager"):SendKeyEvent(false,"V",false,game)
                                    task.wait(3)
                                    EquipMelee()
                                    game:GetService("VirtualInputManager"):SendKeyEvent(true,"Z",false,game)
                                    task.wait()
                                    game:GetService("VirtualInputManager"):SendKeyEvent(false,"Z",false,game)
                                    task.wait(2)
                                    game:GetService("VirtualInputManager"):SendKeyEvent(true,"X",false,game)
                                    task.wait()
                                    game:GetService("VirtualInputManager"):SendKeyEvent(false,"X",false,game)
                                    task.wait(2)
                                    game:GetService("VirtualInputManager"):SendKeyEvent(true,"C",false,game)
                                    task.wait()
                                    game:GetService("VirtualInputManager"):SendKeyEvent(false,"C",false,game)
                                end
                            end
                        end
                    end
                end)
                AutoCompleteTrialValue:clear()
            end
        end)
    end
end)

--Ui Section--

local kkii = require(game.ReplicatedStorage.Util.CameraShaker)
kkii:Stop()

getgenv().Key = "KuySixSen"
local Lib = loadstring(game:HttpGet('https://raw.githubusercontent.com/REALSALFES/BloxFruit/main/Load.lua'))():New() ;

local General = Lib.new({Title = "General"  , Icon = "rbxassetid://12967034277"})
local Automatic = Lib.new({Title = "Automatic" , Icon = "rbxassetid://12967035609" })
local Weapon = Lib.new({Title = "Weapon" , Icon = "rbxassetid://12967037073" })
local Race = Lib.new({Title = "Race" , Icon = "rbxassetid://12967038588"})
local Visual = Lib.new({Title = "Visual" , Icon = "rbxassetid://12967040337" })
local Combat = Lib.new({Title = "Combat" , Icon = "rbxassetid://12967042045"})
local Misc = Lib.new({Title = "Misc" , Icon = "rbxassetid://12967046276" })
local setting = Lib.new({Title = "setting" , Icon = "rbxassetid://12967048346" })

function Toggle(section,Name,desc,Page,...)
    local SettingName,func = ...
    if not func and type(SettingName) == "function" then func = SettingName end
    if not SettingName then SettingName = Name end
    return section:Create({Text = Name ,Value = Settings[SettingName],Callback = function(value)
        Settings[SettingName] = value
        if Funcs[SettingName] then
            task.spawn(Funcs[SettingName])
        end
    end,},"Toggle",Page)
end
function Slider(section,Name,min,max,Page,...)
    local SettingName,func = ...
    if not func and type(SettingName) == "function" then func = SettingName end
    if not SettingName then SettingName = Name end
    local default = Settings[SettingName]
    return section:Create({Text = Name ,Value = default ~= nil and default or min,Max = max,Min = min,Callback = function(value)
        Settings[SettingName] = value
    end,},"Slider",Page)
end
function TextBox(section,Name,PlaceHolder,Page,...)
    local SettingName,func = ...
    if not func and type(SettingName) == "function" then func = SettingName end
    if not SettingName then SettingName = Name end
    local TextBox = section:Create({Text = Name,Placeholder = PlaceHolder,Callback = function(value)
        Settings[SettingName] = value
    end,},"TextBox",Page)
    if Settings[SettingName] then
        TextBox.Value = Settings[SettingName]
    end
end
function Dropdown(section,Name,default,list,Page,...)
    local SettingName,func = ...
    if not func and type(SettingName) == "function" then func = SettingName end
    if not SettingName then SettingName = Name end
    section:Create({Text = Name ,Value = list,Default = Settings[SettingName] or default, Callback = function(value)
        Settings[SettingName] = value
    end,},"Dropdown",Page)
end

function MultiDropdown(section,Name,default,list,Page,...)
    local SettingName,func = ...
    local Converted = {}
    local firstTime
    if not func and type(SettingName) == "function" then func = SettingName end
    if not SettingName then SettingName = Name end
    if not Settings[SettingName] then firstTime = true Settings[SettingName] = {} end
    for i,v in pairs(Settings[SettingName]) do
        if v then
            table.insert(Converted,i) 
        end 
    end
    section:Create({Text = Name ,Value = list,Default = firstTime and default or Converted,Multi = true ,Callback = function(value) 
        Settings[SettingName] = value
    end,},"Dropdown",tonumber(Page))
end

function Click()
	game:GetService("VirtualUser"):CaptureController()
	game:GetService("VirtualUser"):Button1Down(Vector2.new(1280, 672))
end

--[General]--

General:Create({
    Text = "Main"
},"Label",1)

Toggle(General,"Auto Farm [Level]","Grinding Level",1,"AutoFarm")
Toggle(General,"Auto Second Sea","Auto Unlock SecondSea",1,"AutoSecondSea")
Toggle(General,"Auto Third Sea","Auto Unlock ThirdSea",1,"AutoThirdSea")
Toggle(General,"Auto ThirdSea [Hop]","AutoThirdSea can hopserver",1,"AutoThirdSeaHop")

General:Create({
    Text = "Boss"
},"Label",1)

local BossTable = {}   
for i,v in pairs(Mon) do
	table.insert(BossTable, v)
end

Dropdown(General,"Select Boss","",BossTable,1,"SelectBoss")
Toggle(General,"Auto Farm Boss","Farm Boss",1,"AutoFarmBoss")

General:Create({
    Text = "Stats"
},"Label",2)

Slider(General,"Redeem Code After Level",1,MAXLEVEL,2,"AutoRedeemCodeOnLevel")
Toggle(General,"Redeem Enable","redeem all codes",2,"AutoRedeemCode")

General:Create({Text = "Redeem X2 EXP Code",Callback = function()
    local function UseCode(Text)
        game:GetService("ReplicatedStorage").Remotes.Redeem:InvokeServer(Text)
    end
    for i,v in pairs({
        "GAMERROBOT_YT",
        "EXP_5B",
        "kittgaming",
        "Enyu_is_Pro",
        "Sub2Fer999",
        "THEGREATACE",
        "SUB2GAMERROBOT_EXP1",
        "Sub2OfficialNoobie",
        "StrawHatMaine",
        "SUB2NOOBMASTER123",
        "Sub2Daigrock",
        "Axiore",
        "TantaiGaming",
        "STRAWHATMAINE",
        "JCWK",
        "Magicbus",
        "Starcodeheo",
        "Bluxxy",
    }) do
        task.spawn(UseCode,v)
    end
end,},"Button",2)

Toggle(General,"Kaitan Sword","Melee & Defense & Sword",2,"KaitanSword",function(value)
    Settings.KaitanSword = value
    if value then
        if General.Toggles["Kaitan Gun"] then
            General.Toggles["Kaitan Gun"].Value = false
            General.Toggles["Kaitan Fruit"].Value = false
        end
    end
end)
Toggle(General,"Kaitan Gun","Melee & Defense & Gun",2,"KaitanGun",function(value)
    Settings.KaitanGun = value
    if value then
        General.Toggles["Kaitan Sword"].Value = false
        if General.Toggles["Kaitan Fruit"] then
            General.Toggles["Kaitan Fruit"].Value = false
        end
    end
end)
Toggle(General,"Kaitan Fruit","Melee & Defense & Fruit",2,"KaitanFruit",function(value)
    Settings.KaitanFruit = value
    if value then
        General.Toggles["Kaitan Sword"].Value = false
        General.Toggles["Kaitan Gun"].Value = false
    end
end)

General:Create({
    Text = "Mastery"
},"Label",1)

Dropdown(General,"Select Mastery Mode","Fruit Mastery",{"Fruit Mastery","Gun Mastery"},1,"SelectMasteryMode")
Toggle(General,"Auto Farm Mastery","Farm Mastery",1,"AutoFarmMastery")

General:Create({
    Text = "Mastery Setting"
},"Label",1)

Slider(General,"Mob Health (%)",1,100,1,"HealthMob")
Toggle(General,"Skill Z","Skill Z",1,"SkillZ")
Toggle(General,"Skill X","Skill X",1,"SkillX")
Toggle(General,"Skill C","Skill C",1,"SkillC")
Toggle(General,"Skill V","Skill V",1,"SkillV")

General:Create({
    Text = "Setting Farm"
},"Label",2)

Dropdown(General,"Weapon","Melee",{"Melee","Sword","Gun"},2,"Weapon")
Toggle(General,"Player Hunter","do playerhunt quest while level higher than 20 (if can)",2,"PlayerHunt")
Toggle(General,"Double Quest","do second quest while waiting first quest mob spawn",2,"DoubleQuest")
Toggle(General,"Fast Attack","Attack faster from normal",2,"FastAttack")
Toggle(General,"Instant Attack","Almost Remove attack Cooldown from game",2,"NewFastAttack")
Toggle(General,"No Attack Animation","Remove all attack animation from exploit attack",2,"NoAttackAnimation")
Toggle(General,"Instant Teleport","Instant move to target within 5secs",2,"IslandTP")
Toggle(General,"Random Position Farm","Rotate Position Around Target",2,"PositionRotate")

--[Automatic]--

Automatic:Create({
    Text = "Fighting Style"
},"Label",1)

Toggle(Automatic,"Auto Godhuman","No Auto Material",1,"AutoGodhuman")
Toggle(Automatic,"Auto Superhuman","Buy DarkStep,Electric,Water Kung Fu,Dragon Breath and Purchase Superhuman",1,"AutoSuperhuman")
Toggle(Automatic,"Auto Electric Claw","Farm Electric and do Speedrun Quest",1,"AutoElectricClaw")
Toggle(Automatic,"Auto Dragon Talon","Farm Dragon Breath and purchase talon",1,"AutoDragonTalon")
Toggle(Automatic,"Auto Death Step","Farm DarkStep then find key and purchase DeathStep",1,"AutoDeathStep")
Toggle(Automatic,"Auto SharkmanKarate","Farm Water Kung Fu then find key and purchase Sharkman Karate",1,"AutoSharkmanKarate")

Automatic:Create({
    Text = "Mob Aura"
},"Label",2)

Slider(Automatic,"Distance Mob Aura",1,5000,2,"DistanceMobAura")
Toggle(Automatic,"Mob Aura","Farm Mob Around",2,"MobAura")

Automatic:Create({
    Text = "Cake Prince"
},"Label",2)

local TotalMob = Automatic:Create({
    Text = "Total Mob"
},"Label",2)

task.spawn(function()
    while wait(.1) do
        pcall(function()
            local caketotal = string.match(game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CakePrinceSpawner"),"%d+")
            if caketotal then
                TotalMob.Text = "Total : "..tostring(caketotal)
            else
                TotalMob.Text = "Boss : Spawned"
            end
        end)
    end
end)

Toggle(Automatic,"Auto Cake Prince","Auto Cake Prince",2,"AutoCakePrince")

Automatic:Create({
    Text = "Elite Hunter"
},"Label",2)

local EliteHunterCount = Automatic:Create({
    Text = "Elite Hunter"
},"Label",2)

task.spawn(function()
    while wait() do
        pcall(function()
            local Data = _C("EliteHunter","Progress")
            EliteHunterCount.Text = "Total : "..tostring(Data)
        end)
    end
end)

Toggle(Automatic,"Auto Elite Hunter","Auto Kill EliteHunter",2,"AutoEliteHunter")
Toggle(Automatic,"Auto Elite Hunter [Hop]","Rejoin when no elite hunter found",2,"AutoEliteHunterHop")
Toggle(Automatic,"Stop Until Have God Chalice","Stop Until Have God Chalice",2,"AutoStopWhenUntilGodChalice")

Automatic:Create({
    Text = "Bone"
},"Label",2)

local BoneCount = Automatic:Create({
    Text = "Bone : "
},"Label",2)

task.spawn(function()
    while wait() do
        pcall(function()
            BoneCount.Text = "Bones : "..CurrentBone
        end)
    end
end)

Toggle(Automatic,"Auto Bones","Automatic Farming bones",2,"AutoBone")

Automatic:Create({
    Text = "Main AutoMatic"
},"Label",1)

Toggle(Automatic,"Auto Pirate Raid","Farm Pirate Raid",1,"AutoPirateRaid")
Toggle(Automatic,"Auto Rainbow Haki","Do Rainbow Haki",1,"AutoRainbowHaki")
Toggle(Automatic,"Auto Dough V2","Dough V2",1,"AutoDoughV2")
Toggle(Automatic,"Auto Soul Guitar","Soul Guitar",1,"AutoSoulGuitar")

Automatic:Create({
    Text = "Observation"
},"Label",2)

Toggle(Automatic,"Auto Farm Observation Haki","Farm Pirate Raid",2,"AutoFarmObservation")

--[Weapon]--

Weapon:Create({
    Text = "Sword"
},"Label",1)

Weapon:Create({
    Text = "World 1"
},"Label",1)

Toggle(Weapon,"Auto Saber","Complete Saber Quest and Kill Boss",1,"AutoSaber")
Toggle(Weapon,"Auto Pole V1","Auto Kill Thunder God",1,"AutoPoleV1")
Toggle(Weapon,"Auto Cannon","Auto Find Cannon",1,"AutoCannon")
Toggle(Weapon,"Auto Bizento V2","Auto Bizento V2",1,"AutoBizentoV2")
Weapon:Create({
    Text = "World 2"
},"Label",1)
Toggle(Weapon,"Auto True Triple Katana","Auto Make True Triple Katana",1,function(value)
    while value and task.wait(.1) do
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("MysteriousMan",2)
    end
end)
Toggle(Weapon,"Auto Midnigh Blade","Auto Purchase Midnight Blade",1,"AutoMidnightBlade")
Toggle(Weapon,"Auto Rengoku","Auto Find Key and Open Chest",1,"AutoRengoku")
Toggle(Weapon,"Auto Kabucha","Auto Do Kabucha",1,"AutoKabucha")
Toggle(Weapon,"Auto Dragon Trident","Auto Find Dragon Trident",1,"AutoDragonTrident")
Weapon:Create({
    Text = "World 3"
},"Label",1)
Toggle(Weapon,"Auto Serpent Bow","Auto Find Serpent Bow",1,"AutoSerpentBow")
Toggle(Weapon,"Auto Twin hook","Auto Find Twin hook",1,"AutoTwinhook")
Toggle(Weapon,"Auto Buddy Sword","Auto Find Buddy Sword",1,"AutoBuddySword")
Toggle(Weapon,"Auto Yama","Auto get yama",1,"AutoYama")
Toggle(Weapon,"Auto Cavander","Auto get yama",1,"AutoCavander")
Toggle(Weapon,"Auto Hallow Scythe","kill bone boss",1,"AutoHallowScythe")
Toggle(Weapon,"Auto Buddy","kill Buddy boss",1,"AutoBuddy")
Toggle(Weapon,"Auto Tushita","use torch and kill longma",1,"AutoTushita")
Toggle(Weapon,"Auto Dark Dagger","kill rip_dra",1,"AutoDarkDagger")
Toggle(Weapon,"Auto Cursed Dual Katana","Do CDK",1,"AutoCursedDualKatana")

Weapon:Create({
    Text = "Accessory"
},"Label",2)

Toggle(Weapon,"Auto Bartilo Quest","Finish the Bartilo Quest Step by step",2,"AutoBartiloQuest")
Toggle(Weapon,"Auto Dark Coat","Auto Find Dark Coat",2,"AutoDarkCoat")
Toggle(Weapon,"Auto Swan Glasses","Auto Find Swan Glasses",2,"AutoSwanGlasses")
--[Race]--

Race:Create({
    Text = "Race V.4"
},"Label",1)

local FullMoon_Status = Race:Create({
    Text = "Status : "
},"Label",1)

task.spawn(function()
	while wait() do
		pcall(function()
			if game:GetService("Lighting").Sky.MoonTextureId=="http://www.roblox.com/asset/?id=9709149431" then
				FullMoon_Status.Text = "Status : 🌕 [Full Moon 100 %]"
            elseif game:GetService("Lighting").Sky.MoonTextureId=="http://www.roblox.com/asset/?id=9709149052" then
				FullMoon_Status.Text = "Status : 🌖 [Full Moon 75 %]"
            elseif game:GetService("Lighting").Sky.MoonTextureId=="http://www.roblox.com/asset/?id=9709143733" then
				FullMoon_Status.Text = "Status : 🌗 [Full Moon 50 %]"
            elseif game:GetService("Lighting").Sky.MoonTextureId=="http://www.roblox.com/asset/?id=9709150401" then
				FullMoon_Status.Text = "Status : 🌘 [Full Moon 25 %]"
            elseif game:GetService("Lighting").Sky.MoonTextureId=="http://www.roblox.com/asset/?id=9709149680" then
				FullMoon_Status.Text = "Status : 🌘 [Full Moon 15 %]"
            else
				FullMoon_Status.Text = "Status : 🌑 [Full Moon 0 %]"
            end
		end)
	end
end)

local Mirage_Island_Status = Race:Create({
    Text = "Mirage : "
},"Label",1)

task.spawn(function()
	while task.wait() do
		if game:GetService('Workspace').Map:FindFirstChild('MysticIsland') then
			Mirage_Island_Status.Text = "Mirage : Spawned"
		elseif game:GetService('Workspace')["_WorldOrigin"].Locations:FindFirstChild('MysticIsland') then
			Mirage_Island_Status.Text = "Mirage : Ready to Spawn"
		else
			Mirage_Island_Status.Text = "Mirage : Not Spawned"
		end
	end
end)

Toggle(Race,"Teleport To Gear","Teleport To Gear",1,"TeleportToGear")
Toggle(Race,"Teleport To Trial Door","Teleport To Trial Door",1,"TeleportToTrialDoor")
Toggle(Race,"Auto Pull Lever","Auto Pull Lever",1,function(value)
    if value then
        if game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("CheckTempleDoor") then
            fireproximityprompt(game:GetService("Workspace").Map["Temple of Time"].Lever.Prompt.ProximityPrompt,math.huge)
        end
    end
end)
Toggle(Race,"Auto AncientOne Quest","AutoAncientOneQuest",1,"AutoAncientOneQuest")
Toggle(Race,"Auto Active Ability","Auto Active Ability",1,function(value)
    while value and task.wait(.1) do
        if value then
            game:GetService("VirtualInputManager"):SendKeyEvent(true,"Y",false,game)
            task.wait()
            game:GetService("VirtualInputManager"):SendKeyEvent(false,"Y",false,game)
            game:GetService("ReplicatedStorage").Remotes.CommE:FireServer("ActivateAbility")
        end
    end
end)
Toggle(Race,"Auto Complete Trial","Auto Complete Trial",1,"AutoCompleteTrial")

Race:Create({
    Text = "Teleport To Temple Of Time",
    Callback = function() 
		game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(28286.35546875, 14895.3017578125, 102.62469482421875)
    end,
},"Button",1)

Race:Create({
    Text = "Teleport To Lever",
    Callback = function() 
		game:GetService("Players").LocalPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(28576.873046875, 14937.958984375, 76.49504852294922)
    end,
},"Button",1)

Race:Create({
    Text = "Race V.1-3"
},"Label",2)

Toggle(Race,"Auto Evolution Race V2","Evolution Race V2 Step by step",2,"AutoEvoRaceV2")

--[Visual]--

Visual:Create({
    Text = "Teleport World"
},"Label",1)

Visual:Create({
    Text = "Teleport Main",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelMain")
    end ;
},"Button",1)

Visual:Create({
    Text = "Teleport Dressrosa",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelDressrosa")
    end ;
},"Button",1)

Visual:Create({
    Text = "Teleport Zou",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("TravelZou")
    end ;
},"Button",1)

Visual:Create({
    Text = "Teleport Island"
},"Label",1)

Location = {}
for i,v in pairs(game:GetService("Workspace")["_WorldOrigin"].Locations:GetChildren()) do  
    table.insert(Location ,v.Name)
end

Dropdown(Visual,"Select Location","Sea",Location,1,"SelectIsland")
Toggle(Visual,"Teleport To Island","Start Teleprot Island",1,"TeleportIsland")

Visual:Create({
    Text = "Devil Fruit"
},"Label",1)

Toggle(Visual,"Auto Random Fruit","Auto Random Fruit",1,"AutoRandomFruit")
Toggle(Visual,"Auto Grab Fruit","Instant Teleport to fruit and Automatic Grab",1,"AutoCollectFruit")
Toggle(Visual,"Auto Store Fruit","Store fruit to Inventory",1,"AutoStoreFruit")
Toggle(Visual,"Auto Factory","Attack Factory Core",1,"AutoFactory")

Visual:Create({
    Text = "Raid"
},"Label",2)

Dropdown(Visual,"Microchip","CurrentFruit",RaidMicroship,2,"RaidMicroship")
Toggle(Visual,"Auto Start Raid",'Start Raid Automatically',2,"AutoStartRaid")
Toggle(Visual,"Auto Clear Raid",'Auto Clear Raid Automatically',2,"AutoRaid")
Toggle(Visual,"KillAura","Force NPC to dead state",2)
Toggle(Visual,"Auto Awaken","Auto Awake Fruit",2,"AutoAwaken")
Toggle(Visual,"Serverhop","Change server if current server is not available",2,"AutoRaidHop")
Slider(Visual,"Start After Level",1,MAXLEVEL,2,"AutoStartRaidLevel")
Slider(Visual,"Fragments Lock",0,math.huge,2,"LockFragmentsAmount")

Visual:Create({
	Text = "Color ESP"
},"Label",2)

Visual:Create({
    Text = "ESP Flower Color",
    Value = Color3.fromRGB(255, 0, 0),
   	Callback = function(value) 
		_G.ESP_Flower_Color = value
   end
},"ColorPicker",2)

Visual:Create({
    Text = "ESP Demon Fruit Color",
    Value = Color3.fromRGB(255, 0, 0),
   	Callback = function(value) 
       _G.ESP_Demon_Fruit_Color = value
   end
},"ColorPicker",2)

Visual:Create({
    Text = "ESP Chest Color",
    Value = Color3.fromRGB(255, 0, 0),
   	Callback = function(value) 
       _G.ESP_Chest_Color = value
   end
},"ColorPicker",2)


Visual:Create({
    Text = "ESP Island Color",
    Value = Color3.fromRGB(255, 0, 0),
   Callback = function(value) 
       _G.ESP_Island_Color = value
   end
},"ColorPicker",2)

Visual:Create({
	Text = "ESP"
},"Label",2)

local ESP = loadstring(game:HttpGet("https://raw.githubusercontent.com/hajibeza/File/main/ESP.lua"))()

Visual:Create({
	Text = "Flower Esp",
	Value = _G.FlowerEsp,
	Callback = function(value) 
		_G.FlowerEsp = value
		while _G.FlowerEsp do wait()
			FlowerESP()
		end
	end ,
},"Toggle",2)

Visual:Create({
	Text = "Demon Fruit Esp",
	Value = _G.DFEsp,
	Callback = function(value) 
		_G.DFEsp = value
		while _G.DFEsp do wait()
			UpdateBfEsp()
		end
	end ,
},"Toggle",2)

Visual:Create({
	Text = "Island Esp",
	Value = _G.IslandEsp,
	Callback = function(value) 
		_G.IslandEsp = value
		while _G.IslandEsp do wait()
			IslandESP()
		end
	end ,
},"Toggle",2)

Visual:Create({
	Text = "Chest Esp",
	Value = _G.ChestEsp,
	Callback = function(value) 
		_G.ChestEsp = value
		while _G.ChestEsp do wait()
			ChestSESP()
		end
	end ,
},"Toggle",2)

Visual:Create({
    Text = "Screen Kaitun"
},"Label",2)

Visual:Create({
    Text = "Kaitun Screen Capture",
    Callback = function()
        loadstring(game:HttpGet("https://raw.githubusercontent.com/hajibeza/File/main/Kaitun_Cap.lua"))()
    end;
},"Button",2)

Visual:Create({
    Text = "Destroy Screen Kaitun",
    Callback = function()
		game:GetService("TeleportService"):Teleport(game.PlaceId, game:GetService("Players").localPlayer)
    end ;
},"Button",2)

--[Combat]--

Combat:Create({
    Text = "Kill Player"
},"Label",1)

getplayers = {}
for i,v in pairs(game.Players:GetChildren()) do  
	if v.Name ~= game.Players.LocalPlayer.Name then
		table.insert(getplayers ,v.Name)
	end
end

local Player_Dropdown = Combat:Create({
    Text = "Select Player",
    Value = getplayers,
    Default = SelectPlayer, 
    Callback = function(value)
		SelectPlayer = value
    end ;   
},"Dropdown",1)

Combat:Create({
    Text = "Refresh Player",
    Callback = function()
		Player_Dropdown:Clear()
		for i,v in pairs(game.Players:GetChildren()) do  
			if v.Name ~= Client.Name then
				Player_Dropdown:Add(v.Name)
			end
		end
    end ;
},"Button",1)

Toggle(Combat,"Spectator Player",'Spectator Player',1,function(value)
    if value then
        if game.Players:FindFirstChild(SelectPlayer) then
            game.Workspace.Camera.CameraSubject = game.Players:FindFirstChild(SelectPlayer).Character.Humanoid
        end
    else
        game.Workspace.Camera.CameraSubject = game.Players.LocalPlayer.Character.Humanoid
    end
end)
Toggle(Combat,"Auto Kill Player",'Spectator Player',1,"AutoKillPlayer")
Toggle(Combat,"Teleport to Player",'Teleport to Player',1,"TeleporttoPlayer")

Combat:Create({
    Text = "Bring Player [Select Player]",
    Callback = function()
		Equip("Electric Claw")
		game:service('VirtualInputManager'):SendKeyEvent(true, "X", false, game)
		wait(.1)
		game:service('VirtualInputManager'):SendKeyEvent(false, "X", false, game)
		game.Players.LocalPlayer.Character.HumanoidRootPart.CFrame = game.Players[SelectPlayer].Character.HumanoidRootPart.CFrame	
    end ;
},"Button",1)

Combat:Create({
    Text = "Aimbot"
},"Label",1)

local lp = game:GetService('Players').LocalPlayer
local mouse = lp:GetMouse()
task.spawn(function()
	while wait() do
		if (AimbotSkill or AimbotGun) and SelectAimbotMode == "Fov" then
			pcall(function()
				local MaxDist, Closest = math.huge
				for i,v in pairs(game:GetService("Players"):GetChildren()) do 
					local Head = v.Character:FindFirstChild("HumanoidRootPart")
					local Pos, Vis = game.Workspace.CurrentCamera.WorldToScreenPoint(game.Workspace.CurrentCamera, Head.Position)
					local MousePos, TheirPos = Vector2.new(mouse.X, mouse.Y), Vector2.new(Pos.X, Pos.Y)
					local Dist = (TheirPos - MousePos).Magnitude
					if Dist < MaxDist and Dist <= tonumber(FovSize) and v.Name ~= game.Players.LocalPlayer.Name then
						MaxDist = Dist
						_G.Aim_Players = v
						_G.Aim_Gun_Player = v
					end
				end
			end)
		end
	end
end)

task.spawn(function()
	local gg = getrawmetatable(game)
	local old = gg.__namecall
	setreadonly(gg,false)
	gg.__namecall = newcclosure(function(...)
		local method = getnamecallmethod()
		local args = {...}
		if tostring(method) == "FireServer" then
			if tostring(args[1]) == "RemoteEvent" then
				if tostring(args[2]) ~= "true" and tostring(args[2]) ~= "false" then
                    if UseSkillMasteryDevilFruit and Settings.AutoFarmMastery and Settings.SelectMasteryMode == "Fruit Mastery" then
						if type(args[2]) == "vector" then 
							args[2] = PositionSkillMasteryDevilFruit
						else
							args[2] = CFrame.new(PositionSkillMasteryDevilFruit)
						end
						return old(unpack(args))
                    end
					if AimbotSkill and SelectAimbotMode == "Fov" then
						args[2] = _G.Aim_Players.Character.HumanoidRootPart.Position
						return old(unpack(args))
					elseif AimbotSkill and SelectAimbotMode == "Automatic" then
						args[2] = _G.Aim_Select_Players.Character.HumanoidRootPart.Position
						return old(unpack(args))
					end
				end
			end
		end
		return old(...)
	end)
end)

task.spawn(function()
	while wait() do
		for i,v in pairs(Client.Backpack:GetChildren()) do  
			if v:IsA("Tool") then
				if v:FindFirstChild("RemoteFunctionShoot") then 
					SelectWeaponGun = v.Name
				end
			end
		end
	end
end)

task.spawn(function()
	local gt = getrawmetatable(game)
	local old = gt.__namecall
	setreadonly(gt,false)
	gt.__namecall = newcclosure(function(...)
		local args = {...}
		if getnamecallmethod() == "InvokeServer" then 
			if SelectWeaponGun then
				if SelectWeaponGun == "Soul Guitar" then
					if tostring(args[2]) == "TAP" then
						if Settings.AutoFarmMastery and Settings.SelectMasteryMode == "Gun Mastery" and UseSkillMasteryGun then
							args[3] = PositionSkillMasteryGun
						end
					end
				end
			end
		end
		return old(unpack(args))
	end)
	setreadonly(gt,true)
end)

task.spawn(function()
	while wait() do
		pcall(function()
			if (AimbotSkill or AimbotGun) and SelectAimbotMode == "Automatic" then
				_G.Aim_Select_Players = game.Players:FindFirstChild(SelectPlayer)
			end
		end)
	end
end)

Combat:Create({Text = "Select Mode Aimbot" ,Value = {'Fov','Automatic'},Default = {'Fov'}, Callback = function(value)
    SelectAimbotMode = value
end,},"Dropdown",1)

local Circle = Drawing.new("Circle")
Circle.Thickness = 1
Circle.NumSides = 460
Circle.Filled = false
Circle.Transparency = 1

task.spawn(function()
	while task.wait() do
        if FovSize == nil then
            Circle.Radius = 250
        else
            Circle.Radius = FovSize
        end
		Circle.Thickness = 1
		Circle.NumSides = 460
		Circle.Position = game:GetService('UserInputService'):GetMouseLocation()
		if ShowFov then
			Circle.Visible = true
		else
			Circle.Visible = false
		end
		Circle.Color = FovColor
	end
end)

Combat:Create({Text = "Fov Color",Value = Color3.fromRGB(255, 0, 0),Callback = function(value) 
    FovColor = value
end},"ColorPicker",1)

Combat:Create({Text = "Fov Size" ,Value = 300,Max = 1000,Min = 1,Callback = function(value) 
    FovSize = value
end,},"Slider",1)

Combat:Create({Text = "Show Fov",Value = false,Callback = function(value) 
    ShowFov = value
end ,},"Toggle",1)

Combat:Create({Text = "Aimbot Skill",Value = false,Callback = function(value) 
    AimbotSkill = value
end ,},"Toggle",1)

Combat:Create({Text = "Aimbot Gun",Value = false,Callback = function(value) 
    AimbotGun = value
end ,},"Toggle",1)

task.spawn(function()
	while wait() do
		pcall(function()
			if AimbotGun and SelectAimbotMode == "Automatic" then
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild(SelectWeaponGun) and game:GetService("Players").LocalPlayer.Character:FindFirstChild(SelectWeaponGun):FindFirstChild("RemoteFunctionShoot") then
					repeat wait()
						game:GetService("Players").LocalPlayer.Character[SelectWeaponGun].RemoteFunctionShoot:InvokeServer(_G.Aim_Select_Players.Character.HumanoidRootPart.Position,_G.Aim_Select_Players.Character.HumanoidRootPart)
					until AimbotGun == false or game:GetService("Players").LocalPlayer.Character:FindFirstChild(SelectWeaponGun) == false
				end 
			elseif AimbotGun and SelectAimbotMode == "Fov" then
				if game:GetService("Players").LocalPlayer.Character:FindFirstChild(SelectWeaponGun) and game:GetService("Players").LocalPlayer.Character:FindFirstChild(SelectWeaponGun):FindFirstChild("RemoteFunctionShoot") then
					repeat wait()
						game:GetService("Players").LocalPlayer.Character[SelectWeaponGun].RemoteFunctionShoot:InvokeServer(_G.Aim_Players.Character.HumanoidRootPart.Position,_G.Aim_Players.Character.HumanoidRootPart)
					until AimbotGun == false or game:GetService("Players").LocalPlayer.Character:FindFirstChild(SelectWeaponGun) == false
				end 
			end
		end)
	end
end)

Combat:Create({
    Text = "Player"
},"Label",2)

Toggle(Combat,"Water Walk",'like it name',2,"WaterWalk")
Toggle(Combat,"Auto Damage","Auto Damage All Entities in Radius",2,"DamageAura")

Combat:Create({
    Text = "ESP"
},"Label",2)

Combat:Create({Text = "ESP Player Color",Value = Color3.fromRGB(255,0,0),Callback = function(value) 
    _G.ESP_Player_Color = value
end},"ColorPicker",2)

Combat:Create({Text = "ESP Player",Value = _G.ESP_Player,Callback = function(value) 
    _G.ESP_Player = value
	while _G.ESP_Player do wait()
		PlrESP()
	end
end ,},"Toggle",2)

Combat:Create({
    Text = "Team"
},"Label",2)

Combat:Create({Text = "Join Pirate Team",Callback = function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetTeam","Pirates") 
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress")
end,},"Button",2)

Combat:Create({Text = "Join Marin Team",Callback = function()
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("SetTeam","Marines") 
    game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BartiloQuestProgress")
end ;},"Button",2)

--[Misc]--
Misc:Create({
    Text = "Abilities"
},"Label",1)

Misc:Create({
    Text = "Auto Buy Ablility",
    Value = false,
    Callback = function(value) 
		AutoBuyAblility = value
    end ,
},"Toggle",1)

task.spawn(function()
    while wait() do
        pcall(function()
            if AutoBuyAblility then
                local Beli = game:GetService("Players").LocalPlayer.Data.Beli.Value
                local BusoCheck = false
                local SoruCheck = false
                local GeppoCheck = false
                local KenCheck = false
                if Beli >= 885000 then
                    repeat wait() 
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyHaki","Buso")
                        BusoCheck = true
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyHaki","Geppo")
                        GeppoCheck = true
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyHaki","Soru")
                        SoruCheck = true
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("KenTalk","Start")
                        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("KenTalk","Buy")
                        KenCheck = true
                    until not BusoCheck and not GeppoCheck and not SoruCheck and not KenCheck or not AutoBuyAblility
                end
            end
        end)
    end
end)

Misc:Create({
    Text = "Event"
},"Label",2)

Misc:Create({
    Text = "Auto Random Bone",
    Value = false,
    Callback = function(value) 
		AutoRandomBone = value
    end ,
},"Toggle",2)

task.spawn(function()
	while wait() do
		if AutoRandomBone then
			game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("Bones","Buy",1,1)
		end
	end
end)

Misc:Create({
    Text = "Refund Stat",
    Callback = function()
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Refund","1")
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Refund","2")
    end ;
},"Button",2):Add({
    Text = "Reroll Race",
    Callback = function()
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Reroll","1")
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Reroll","2")
    end
})

Misc:Create({
    Text = "Shop"
},"Label",2)

Misc:Create({
    Text = "Title Name",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("getTitles")
		game.Players.localPlayer.PlayerGui.Main.Titles.Visible = true
    end ;
},"Button",2):Add({
    Text = "Color Haki",
    Callback = function()
        game.Players.localPlayer.PlayerGui.Main.Colors.Visible = true
    end
})


Misc:Create({
    Text = "Combat"
},"Label",1)

Misc:Create({
    Text = "Black Leg",
    Callback = function()
        game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyBlackLeg")
    end ;
},"Button",1):Add({
    Text = "Electro",
    Callback = function()
        game:GetService("ReplicatedStorage").Remotes.CommF:InvokeServer("BuyElectro")
    end
}):Add({
    Text = "Fishman Karate",
    Callback = function()
        game:GetService("ReplicatedStorage").Remotes.CommF:InvokeServer("BuyFishmanKarate")
    end
})

Misc:Create({
    Text = "Dragon Claw",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","1")
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","DragonClaw","2")
    end ;
},"Button",1):Add({
    Text = "Superhuman",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuySuperhuman")
    end
}):Add({
    Text = "Death Step",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyDeathStep")
    end
})

Misc:Create({
    Text = "Electric Claw",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw",true)
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyElectricClaw")
    end ;
},"Button",1):Add({
    Text = "Dragon Talon",
    Callback = function()
        game:GetService("ReplicatedStorage").Remotes.CommF:InvokeServer("BuyDragonTalon",true)
        game:GetService("ReplicatedStorage").Remotes.CommF:InvokeServer("BuyDragonTalon")
    end
}):Add({
    Text = "Godhuman",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyGodhuman",true)
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyGodhuman")
    end
})

Misc:Create({
    Text = "Sword"
},"Label",1)

Misc:Create({
    Text = "Katana",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Katana")
    end ;
},"Button",1):Add({
    Text = "Cutlass",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Cutlass")
    end
}):Add({
    Text = "Duel Katana",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Duel Katana")
    end
})

Misc:Create({
    Text = "Iron Mace",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Iron Mace")
    end ;
},"Button",1):Add({
    Text = "Pipe",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Pipe")
    end
}):Add({
    Text = "Triple Katana",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Triple Katana")
    end
})

Misc:Create({
    Text = "Dual-Headed",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Dual-Headed Blade")
    end ;
},"Button",1):Add({
    Text = "Bisento",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Bisento")
    end
}):Add({
    Text = "Soul Cane",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Soul Cane")
    end
})

Misc:Create({
    Text = "Gun"
},"Label",1)

Misc:Create({
    Text = "Slingshot",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Slingshot")
    end ;
},"Button",1):Add({
    Text = "Musket",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Musket")
    end
}):Add({
    Text = "Flintlock",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Flintlock")
    end
})

Misc:Create({
    Text = "Refined Flintlock",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Refined Flintlock")
    end ;
},"Button",1):Add({
    Text = "Cannon",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BuyItem","Cannon")
    end
}):Add({
    Text = "Kabucha",
    Callback = function()
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Slingshot","1")
		game:GetService("ReplicatedStorage").Remotes.CommF_:InvokeServer("BlackbeardReward","Slingshot","2")
    end
})

Misc:Create({
    Text = "Fps"
},"Label",2)

Misc:Create({
    Text = "FPS Limit",
    Value = 120,
    Max = 240,
    Min = 5,
    Callback = function(value) 
		FPSLimit = value
		setfpscap(FPSLimit)
    end,
},"Slider",2)

Misc:Create({
    Text = "Main Misc"
},"Label",2)

local UserInputService = game:GetService("UserInputService")
local RunService = game:GetService("RunService")

Misc:Create({
	Text = "White Screen",
    Value = false,
    Callback = function(value) 
		WhiteScreen = value
		if value == true then
			RunService:Set3dRenderingEnabled(false)
			setfpscap(30)
		else
			RunService:Set3dRenderingEnabled(true)
			setfpscap(120)
		end
    end,
},"Toggle",2)

Misc:Create({
    Text = "No Fog",
    Value = false,
    Callback = function(value) 
		NoFog = value
    end,
},"Toggle",2)

task.spawn(function()
	while wait() do
		pcall(function()
			if NoFog then
				game.Lighting.FogEnd = math.huge
				if game:GetService("Lighting"):FindFirstChild("BaseAtmosphere") then
					game:GetService("Lighting"):FindFirstChild("BaseAtmosphere"):Destroy()
				end
			else
				game.Lighting.FogEnd = 2500
			end
		end)
	end
end)

Misc:Create({
    Text = "Remove Lava",
    Callback = function()
		for i,v in pairs(game.Workspace:GetDescendants()) do
			if v.Name == "Lava" then   
				v:Destroy()
			end
		end
		for i,v in pairs(game.ReplicatedStorage:GetDescendants()) do
			if v.Name == "Lava" then   
				v:Destroy()
			end
		end
    end ;
},"Button",2)

--[Setting]--

setting:Create({
    Text = "Hop"
},"Label",1)

setting:Create({
    Text = "Hop Server",
    Callback = function()
		Fast_Hop()
    end ;
},"Button",1)

setting:Create({
    Text = "Rejoin",
    Callback = function()
        game:GetService("TeleportService"):Teleport(game.PlaceId, game:GetService("Players").localPlayer)
    end ;
},"Button",1)

setting:Create({
    Text = "Server Info"
},"Label",2)

local Player_In_Server = setting:Create({
    Text = "Total Player : "
},"Label",2)

task.spawn(function()
	while wait() do
		Player_In_Server.Text = "Total Player : "..#game.Players:GetChildren()
	end
end)

local Total_Bounty = setting:Create({
    Text = "Total Bounty : "
},"Label",2)

task.spawn(function()
	while wait() do
		Total_Bounty.Text = "Total Bounty : "..game:GetService("Players").LocalPlayer.leaderstats["Bounty/Honor"].Value
	end
end)

local Job_ID = setting:Create({
    Text = "Job ID : "
},"Label",2)

task.spawn(function()
	while wait() do
		Job_ID.Text = "Job ID : "..game.JobId
	end
end)

setting:Create({
    Text = "Copy Job ID",
    Callback = function()
		setclipboard(game.JobId)
    end ;
},"Button",2)

local Crew_ID = setting:Create({
    Text = "Crew ID : "
},"Label",2)

task.spawn(function()
	while wait() do
		Crew_ID.Text = "Crew ID : "..game:GetService("Players").LocalPlayer.Data.CrewID.Value
	end
end)

local Total_Fruit = setting:Create({
    Text = "Total Fruit : "
},"Label",2)

task.spawn(function()
	while wait() do
		Total_Fruit.Text = "Total Fruit : "..game:GetService("Players").LocalPlayer.Data.CrewID.Value
	end
end)

setting:Create({
    Text = "Server"
},"Label",1)

setting:Create({
    Text = "Job ID",
    Placeholder = "Put Job ID",
    Callback = function(value) 
		Server_ID = value
    end;
},"TextBox",1)

setting:Create({
    Text = "Join Server",
    Callback = function()
		game.ReplicatedStorage['__ServerBrowser']:InvokeServer('teleport',"'"..Server_ID.."'")
    end ;
},"Button",1)

LaunchedSuccessfully = true

-- [[ Setting ]]

setting:Create({
    Text = "Change Main Toggle Color" ,
    Value = Color3.fromRGB(255,11,97),
    Callback = function(v)
        ColorSettings:Set("ToggleColor",v)
    end
},"ColorPicker",1)

setting:Create({
    Text = "Change Main Slider Color" ,
    Value = Color3.fromRGB(255,11,97),
    Callback = function(v)
        ColorSettings:Set("SliderColor",v)
    end
},"ColorPicker",1)

setting:Create({
    Text = "Change Main Dropdown Color" ,
    Value = Color3.fromRGB(255,11,97),
    Callback = function(v)
        ColorSettings:Set("DropdownClor",v)
    end
},"ColorPicker",1)

setting:Create({
    Text = "Change Main TextBox Color" ,
    Value = Color3.fromRGB(255,11,97),
    Callback = function(v)
        ColorSettings:Set("TextBoxColor",v)
    end
},"ColorPicker",1)

setting:Create({
    Text = "Change Main Button Color" ,
    Value = Color3.fromRGB(255,11,97),
    Callback = function(v)
        ColorSettings:Set("ButtonColor",v)
    end
},"ColorPicker",1)


setting:Create({
    Text = "Change MainBackground Color" ,
    Value = Color3.fromRGB(25,25,25),
    Callback = function(v)
        ColorSettings:Set("MainBackGroundColor",v)
    end
},"ColorPicker",2)

setting:Create({
    Text = "Change PageBackground Color" ,
    Value = Color3.fromRGB(30,30,30),
    Callback = function(v)
        ColorSettings:Set("PageBackground",v)
    end
},"ColorPicker",2)

setting:Create({
    Text = "Change StrokeBackground Color" ,
    Value = Color3.fromRGB(255,11,97),
    Callback = function(v)
        ColorSettings:Set("StrokeBackground",v)
    end
},"ColorPicker",2)

setting:Create({
    Text = "Change Page Color" ,
    Value = Color3.fromRGB(25,25,25),
    Callback = function(v)
        ColorSettings:Set("PageColor",v)
    end
},"ColorPicker",2)

setting:Create({
    Text = "Change Text Color" ,
    Value = Color3.fromRGB(255,255,255),
    Callback = function(v)
        ColorSettings:Set("TextColor",v)
    end
},"ColorPicker",2)
