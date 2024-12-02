-- Anti-Cheat Script para impedir execução de scripts maliciosos no Roblox

local Players = game:GetService("Players")
local RunService = game:GetService("RunService")

-- Função para detectar execução de LocalScripts ou comportamentos suspeitos
local function detectExploit(player)
    local character = player.Character
    if not character then return end
    
    -- Verificar se o jogador está tentando usar LocalScripts no seu personagem
    for _, object in pairs(character:GetChildren()) do
        if object:IsA("LocalScript") then
            warn(player.Name .. " tentou executar um LocalScript!")
            player:Kick("Tentativa de execução de script detectada. Você foi expulso do servidor.")
            return true
        end
    end
    
    -- Verificar se o jogador tem Scripts maliciosos dentro de PlayerScripts ou outras áreas críticas
    local playerScripts = player:FindFirstChild("PlayerScripts")
    if playerScripts then
        for _, object in pairs(playerScripts:GetChildren()) do
            if object:IsA("LocalScript") then
                warn(player.Name .. " tentou usar LocalScript no PlayerScripts.")
                player:Kick("Tentativa de execução de script detectada. Você foi expulso do servidor.")
                return true
            end
        end
    end

    return false
end

-- Função para monitorar o comportamento de novos jogadores
Players.PlayerAdded:Connect(function(player)
    player.CharacterAdded:Connect(function(character)
        -- Detecta se o jogador está tentando rodar scripts maliciosos quando ele entra
        if detectExploit(player) then
            return
        end
    end)
end)

-- Verificar os jogadores que já estão no jogo
for _, player in pairs(Players:GetPlayers()) do
    if player.Character then
        detectExploit(player)
    end
end)

-- Função de segurança para detectar ações suspeitas durante o jogo
RunService.Stepped:Connect(function(_, _, deltaTime)
    -- Monitoramento contínuo para ações em tempo real
    for _, player in pairs(Players:GetPlayers()) do
        local character = player.Character
        if character then
            -- Aqui você pode adicionar verificações extras, como comportamento suspeito em partes específicas do personagem
        end
    end
end)
