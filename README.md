-- Carregar Rayfield
local Rayfield = loadstring(game:HttpGet("https://sirius.menu/rayfield"))()

-- Criar Janela Principal
local Window = Rayfield:CreateWindow({
    Name = "Meu Script Rayfield",
    LoadingTitle = "Carregando...",
    LoadingSubtitle = "By SeuNome",
    ConfigurationSaving = {
        Enabled = true,
        FolderName = "MeuScriptRayfield",
        FileName = "Config"
    },
    Discord = {
        Enabled = false,
        Invite = "",
        RememberJoins = true
    },
    KeySystem = false,
})

-- 1. Aba Info
local InfoTab = Window:CreateTab("Info", 4483362458)
InfoTab:CreateParagraph({
    Title = "Chorou Pro Luar.Exe e Pro Miranha",
    Content = "Será???"
})

-- 2. Aba PVP
local PVP_T = Window:CreateTab("PVP", 4483362458)

-- No-Clip funcional
local noclipConnection
local noclipEnabled = false

PVP_T:CreateToggle({
    Name = "No-Clip",
    CurrentValue = false,
    Flag = "NoClipToggle",
    Callback = function(state)
        noclipEnabled = state
        if noclipEnabled then
            noclipConnection = game:GetService("RunService").Stepped:Connect(function()
                local char = game.Players.LocalPlayer.Character
                if char and char:FindFirstChildOfClass("Humanoid") then
                    char:FindFirstChildOfClass("Humanoid"):ChangeState(11)
                    for _, part in pairs(char:GetDescendants()) do
                        if part:IsA("BasePart") and part.CanCollide == true then
                            part.CanCollide = false
                        end
                    end
                end
            end)
        else
            if noclipConnection then noclipConnection:Disconnect() end
            local char = game.Players.LocalPlayer.Character
            if char then
                for _, part in pairs(char:GetDescendants()) do
                    if part:IsA("BasePart") then
                        part.CanCollide = true
                    end
                end
            end
        end
    end,
})

-- Speed funcional
local originalWalkSpeed = 16
local speedEnabled = false

PVP_T:CreateToggle({
    Name = "Speed (Corrida Rápida)",
    CurrentValue = false,
    Flag = "SpeedToggle",
    Callback = function(state)
        speedEnabled = state
        local humanoid = game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
        if humanoid then
            if speedEnabled then
                originalWalkSpeed = humanoid.WalkSpeed
                humanoid.WalkSpeed = 50
            else
                humanoid.WalkSpeed = originalWalkSpeed
            end
        end
    end,
})

-- 3. Aba Aimbot
local AimbotTab = Window:CreateTab("Aimbot", 4483362458)

AimbotTab:CreateButton({
    Name = "Ativar Aimbot",
    Callback = function()
        loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Aimbot-fov-mobile-7607"))()
    end,
})

-- 4. Aba Visual
local VisualTab = Window:CreateTab("Visual", 4483362458)

-- Infinite Yield
local infiniteYieldEnabled = false

VisualTab:CreateToggle({
    Name = "Infinite Yield",
    CurrentValue = false,
    Flag = "InfiniteYieldToggle",
    Callback = function(state)
        infiniteYieldEnabled = state
        if infiniteYieldEnabled then
            loadstring(game:HttpGet("https://raw.githubusercontent.com/EdgeIY/infiniteyield/master/source"))()
        end
    end,
})

-- God Mode
local godModeEnabled = false

VisualTab:CreateToggle({
    Name = "God Mode",
    CurrentValue = false,
    Flag = "GodModeToggle",
    Callback = function(state)
        godModeEnabled = state
        local humanoid = game.Players.LocalPlayer.Character and game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
        if humanoid then
            humanoid.MaxHealth = 99999
            humanoid.Health = 99999
            humanoid.HealthChanged:Connect(function()
                if godModeEnabled then
                    humanoid.Health = 99999
                end
            end)
        end
    end,
})

-- Anti Staff
local antiStaffEnabled = false

VisualTab:CreateToggle({
    Name = "Anti Staff",
    CurrentValue = false,
    Flag = "AntiStaffToggle",
    Callback = function(state)
        antiStaffEnabled = state
        -- Adicionar lógica para anti staff
    end,
})

-- Revistar (PC e Mobile)
local revistarEnabled = false

VisualTab:CreateToggle({
    Name = "Revistar (Loop no Chat)",
    CurrentValue = false,
    Flag = "RevistarToggle",
    Callback = function(state)
        revistarEnabled = state
        if revistarEnabled then
            while revistarEnabled do
                game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest:FireServer("/revistar morto", "All")
                wait(1)  -- Aguarda 1 segundo entre cada comando
            end
        end
    end,
})

-- 5. Aba Trolls
local TrollsTab = Window:CreateTab("Trolls", 4483362458)

TrollsTab:CreateButton({
    Name = "Crash Server",
    Callback = function()
        -- Não é recomendado fazer scripts para crashar o servidor
    end
})

-- Fake Lag (Visual)
local fakeLagEnabled = false
local fakeLagConnection

TrollsTab:CreateToggle({
    Name = "Fake Lag",
    CurrentValue = false,
    Flag = "FakeLagToggle",
    Callback = function(state)
        fakeLagEnabled = state
        if fakeLagEnabled then
            fakeLagConnection = game:GetService("RunService").Heartbeat:Connect(function()
                -- Simula a perda de frames (lag) alterando a renderização do jogo
                game:GetService("RunService").RenderStepped:Wait()
            end)
        else
            if fakeLagConnection then fakeLagConnection:Disconnect() end
        end
    end,
})

-- 6. Aba Players
local PlayersTab = Window:CreateTab("Players", 4483362458)

PlayersTab:CreateButton({
    Name = "Bring All",
    Callback = function()
        for _, player in pairs(game.Players:GetPlayers()) do
            if player.Character then
                player.Character:MoveTo(game.Players.LocalPlayer.Character.HumanoidRootPart.Position)
            end
        end
    end
})

-- 7. Aba Farms
local FarmsTab = Window:CreateTab("Farms", 4483362458)

-- Exemplo de AutoFarm de Lixo da Cidade
local autoFarmEnabled = false

FarmsTab:CreateToggle({
    Name = "AutoFarm Lixo da Cidade",
    CurrentValue = false,
    Flag = "AutoFarmLixoToggle",
    Callback = function(state)
        autoFarmEnabled = state
        if autoFarmEnabled then
            while autoFarmEnabled do
                -- Lógica do AutoFarm
                print("Farmando Lixo da Cidade")
                wait(1)
            end
        end
    end,
})
