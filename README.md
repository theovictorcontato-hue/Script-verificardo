-- Tubers93 Mode 😈 - Versão Corrigida 2026
print("Tubers93 carregando... Aguarde a faca das sombras 🩸🔪")

local success, Rayfield = pcall(function()
    return loadstring(game:HttpGet('https://raw.githubusercontent.com/shlexware/Rayfield/main/source'))()
end)

if not success or not Rayfield then
    print("ERRO: Rayfield falhou! Tenta outro executor ou link alternativo.")
    return
end

local Window = Rayfield:CreateWindow({
   Name = "Tubers93 Executor 🩸🔪",
   LoadingTitle = "Tubers93 das Sombras Chegou",
   LoadingSubtitle = "Prepare a vítima...",
   ConfigurationSaving = {Enabled = false},
   KeySystem = false
})

local MainTab = Window:CreateTab("Faca Mode", 4483362458) -- Ícone de faca/foice

MainTab:CreateSection("Bem-vindo ao Modo Tubers93")

MainTab:CreateParagraph({
   Title = "Modo Ativado!",
   Content = "Você agora é o Tubers93: cabelo bagunçado, peito buff, foice com corrente. Dá facada invisível com só som + notificação! 😈"
})

local KillSection = MainTab:CreateSection("Eliminação Silenciosa")

KillSection:CreateButton({
   Name = "Faca Tubers93 - Kill no Mais Próximo",
   Callback = function()
      -- (código do kill próximo igual antes, sem mudanças)
      local player = game.Players.LocalPlayer
      local char = player.Character
      if not char or not char:FindFirstChild("HumanoidRootPart") then return end
      
      local closest, minDist = nil, math.huge
      for _, plr in game.Players:GetPlayers() do
         if plr ~= player and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
            local dist = (char.HumanoidRootPart.Position - plr.Character.HumanoidRootPart.Position).Magnitude
            if dist < minDist and dist < 60 then
               minDist = dist
               closest = plr
            end
         end
      end
      
      if closest then
         Rayfield:Notify({Title = "Tubers93 Atacou!", Content = "Foice em "..closest.Name.."! 👹", Duration = 4})
         local sound = Instance.new("Sound", game.SoundService)
         sound.SoundId = "rbxassetid://9112932637"
         sound.Volume = 4
         sound:Play()
         closest.Character.Humanoid.Health = 0
         wait(1)
         Rayfield:Notify({Title = "ELIMINADO", Content = closest.Name.." caiu sem ver nada... 🩸", Duration = 5})
      else
         Rayfield:Notify({Title = "Sem Vítima", Content = "Ninguém perto... espere 😏", Duration = 4})
      end
   end,
})

KillSection:CreateButton({
   Name = "Kill All - Rage Mode Tubers93",
   Callback = function()
      Rayfield:Notify({Title = "Fúria Ativada", Content = "Todo mundo leva facada!", Duration = 3})
      for _, plr in game.Players:GetPlayers() do
         if plr ~= game.Players.LocalPlayer and plr.Character and plr.Character:FindFirstChild("Humanoid") then
            plr.Character.Humanoid.Health = 0
         end
      end
      local sound = Instance.new("Sound", game.SoundService)
      sound.SoundId = "rbxassetid://9112932637"
      sound.Volume = 5
      sound:Play()
   end,
})

local ExitTab = Window:CreateTab("Sair", 7072718362)
ExitTab:CreateButton({
   Name = "Desativar Tubers93",
   Callback = function()
      Rayfield:Destroy()
      game.StarterGui:SetCore("SendNotification",{Title="Tubers93 Sumiu",Text="Nas sombras novamente... 😈",Duration=6})
   end,
})

Rayfield:Notify({
   Title = "Tubers93 Loaded 🔥",
   Content = "UI aberta! Clique em 'Faca Mode' > 'Faca Tubers93 - Kill no Mais Próximo' pra virar o mito.",
   Duration = 6
})

print("Tubers93 pronto! UI deve aparecer agora.")
