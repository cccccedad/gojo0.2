-- ============================================================
-- Black Flash - Key System + Combat + Batata + Mobile + GOJO 0.2 (Fixed)
-- ============================================================

local Players = game:GetService("Players")
local Lighting = game:GetService("Lighting")
local UserInputService = game:GetService("UserInputService")
local VirtualInputManager = game:GetService("VirtualInputManager")
local RunService = game:GetService("RunService")
local Workspace = game:GetService("Workspace")
local CoreGui = game:GetService("CoreGui")
local Player = Players.LocalPlayer

-- ============================================================
-- JUNKIE
-- ============================================================

local Junkie = loadstring(game:HttpGet(
    "https://jnkie.com/sdk/library.lua"
))()

local IDENTIFIER = "1177694"

local PROVIDERS = {
    Linkvertise = {
        service = "Black Flash key",
        provider = "Key"
    },
    Workink = {
        service = "Black Flash key2",
        provider = "Key-work.ink"
    }
}

local function setupProvider(providerData)
    Junkie.identifier = IDENTIFIER
    Junkie.service = providerData.service
    Junkie.provider = providerData.provider
end

local function getProviderLink(providerData)
    local success, result = pcall(function()
        setupProvider(providerData)
        return Junkie.get_key_link()
    end)

    if success and result then
        return result
    end

    return nil
end

local function verifyKey(key)
    do
        local success, result = pcall(function()
            setupProvider(PROVIDERS.Linkvertise)
            return Junkie.check_key(key)
        end)

        if success and result and result.valid then
            return true, "Linkvertise"
        end
    end

    do
        local success, result = pcall(function()
            setupProvider(PROVIDERS.Workink)
            return Junkie.check_key(key)
        end)

        if success and result and result.valid then
            return true, "Work.ink"
        end
    end

    return false, nil
end

-- ============================================================
-- LIMPA UI ANTIGA
-- ============================================================

if Player.PlayerGui:FindFirstChild("BlackFlashKeySystem") then
    Player.PlayerGui.BlackFlashKeySystem:Destroy()
end

-- ============================================================
-- KEY SYSTEM
-- ============================================================

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "BlackFlashKeySystem"
ScreenGui.ResetOnSpawn = false
ScreenGui.IgnoreGuiInset = true

local successGui = pcall(function()
    ScreenGui.Parent = CoreGui
end)

if not successGui then
    ScreenGui.Parent = Player.PlayerGui
end

local Main = Instance.new("Frame")
Main.Size = UDim2.fromOffset(390, 285)
Main.Position = UDim2.new(0.5, -195, 0.5, -142)
Main.BackgroundColor3 = Color3.fromRGB(13, 17, 23)
Main.BorderSizePixel = 0
Main.Active = true
Main.Draggable = true
Main.Parent = ScreenGui

local MainCorner = Instance.new("UICorner")
MainCorner.CornerRadius = UDim.new(0, 14)
MainCorner.Parent = Main

local MainStroke = Instance.new("UIStroke")
MainStroke.Color = Color3.fromRGB(48, 54, 61)
MainStroke.Thickness = 1
MainStroke.Parent = Main

local Header = Instance.new("Frame")
Header.Size = UDim2.new(1, 0, 0, 48)
Header.BackgroundColor3 = Color3.fromRGB(22, 27, 34)
Header.BorderSizePixel = 0
Header.Parent = Main

local HeaderCorner = Instance.new("UICorner")
HeaderCorner.CornerRadius = UDim.new(0, 14)
HeaderCorner.Parent = Header

local HeaderFix = Instance.new("Frame")
HeaderFix.Size = UDim2.new(1, 0, 0, 15)
HeaderFix.Position = UDim2.new(0, 0, 1, -15)
HeaderFix.BackgroundColor3 = Color3.fromRGB(22, 27, 34)
HeaderFix.BorderSizePixel = 0
HeaderFix.Parent = Header

local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, -60, 1, 0)
Title.Position = UDim2.new(0, 18, 0, 0)
Title.BackgroundTransparency = 1
Title.Text = "Black Flash"
Title.TextColor3 = Color3.fromRGB(230, 237, 243)
Title.TextSize = 17
Title.Font = Enum.Font.GothamBold
Title.TextXAlignment = Enum.TextXAlignment.Left
Title.Parent = Header

local Close = Instance.new("TextButton")
Close.Size = UDim2.fromOffset(30, 30)
Close.Position = UDim2.new(1, -40, 0.5, -15)
Close.BackgroundColor3 = Color3.fromRGB(248, 81, 73)
Close.BackgroundTransparency = 0.75
Close.BorderSizePixel = 0
Close.Text = "×"
Close.TextColor3 = Color3.fromRGB(255, 255, 255)
Close.TextSize = 20
Close.Font = Enum.Font.GothamBold
Close.Parent = Header

local CloseCorner = Instance.new("UICorner")
CloseCorner.CornerRadius = UDim.new(0, 8)
CloseCorner.Parent = Close

Close.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

local Subtitle = Instance.new("TextLabel")
Subtitle.Size = UDim2.new(1, -40, 0, 25)
Subtitle.Position = UDim2.new(0, 20, 0, 62)
Subtitle.BackgroundTransparency = 1
Subtitle.Text = "Enter your verification key"
Subtitle.TextColor3 = Color3.fromRGB(139, 148, 158)
Subtitle.TextSize = 13
Subtitle.Font = Enum.Font.Gotham
Subtitle.TextXAlignment = Enum.TextXAlignment.Center
Subtitle.Parent = Main

local KeyBox = Instance.new("TextBox")
KeyBox.Size = UDim2.new(1, -40, 0, 45)
KeyBox.Position = UDim2.new(0, 20, 0, 95)
KeyBox.BackgroundColor3 = Color3.fromRGB(30, 36, 44)
KeyBox.BorderSizePixel = 0
KeyBox.PlaceholderText = "Cole sua Key aqui..."
KeyBox.PlaceholderColor3 = Color3.fromRGB(110, 118, 129)
KeyBox.Text = ""
KeyBox.TextColor3 = Color3.fromRGB(230, 237, 243)
KeyBox.TextSize = 14
KeyBox.Font = Enum.Font.Gotham
KeyBox.ClearTextOnFocus = false
KeyBox.Parent = Main

local KeyCorner = Instance.new("UICorner")
KeyCorner.CornerRadius = UDim.new(0, 10)
KeyCorner.Parent = KeyBox

local KeyStroke = Instance.new("UIStroke")
KeyStroke.Color = Color3.fromRGB(48, 54, 61)
KeyStroke.Thickness = 1
KeyStroke.Parent = KeyBox

local Linkvertise = Instance.new("TextButton")
Linkvertise.Size = UDim2.new(0.5, -25, 0, 40)
Linkvertise.Position = UDim2.new(0, 20, 0, 153)
Linkvertise.BackgroundColor3 = Color3.fromRGB(88, 166, 255)
Linkvertise.BorderSizePixel = 0
Linkvertise.Text = "Linkvertise"
Linkvertise.TextColor3 = Color3.fromRGB(255, 255, 255)
Linkvertise.TextSize = 13
Linkvertise.Font = Enum.Font.GothamBold
Linkvertise.Parent = Main

local LVCorner = Instance.new("UICorner")
LVCorner.CornerRadius = UDim.new(0, 9)
LVCorner.Parent = Linkvertise

local Workink = Instance.new("TextButton")
Workink.Size = UDim2.new(0.5, -25, 0, 40)
Workink.Position = UDim2.new(0.5, 5, 0, 153)
Workink.BackgroundColor3 = Color3.fromRGB(47, 183, 117)
Workink.BorderSizePixel = 0
Workink.Text = "Work.ink"
Workink.TextColor3 = Color3.fromRGB(255, 255, 255)
Workink.TextSize = 13
Workink.Font = Enum.Font.GothamBold
Workink.Parent = Main

local WICorner = Instance.new("UICorner")
WICorner.CornerRadius = UDim.new(0, 9)
WICorner.Parent = Workink

local Verify = Instance.new("TextButton")
Verify.Size = UDim2.new(1, -40, 0, 40)
Verify.Position = UDim2.new(0, 20, 0, 203)
Verify.BackgroundColor3 = Color3.fromRGB(136, 87, 224)
Verify.BorderSizePixel = 0
Verify.Text = "Verificar Key"
Verify.TextColor3 = Color3.fromRGB(255, 255, 255)
Verify.TextSize = 14
Verify.Font = Enum.Font.GothamBold
Verify.Parent = Main

local VerifyCorner = Instance.new("UICorner")
VerifyCorner.CornerRadius = UDim.new(0, 9)
VerifyCorner.Parent = Verify

local Status = Instance.new("TextLabel")
Status.Size = UDim2.new(1, -40, 0, 25)
Status.Position = UDim2.new(0, 20, 0, 248)
Status.BackgroundTransparency = 1
Status.Text = "Escolha um provedor para obter sua key."
Status.TextColor3 = Color3.fromRGB(139, 148, 158)
Status.TextSize = 11
Status.Font = Enum.Font.Gotham
Status.TextXAlignment = Enum.TextXAlignment.Center
Status.Parent = Main

local function setStatus(text, color)
    Status.Text = text
    Status.TextColor3 = color or Color3.fromRGB(139, 148, 158)
end

Linkvertise.MouseButton1Click:Connect(function()
    setStatus("Obtendo link do Linkvertise...", Color3.fromRGB(88, 166, 255))

    local link = getProviderLink(PROVIDERS.Linkvertise)

    if link then
        if setclipboard then
            setclipboard(link)
            setStatus("Linkvertise copiado!", Color3.fromRGB(47, 183, 117))
        else
            setStatus(link, Color3.fromRGB(88, 166, 255))
        end
    else
        setStatus("Não foi possível obter.", Color3.fromRGB(248, 81, 73))
    end
end)

Workink.MouseButton1Click:Connect(function()
    setStatus("Obtendo link do Work.ink...", Color3.fromRGB(47, 183, 117))

    local link = getProviderLink(PROVIDERS.Workink)

    if link then
        if setclipboard then
            setclipboard(link)
            setStatus("Work.ink copiado!", Color3.fromRGB(47, 183, 117))
        else
            setStatus(link, Color3.fromRGB(88, 166, 255))
        end
    else
        setStatus("Não foi possível obter.", Color3.fromRGB(248, 81, 73))
    end
end)

-- ============================================================
-- SCRIPT PRINCIPAL
-- ============================================================

local function StartBlackFlash()

    local Fluent = loadstring(game:HttpGet(
        "https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"
    ))()

    local Window = Fluent:CreateWindow({
        Title = "Jujutsu Shenanigans",
        SubTitle = "GOJO 0.2",
        TabWidth = 140,
        Size = UDim2.fromOffset(430, 290),
        Acrylic = false,
        Theme = "Dark",
        MinimizeKey = Enum.KeyCode.LeftControl
    })

    local Tabs = {

        Gojo = Window:AddTab({
            Title = "GOJO 0.2",
            Icon = "zap"
        }),

        -- ====================================================
        -- NOVA ABA: INFORMAÇÕES
        -- ====================================================

        Informacoes = Window:AddTab({
            Title = "Informações",
            Icon = "info"
        })

    }

    -- ========================================================
    -- CONTEÚDO DA ABA INFORMAÇÕES
    -- ========================================================

    Tabs.Informacoes:AddParagraph({
        Title = "Português",
        Content = "Utilize o Bypass até você conseguir dar teleporte em um player, caso não dê o teleporte se jogue no void e tente novamente."
    })

    Tabs.Informacoes:AddParagraph({
        Title = "English",
        Content = "Use the Bypass until you are able to teleport to a player, if the teleport does not work, jump into the void and try again."
    })

    -- ========================================================
    -- GOJO
    -- ========================================================

    local GojoAtivo = false
    local GojoAutoTeleport = false
    local GojoNoclip = false
    local GojoAutoAttack = false
    local GojoAttackDelay = 0.3
    local GojoNpcRefresh = 1
    local GojoNpcCache = {}
    local GojoNpcCacheTime = 0

    local function GojoGetHRP()
        local character = Player.Character

        if not character then
            return nil
        end

        return character:FindFirstChild("HumanoidRootPart")
    end

    local function GojoSetCollision(value)
        local character = Player.Character

        if not character then
            return
        end

        for _, obj in ipairs(character:GetDescendants()) do
            if obj:IsA("BasePart") then
                obj.CanCollide = value
            end
        end
    end

    local function GojoGetPlayers()
        local result = {}

        for _, otherPlayer in ipairs(Players:GetPlayers()) do
            if otherPlayer ~= Player and otherPlayer.Character then

                local root =
                    otherPlayer.Character:FindFirstChild("HumanoidRootPart")

                local humanoid =
                    otherPlayer.Character:FindFirstChildOfClass("Humanoid")

                if root and humanoid and humanoid.Health > 0 then
                    table.insert(result, root)
                end
            end
        end

        return result
    end

    local function GojoRefreshNPCs()

        local newCache = {}
        local seen = {}

        for _, obj in ipairs(Workspace:GetDescendants()) do

            if obj:IsA("Model")
                and obj ~= Player.Character
                and not obj:IsA("Tool") then

                local humanoid =
                    obj:FindFirstChildOfClass("Humanoid")

                local root =
                    obj:FindFirstChild("HumanoidRootPart")
                    or obj:FindFirstChild("UpperTorso")
                    or obj:FindFirstChild("Torso")

                if humanoid
                    and root
                    and humanoid.Health > 0
                    and not seen[humanoid] then

                    local isPlayerCharacter = false

                    for _, otherPlayer in ipairs(Players:GetPlayers()) do
                        if otherPlayer.Character == obj then
                            isPlayerCharacter = true
                            break
                        end
                    end

                    if not isPlayerCharacter and obj.Parent then

                        seen[humanoid] = true

                        table.insert(newCache, {
                            Root = root,
                            Hum = humanoid,
                            Model = obj
                        })

                    end
                end
            end
        end

        GojoNpcCache = newCache
    end

    local function GojoGetTargets()

        local targets = {}

        for _, root in ipairs(GojoGetPlayers()) do
            table.insert(targets, root)
        end

        if os.clock() - GojoNpcCacheTime > GojoNpcRefresh then
            GojoRefreshNPCs()
            GojoNpcCacheTime = os.clock()
        end

        for _, npc in ipairs(GojoNpcCache) do

            if npc.Root
                and npc.Root.Parent
                and npc.Hum
                and npc.Hum.Health > 0 then

                table.insert(targets, npc.Root)
            end
        end

        return targets
    end

    local function GojoGetNearestTarget(position)

        local best = nil
        local bestDistance = math.huge

        for _, root in ipairs(GojoGetTargets()) do

            if root and root.Parent then

                local distance =
                    (root.Position - position).Magnitude

                if distance < bestDistance then
                    bestDistance = distance
                    best = root
                end
            end
        end

        return best, bestDistance
    end

    task.spawn(function()

        while true do

            if GojoAtivo and GojoAutoTeleport then

                local myRoot = GojoGetHRP()

                if myRoot then

                    local targets = GojoGetTargets()

                    if #targets > 0 then

                        local target =
                            targets[math.random(1, #targets)]

                        if target and target.Parent then

                            local offsets = {
                                CFrame.new(0, 0, 4),
                                CFrame.new(0, 0, -4),
                                CFrame.new(4, 0, 0),
                                CFrame.new(-4, 0, 0)
                            }

                            local offset =
                                offsets[math.random(1, #offsets)]

                            myRoot.CFrame =
                                CFrame.lookAt(
                                    (target.CFrame * offset).Position,
                                    target.Position
                                )
                        end
                    end
                end
            end

            RunService.Heartbeat:Wait()
        end
    end)

    RunService.Stepped:Connect(function()

        if GojoAtivo and GojoNoclip then
            GojoSetCollision(false)
        end
    end)

    task.spawn(function()

        while true do

            if GojoAtivo and GojoAutoAttack then

                local myRoot = GojoGetHRP()

                if myRoot then

                    local target, distance =
                        GojoGetNearestTarget(myRoot.Position)

                    if target and target.Parent then

                        if distance > 12 then

                            myRoot.CFrame =
                                CFrame.lookAt(
                                    (target.CFrame * CFrame.new(0, 0, 5)).Position,
                                    target.Position
                                )

                            RunService.Heartbeat:Wait()
                        end

                        myRoot.CFrame =
                            CFrame.lookAt(
                                myRoot.Position,
                                target.Position
                            )

                        local Camera = Workspace.CurrentCamera

                        if Camera then

                            Camera.CFrame =
                                CFrame.lookAt(
                                    Camera.CFrame.Position,
                                    target.Position
                                )

                            RunService.RenderStepped:Wait()
                        end
                    end
                end
            end

            task.wait(GojoAttackDelay)
        end
    end)

    local GojoToggle = Tabs.Gojo:AddToggle("Gojo02Toggle", {
        Title = "GOJO 0.2",
        Description = "Teleporte",
        Default = false
    })

    GojoToggle:OnChanged(function(Value)

        GojoAtivo = Value

        if Value then

            GojoAutoTeleport = true
            GojoNoclip = true
            GojoAutoAttack = true

            Fluent:Notify({
                Title = "GOJO 0.2",
                Content = "",
                Duration = 0
            })

        else

            GojoAutoTeleport = false
            GojoNoclip = false
            GojoAutoAttack = false

            GojoSetCollision(true)

            Fluent:Notify({
                Title = "GOJO 0.2",
                Content = "",
                Duration = 0
            })
        end
    end)

    local LP = Player

    local function AtualizarChar()

        local char =
            LP.Character
            or LP.CharacterAdded:Wait()

        return char,
            char:WaitForChild("HumanoidRootPart", 5)
    end

    local function ObterAlvos()

        local alvos = {}

        for _, p in ipairs(Players:GetPlayers()) do

            if p ~= LP
                and p.Character
                and p.Character:FindFirstChild("HumanoidRootPart") then

                local hum =
                    p.Character:FindFirstChildOfClass("Humanoid")

                if hum and hum.Health > 0 then

                    table.insert(
                        alvos,
                        p.Character.HumanoidRootPart
                    )
                end
            end
        end

        for _, obj in ipairs(Workspace:GetDescendants()) do

            if obj:IsA("Model")
                and obj ~= LP.Character then

                local rootPart =
                    obj:FindFirstChild("HumanoidRootPart")
                    or obj:FindFirstChild("Torso")
                    or obj:FindFirstChild("UpperTorso")

                local humanoid =
                    obj:FindFirstChildOfClass("Humanoid")

                if rootPart
                    and humanoid
                    and humanoid.Health > 0 then

                    if not Players:GetPlayerFromCharacter(obj) then

                        table.insert(alvos, rootPart)
                    end
                end
            end
        end

        return alvos
    end

    local function ExecutarBypass()

        local char, root = AtualizarChar()

        if not root then
            return false
        end

        local sucesso = false

        pcall(function()

            local listaAlvos = ObterAlvos()

            if #listaAlvos > 0 then

                local alvoPart =
                    listaAlvos[math.random(1, #listaAlvos)]

                if alvoPart and alvoPart.Parent then

                    local posInicial = root.Position

                    local posAlvo =
                        alvoPart.Position +
                        Vector3.new(0, 3, 0)

                    root.CFrame = CFrame.new(posAlvo)

                    RunService.Heartbeat:Wait()

                    if root and root.Parent then

                        local distanciaDoAlvo =
                            (root.Position - alvoPart.Position).Magnitude

                        local distanciaDaOrigem =
                            (root.Position - posInicial).Magnitude

                        if distanciaDoAlvo < 15
                            and distanciaDaOrigem > 5 then

                            sucesso = true
                        end
                    end
                end
            end
        end)

        return sucesso
    end

    local bypassAtivo = false

    Tabs.Gojo:AddToggle("BypassToggle", {
        Title = "Bypass",
        Default = false
    }):OnChanged(function(Value)

        bypassAtivo = Value

        if bypassAtivo then

            task.spawn(function()

                local tentativas = 0

                while bypassAtivo do

                    tentativas += 1

                    local sucesso = ExecutarBypass()

                    if not bypassAtivo then
                        break
                    end

                    if sucesso then

                        Fluent:Notify({
                            Title = "Bypass",
                            Content = "",
                            Duration = 0
                        })

                        bypassAtivo = false
                        break

                    else

                        if tentativas >= 5 then

                            Fluent:Notify({
                                Title = "❌ Bypass Falhou / Failed",
                                Content = "Se jogue no void / Jump into the void",
                                Duration = 4
                            })

                            bypassAtivo = false
                            break
                        end

                        task.wait(0.2)
                    end
                end
            end)
        end
    end)

    Fluent:Notify({
        Title = "Sistema",
        Content = "Carregado com sucesso!",
        Duration = 3
    })
end

-- ============================================================
-- VERIFICAÇÃO FINAL
-- ============================================================

Verify.MouseButton1Click:Connect(function()

    local key = KeyBox.Text:gsub("%s+", "")

    if key == "" then

        setStatus(
            "Digite uma key primeiro!",
            Color3.fromRGB(248, 81, 73)
        )

        return
    end

    Verify.Text = "Verificando..."
    Verify.Interactable = false

    setStatus(
        "Verificando...",
        Color3.fromRGB(88, 166, 255)
    )

    task.spawn(function()

        local valid, provider = verifyKey(key)

        if valid then

            getgenv().SCRIPT_KEY = key
            getgenv().KEY_PROVIDER = provider

            setStatus(
                "Key válida!",
                Color3.fromRGB(47, 183, 117)
            )

            task.wait(1)

            ScreenGui:Destroy()

            pcall(function()
                StartBlackFlash()
            end)

        else

            setStatus(
                "Key inválida ou expirada!",
                Color3.fromRGB(248, 81, 73)
            )

            Verify.Text = "Verificar Key"
            Verify.Interactable = true
        end
    end)
end)
