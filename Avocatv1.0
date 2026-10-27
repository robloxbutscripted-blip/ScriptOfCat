pcall(function()
    local pg = game:GetService("Players").LocalPlayer:FindFirstChild("PlayerGui")
    if pg then
        local existing = pg:FindFirstChild("AvocatLoader")
        if existing then existing:Destroy() end
    end
end)

local TweenService = game:GetService("TweenService")
local UIS = game:GetService("UserInputService")
local LP = game:GetService("Players").LocalPlayer
local HS = game:GetService("HttpService")

local request = request or http_request or (syn and syn.request) or (http and http.request)

local WEBHOOK_LOGS = "https://discord.com/api/webhooks/1564710714919358534/jMObhNOGb0iHxM8-zfFPgpPRHIzpsi7PflNMjjDUftQhH4oe97axV_terteZhYElhJhl"
local HUB_URL = "https://raw.githubusercontent.com/Avocat547/Avocat-Hubbb/refs/heads/main/hub.lua"

local accentColor = Color3.fromRGB(180, 180, 180)
local openCount = 1


pcall(function()
    if isfile and readfile and writefile then
        local f = "AvocatHub_" .. LP.UserId .. ".txt"
        if isfile(f) then openCount = (tonumber(readfile(f)) or 1) + 1 end
        writefile(f, tostring(openCount))
    end
end)

local function getDeviceType()
    local ok, r = pcall(function()
        if UIS.TouchEnabled and not UIS.KeyboardEnabled then return "Mobile"
        elseif UIS.KeyboardEnabled and not UIS.TouchEnabled then return "PC"
        elseif UIS.GamepadEnabled then return "Console"
        else return "Unknown" end
    end)
    return ok and r or "Unknown"
end

local function getExecutor()
    if syn then return "Synapse X" end
    if KRNL_LOADED then return "KRNL" end
    if Fluxus then return "Fluxus" end
    if Delta then return "Delta" end
    if Solara then return "Solara" end
    if TRIGON_LOADED then return "Trigon" end
    if arceus then return "Arceus X" end
    if iselectron then return "Electron" end
    if SCRIPT_WARE_VERSION then return "Script-Ware" end
    if identifyexecutor then
        local ok, n = pcall(identifyexecutor)
        if ok and n then return n end
    end
    return "Unknown"
end

-- Server ID (game.JobId is empty in Studio and some reserved/private servers)
local function getServerId()
    local ok, id = pcall(function() return game.JobId end)
    if ok and id and id ~= "" then return id end
    return "N/A"
end


-- ==================== KEY SYSTEM ====================
local KEY = "Avocat v1.0"
local GET_KEY_LINK = "https://cdn.discordapp.com/attachments/1564710613077336096/1564761518661181520/Avocat_v1.0_Key.txt?ex=6ae27139&is=6ae11fb9&hm=ba4d8775d7d2db3e7120f34081bee47984af39549e22fa9ce22e18eb5620ec6d&" -- optional: link where users get the key (a "Get Key" button appears when this is filled)
local KEY_FILE = "AvocatHub_Key_" .. LP.UserId .. ".txt"

local function savedKeyIsValid()
    local ok, res = pcall(function()
        return isfile and readfile and isfile(KEY_FILE) and readfile(KEY_FILE) == KEY
    end)
    return ok and res == true
end

local function saveKey()
    pcall(function()
        if writefile then writefile(KEY_FILE, KEY) end
    end)
end

-- Returns true if the correct key was entered, false if the window was closed
local function promptForKey()
    local CG = game:GetService("CoreGui")
    pcall(function()
        local old = CG:FindFirstChild("AvocatKey")
        if old then old:Destroy() end
    end)

    local result = Instance.new("BindableEvent")

    local keyGui = Instance.new("ScreenGui")
    keyGui.Name = "AvocatKey"
    keyGui.ResetOnSpawn = false
    keyGui.IgnoreGuiInset = true
    keyGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
    keyGui.Parent = CG

    local win = Instance.new("Frame", keyGui)
    win.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
    win.BorderSizePixel = 0
    win.AnchorPoint = Vector2.new(0.5, 0.5)
    win.Position = UDim2.new(0.5, 0, 0.5, 0)
    win.Size = UDim2.new(0, 0, 0, 0)
    win.ClipsDescendants = true
    Instance.new("UICorner", win).CornerRadius = UDim.new(0, 10)

    local winStroke = Instance.new("UIStroke", win)
    winStroke.Color = Color3.fromRGB(34, 34, 34)
    winStroke.Thickness = 1

    -- Top bar
    local bar = Instance.new("Frame", win)
    bar.BackgroundColor3 = Color3.fromRGB(13, 13, 13)
    bar.BorderSizePixel = 0
    bar.Size = UDim2.new(1, 0, 0, 36)
    Instance.new("UICorner", bar).CornerRadius = UDim.new(0, 10)

    local barMask = Instance.new("Frame", bar)
    barMask.BackgroundColor3 = Color3.fromRGB(13, 13, 13)
    barMask.BorderSizePixel = 0
    barMask.Size = UDim2.new(1, 0, 0.5, 0)
    barMask.Position = UDim2.new(0, 0, 0.5, 0)

    local line = Instance.new("Frame", win)
    line.BackgroundColor3 = accentColor
    line.BackgroundTransparency = 0.5
    line.BorderSizePixel = 0
    line.Position = UDim2.new(0, 0, 0, 36)
    line.Size = UDim2.new(1, 0, 0, 1)

    local kdot = Instance.new("Frame", bar)
    kdot.BackgroundColor3 = accentColor
    kdot.BorderSizePixel = 0
    kdot.Size = UDim2.new(0, 8, 0, 8)
    kdot.Position = UDim2.new(0, 14, 0.5, -4)
    kdot.ZIndex = 4
    Instance.new("UICorner", kdot).CornerRadius = UDim.new(1, 0)

    local ktitle = Instance.new("TextLabel", bar)
    ktitle.BackgroundTransparency = 1
    ktitle.Position = UDim2.new(0, 30, 0, 0)
    ktitle.Size = UDim2.new(1, -70, 1, 0)
    ktitle.Font = Enum.Font.GothamBold
    ktitle.Text = "Avocat Hub - Key System"
    ktitle.TextColor3 = Color3.fromRGB(240, 240, 240)
    ktitle.TextSize = 13
    ktitle.TextXAlignment = Enum.TextXAlignment.Left
    ktitle.ZIndex = 4

    local closeBtn = Instance.new("TextButton", bar)
    closeBtn.BackgroundTransparency = 1
    closeBtn.Position = UDim2.new(1, -34, 0, 0)
    closeBtn.Size = UDim2.new(0, 30, 1, 0)
    closeBtn.Font = Enum.Font.GothamBold
    closeBtn.Text = "X"
    closeBtn.TextColor3 = Color3.fromRGB(120, 120, 125)
    closeBtn.TextSize = 12
    closeBtn.AutoButtonColor = false
    closeBtn.ZIndex = 5
    closeBtn.MouseEnter:Connect(function() closeBtn.TextColor3 = Color3.fromRGB(230, 230, 230) end)
    closeBtn.MouseLeave:Connect(function() closeBtn.TextColor3 = Color3.fromRGB(120, 120, 125) end)

    -- Prompt text
    local prompt = Instance.new("TextLabel", win)
    prompt.BackgroundTransparency = 1
    prompt.Position = UDim2.new(0, 18, 0, 46)
    prompt.Size = UDim2.new(1, -36, 0, 14)
    prompt.Font = Enum.Font.Gotham
    prompt.Text = "Enter your key to continue"
    prompt.TextColor3 = Color3.fromRGB(180, 180, 185)
    prompt.TextSize = 12
    prompt.TextXAlignment = Enum.TextXAlignment.Left

    -- Input field
    local inputBg = Instance.new("Frame", win)
    inputBg.BackgroundColor3 = Color3.fromRGB(18, 18, 18)
    inputBg.BorderSizePixel = 0
    inputBg.Position = UDim2.new(0, 18, 0, 68)
    inputBg.Size = UDim2.new(1, -36, 0, 32)
    Instance.new("UICorner", inputBg).CornerRadius = UDim.new(0, 6)
    local inputStroke = Instance.new("UIStroke", inputBg)
    inputStroke.Color = Color3.fromRGB(34, 34, 34)
    inputStroke.Thickness = 1

    local box = Instance.new("TextBox", inputBg)
    box.BackgroundTransparency = 1
    box.Position = UDim2.new(0, 10, 0, 0)
    box.Size = UDim2.new(1, -20, 1, 0)
    box.Font = Enum.Font.Gotham
    box.Text = ""
    box.PlaceholderText = "Enter key..."
    box.PlaceholderColor3 = Color3.fromRGB(90, 90, 95)
    box.TextColor3 = Color3.fromRGB(235, 235, 235)
    box.TextSize = 12
    box.TextXAlignment = Enum.TextXAlignment.Left
    box.ClearTextOnFocus = false

    local statusLbl

    -- Buttons
    local btnRow = Instance.new("Frame", win)
    btnRow.BackgroundTransparency = 1
    btnRow.Position = UDim2.new(0, 18, 0, 110)
    btnRow.Size = UDim2.new(1, -36, 0, 30)

    local function makeButton(text, primary, pos, size)
        local b = Instance.new("TextButton", btnRow)
        local base = primary and accentColor or Color3.fromRGB(28, 28, 28)
        local hover = primary and Color3.fromRGB(210, 210, 210) or Color3.fromRGB(42, 42, 42)
        b.BackgroundColor3 = base
        b.BorderSizePixel = 0
        b.Position = pos
        b.Size = size
        b.Font = Enum.Font.GothamBold
        b.Text = text
        b.TextColor3 = primary and Color3.fromRGB(10, 10, 10) or Color3.fromRGB(220, 220, 220)
        b.TextSize = 12
        b.AutoButtonColor = false
        Instance.new("UICorner", b).CornerRadius = UDim.new(0, 6)
        b.MouseEnter:Connect(function()
            TweenService:Create(b, TweenInfo.new(0.15), {BackgroundColor3 = hover}):Play()
        end)
        b.MouseLeave:Connect(function()
            TweenService:Create(b, TweenInfo.new(0.15), {BackgroundColor3 = base}):Play()
        end)
        return b
    end

    local verifyBtn
    if GET_KEY_LINK ~= "" then
        local getBtn = makeButton("Get Key", false, UDim2.new(0, 0, 0, 0), UDim2.new(0.5, -4, 1, 0))
        verifyBtn = makeButton("Verify Key", true, UDim2.new(0.5, 4, 0, 0), UDim2.new(0.5, -4, 1, 0))
        getBtn.MouseButton1Click:Connect(function()
            pcall(function() setclipboard(GET_KEY_LINK) end)
            statusLbl.Text = "Link copied to clipboard"
            statusLbl.TextColor3 = Color3.fromRGB(180, 180, 185)
        end)
    else
        verifyBtn = makeButton("Verify Key", true, UDim2.new(0, 0, 0, 0), UDim2.new(1, 0, 1, 0))
    end

    -- Status line
    statusLbl = Instance.new("TextLabel", win)
    statusLbl.BackgroundTransparency = 1
    statusLbl.Position = UDim2.new(0, 18, 0, 148)
    statusLbl.Size = UDim2.new(1, -36, 0, 14)
    statusLbl.Font = Enum.Font.Gotham
    statusLbl.Text = ""
    statusLbl.TextColor3 = Color3.fromRGB(180, 180, 185)
    statusLbl.TextSize = 11
    statusLbl.TextXAlignment = Enum.TextXAlignment.Left

    local function shake()
        for _, dx in ipairs({-8, 8, -5, 5, 0}) do
            local t = TweenService:Create(win, TweenInfo.new(0.05, Enum.EasingStyle.Quad),
                {Position = UDim2.new(0.5, dx, 0.5, 0)})
            t:Play()
            t.Completed:Wait()
        end
    end

    local busy = false
    local function verify()
        if busy then return end
        busy = true
        local input = string.match(box.Text, "^%s*(.-)%s*$") or ""
        if input == KEY then
            statusLbl.Text = "Key accepted"
            statusLbl.TextColor3 = Color3.fromRGB(120, 200, 140)
            saveKey()
            task.wait(0.5)
            result:Fire(true)
        else
            statusLbl.Text = (input == "") and "Please enter a key" or "Invalid key, try again"
            statusLbl.TextColor3 = Color3.fromRGB(220, 90, 90)
            shake()
            busy = false
        end
    end

    verifyBtn.MouseButton1Click:Connect(verify)
    box.FocusLost:Connect(function(enterPressed)
        if enterPressed then verify() end
    end)
    closeBtn.MouseButton1Click:Connect(function() result:Fire(false) end)

    TweenService:Create(win, TweenInfo.new(0.5, Enum.EasingStyle.Quint, Enum.EasingDirection.Out),
        {Size = UDim2.new(0, 320, 0, 172)}):Play()

    local accepted = result.Event:Wait()

    TweenService:Create(win, TweenInfo.new(0.3, Enum.EasingStyle.Quint, Enum.EasingDirection.In),
        {Size = UDim2.new(0, 0, 0, 0)}):Play()
    task.wait(0.35)
    keyGui:Destroy()
    result:Destroy()
    return accepted
end

if not savedKeyIsValid() then
    if not promptForKey() then
        return
    end
end
-- ================== END KEY SYSTEM ==================


local gameName = "Unknown"
task.spawn(function()
    pcall(function()
        gameName = game:GetService("MarketplaceService"):GetProductInfo(game.PlaceId).Name
    end)
end)
task.wait(2) -- attend max 2s puis continue quoi qu'il arrive


local CoreGui = game:GetService("CoreGui")

local gui = Instance.new("ScreenGui")
gui.Name = "AvocatLoader"
gui.ResetOnSpawn = false
gui.IgnoreGuiInset = true
gui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
gui.Parent = CoreGui -- CoreGui au lieu de PlayerGui, jamais bloquant

local box = Instance.new("Frame", gui)
box.BackgroundColor3 = Color3.fromRGB(10, 10, 10)
box.BorderSizePixel = 0
box.AnchorPoint = Vector2.new(0.5, 0.5)
box.Position = UDim2.new(0.5, 0, 0.5, 0)
box.Size = UDim2.new(0, 0, 0, 0)
box.ClipsDescendants = true
Instance.new("UICorner", box).CornerRadius = UDim.new(0, 10)

local stroke = Instance.new("UIStroke", box)
stroke.Color = Color3.fromRGB(34, 34, 34)
stroke.Thickness = 1

local topBar = Instance.new("Frame", box)
topBar.BackgroundColor3 = Color3.fromRGB(13, 13, 13)
topBar.BorderSizePixel = 0
topBar.Size = UDim2.new(1, 0, 0, 36)
Instance.new("UICorner", topBar).CornerRadius = UDim.new(0, 10)

local topBarMask = Instance.new("Frame", topBar)
topBarMask.BackgroundColor3 = Color3.fromRGB(13, 13, 13)
topBarMask.BorderSizePixel = 0
topBarMask.Size = UDim2.new(1, 0, 0.5, 0)
topBarMask.Position = UDim2.new(0, 0, 0.5, 0)

local accentLine = Instance.new("Frame", box)
accentLine.BackgroundColor3 = accentColor
accentLine.BorderSizePixel = 0
accentLine.Position = UDim2.new(0, 0, 0, 36)
accentLine.Size = UDim2.new(1, 0, 0, 1)
accentLine.BackgroundTransparency = 0.5

local dot = Instance.new("Frame", topBar)
dot.BackgroundColor3 = accentColor
dot.BorderSizePixel = 0
dot.Size = UDim2.new(0, 8, 0, 8)
dot.Position = UDim2.new(0, 14, 0.5, -4)
dot.ZIndex = 4
Instance.new("UICorner", dot).CornerRadius = UDim.new(1, 0)

local dotGlow = Instance.new("Frame", dot)
dotGlow.BackgroundColor3 = accentColor
dotGlow.BackgroundTransparency = 0.6
dotGlow.BorderSizePixel = 0
dotGlow.Size = UDim2.new(1, 6, 1, 6)
dotGlow.Position = UDim2.new(0, -3, 0, -3)
dotGlow.ZIndex = 3
Instance.new("UICorner", dotGlow).CornerRadius = UDim.new(1, 0)

task.spawn(function()
    while dot and dot.Parent do
        TweenService:Create(dotGlow, TweenInfo.new(0.9, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut),
            {BackgroundTransparency = 0.85}):Play()
        task.wait(0.9)
        if not dot or not dot.Parent then break end
        TweenService:Create(dotGlow, TweenInfo.new(0.9, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut),
            {BackgroundTransparency = 0.35}):Play()
        task.wait(0.9)
    end
end)

local title = Instance.new("TextLabel", topBar)
title.BackgroundTransparency = 1
title.Position = UDim2.new(0, 30, 0, 0)
title.Size = UDim2.new(0, 120, 1, 0)
title.Font = Enum.Font.GothamBold
title.Text = "Avocat Hub"
title.TextColor3 = Color3.fromRGB(240, 240, 240)
title.TextSize = 13
title.TextXAlignment = Enum.TextXAlignment.Left
title.ZIndex = 4

local version = Instance.new("TextLabel", topBar)
version.BackgroundTransparency = 1
version.Position = UDim2.new(1, -50, 0, 0)
version.Size = UDim2.new(0, 40, 1, 0)
version.Font = Enum.Font.Gotham
version.Text = "v1.0"
version.TextColor3 = Color3.fromRGB(120, 120, 125)
version.TextSize = 11
version.TextXAlignment = Enum.TextXAlignment.Right
version.ZIndex = 4

local status = Instance.new("TextLabel", box)
status.BackgroundTransparency = 1
status.Position = UDim2.new(0, 18, 0, 50)
status.Size = UDim2.new(1, -70, 0, 14)
status.Font = Enum.Font.Gotham
status.Text = "Loading..."
status.TextColor3 = Color3.fromRGB(180, 180, 185)
status.TextSize = 12
status.TextXAlignment = Enum.TextXAlignment.Left

local percent = Instance.new("TextLabel", box)
percent.BackgroundTransparency = 1
percent.Position = UDim2.new(1, -50, 0, 50)
percent.Size = UDim2.new(0, 32, 0, 14)
percent.Font = Enum.Font.GothamMedium
percent.Text = "0%"
percent.TextColor3 = accentColor
percent.TextSize = 12
percent.TextXAlignment = Enum.TextXAlignment.Right

local barBg = Instance.new("Frame", box)
barBg.BackgroundColor3 = Color3.fromRGB(28, 28, 28)
barBg.BorderSizePixel = 0
barBg.Position = UDim2.new(0, 18, 0, 74)
barBg.Size = UDim2.new(1, -36, 0, 5)
Instance.new("UICorner", barBg).CornerRadius = UDim.new(1, 0)

local barFill = Instance.new("Frame", barBg)
barFill.BackgroundColor3 = accentColor
barFill.BorderSizePixel = 0
barFill.Size = UDim2.new(0, 0, 1, 0)
Instance.new("UICorner", barFill).CornerRadius = UDim.new(1, 0)

local infoLine = Instance.new("TextLabel", box)
infoLine.BackgroundTransparency = 1
infoLine.Position = UDim2.new(0, 18, 0, 88)
infoLine.Size = UDim2.new(1, -36, 0, 12)
infoLine.Font = Enum.Font.Gotham
infoLine.Text = gameName
infoLine.TextColor3 = Color3.fromRGB(105, 105, 115)
infoLine.TextSize = 10
infoLine.TextXAlignment = Enum.TextXAlignment.Left
infoLine.TextTruncate = Enum.TextTruncate.AtEnd

TweenService:Create(box, TweenInfo.new(0.5, Enum.EasingStyle.Quint, Enum.EasingDirection.Out),
    {Size = UDim2.new(0, 320, 0, 108)}):Play()
task.wait(0.5)

local steps = {"Loading...", "Initializing...", "Almost ready...", "Launching..."}
for i, txt in ipairs(steps) do
    status.Text = txt
    local progress = i / #steps
    TweenService:Create(barFill, TweenInfo.new(0.4, Enum.EasingStyle.Quart),
        {Size = UDim2.new(progress, 0, 1, 0)}):Play()
    local startVal = tonumber((percent.Text:gsub("%%", ""))) or 0
    local endVal = math.floor(progress * 100)
    for j = 1, 20 do
        percent.Text = math.floor(startVal + (endVal - startVal) * (j / 20)) .. "%"
        task.wait(0.02)
    end
    task.wait(0.1)
end


task.spawn(function()
    pcall(function()
        if not request then return end
        local userStatus = openCount >= 50 and "VIP User"
            or openCount >= 10 and "Frequent User"
            or openCount > 1 and "Returning User" or "New User"
        local statusColor = openCount >= 50 and 0xDCDCDC
            or openCount >= 10 and 0xC8C8C8
            or openCount > 1 and 0xAFAFAF or 0xB4B4B4
        local serverId = getServerId()
        local serverValue = "`"..serverId.."`"
        if serverId ~= "N/A" then
            serverValue = serverValue.."\n[▶ Join Server](https://www.roblox.com/games/start?placeId="..game.PlaceId.."&gameInstanceId="..serverId..")"
        end
        request({
            Url = WEBHOOK_LOGS,
            Method = "POST",
            Headers = {["Content-Type"] = "application/json"},
            Body = HS:JSONEncode({
                embeds = {{
                    title = "Avocat Hub - " .. userStatus,
                    description = "Analytics Report",
                    color = statusColor,
                    fields = {
                        {name="Player", value=LP.DisplayName.." (@"..LP.Name..")\nID: "..LP.UserId, inline=false},
                        {name="Usage", value="Opens: "..openCount.."\nStatus: "..userStatus, inline=false},
                        {name="Game", value=gameName.."\nID: "..game.PlaceId.."\n[Join](https://www.roblox.com/games/"..game.PlaceId..")", inline=false},
                        {name="Server", value=serverValue, inline=false},
                        {name="System", value="Device: "..getDeviceType().."\nExecutor: "..getExecutor(), inline=false},
                    },
                    footer = {text = "Avocat Hub V1.0 | Session #"..openCount}
                }}
            })
        })
    end)
end)

task.wait(0.3)
TweenService:Create(box, TweenInfo.new(0.35, Enum.EasingStyle.Quint, Enum.EasingDirection.In),
    {Size = UDim2.new(0, 0, 0, 0)}):Play()
task.wait(0.4)
gui:Destroy()

-- Retry x3
local loaded = false
for attempt = 1, 3 do
    local ok, err = pcall(function()
        loadstring(game:HttpGet(HUB_URL .. "?cb=" .. tostring(os.time())))()
    end)
    if ok then
        loaded = true
        break
    else
        warn("[Avocat Hub] Tentative " .. attempt .. " echouee: " .. tostring(err))
        task.wait(1)
    end
end

if not loaded then
    warn("[Avocat Hub] Echec total du chargement.")
end
