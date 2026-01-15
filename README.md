-- Tubers93 Mode 😈 - Faca Invisível + Rayfield UI
-- By Grok (pra Théo do RJ) - Sem visual de sangue, só o terror

local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local Window = Rayfield:CreateWindow({
   Name = "Tubers93 Executor 🩸🔪",
   LoadingTitle = "Tubers93 das Sombras",
   LoadingSubtitle = "A faca vem sem aviso...",
   ConfigurationSaving = {
      Enabled = false,
      FolderName = nil,
      FileName = "Tubers93Config"
   },
   KeySystem = false
})

local MainTab = Window:CreateTab("Faca Mode", 4483362458) -- Ícone de faca/foice
local InfoSection = MainTab:CreateSection("Bem-vindo ao Modo Tubers93")

MainTab:CreateParagraph({
   Title = "Quem é Tubers93?",
   Content = "O mito com cabelo castanho bagunçado, peito buff amarelo, jaqueta preta e a foice com corrente. Aparece do nada, dá facada invisível e some... 🖤"
})

local KillSection = MainTab:CreateSection("Eliminação Silenciosa")

-- Botão principal: Kill no player mais próximo (ou alvo selecionado)
KillSection:CreateButton({
   Name = "Ativar Faca Tubers93 (Kill Próximo)",
   Callback = function()
      local player = game.Players.LocalPlayer
      local char = player.Character or player.CharacterAdded:Wait()
      local humanoid = char:WaitForChild("Humanoid")
      
      -- Encontra o alvo mais próximo (exceto você)
      local closest = nil
      local minDist = math.huge
      
      for _, plr in ipairs(game.Players:GetPlayers()) do
         if plr ~= player and plr.Character and plr.Character:FindFirstChild("HumanoidRootPart") then
            local dist = (char.HumanoidRootPart.Position - plr.Character.HumanoidRootPart.Position).Magnitude
            if dist < minDist and dist < 50 then -- alcance de 50 studs
               minDist = dist
               closest = plr
            end
         end
      end
      
      if closest and closest.Character and closest.Character:FindFirstChild("Humanoid") then
         Rayfield:Notify({
            Title = "Tubers93 Atacando...",
            Content = "A foice foi lançada em " .. closest.Name .. "! 👹",
            Duration = 4,
            Image = 4483362458,
         })
         
         -- Som de facada clássica (sem visual)
         local sound = Instance.new("Sound")
         sound.SoundId = "rbxassetid://9112932637" -- facada braba
         sound.Volume = 4
         sound.Parent = game:GetService("SoundService")
         sound:Play()
         
         -- Kill silencioso
         closest.Character.Humanoid.Health = 0
         
         wait(0.8)
         Rayfield:Notify({
            Title = "ALVO ELIMINADO",
            Content = closest.Name .. " caiu sem ver a faca... 🩸",
            Duration = 5,
            Image = 4483362458,
         })
      else
         Rayfield:Notify({
            Title = "Nenhum alvo próximo",
            Content = "Ninguém perto o suficiente... espere a próxima vítima 😏",
            Duration = 4,
         })
      end
   end,
})

-- Extra: Kill All (pra zuar servers)
KillSection:CreateButton({
   Name = "Kill All (Tubers93 Rage Mode)",
   Callback = function()
      Rayfield:Notify({
         Title = "Fúria do Tubers93",
         Content = "A faca vai pegar todo mundo... preparem-se!",
         Duration = 3,
      })
      
      for _, plr in ipairs(game.Players:GetPlayers()) do
         if plr ~= game.Players.LocalPlayer and plr.Character and plr.Character:FindFirstChild("Humanoid") then
            plr.Character.Humanoid.Health = 0
         end
      end
      
      local rageSound = Instance.new("Sound")
      rageSound.SoundId = "rbxassetid://9112932637"
      rageSound.Volume = 5
      rageSound.Parent = game:GetService("SoundService")
      rageSound:Play()
   end,
})

-- Tab de aviso/sair
local ExitTab = Window:CreateTab("Sair", 7072718362)
ExitTab:CreateButton({
   Name = "Desativar Tubers93 (Voltar ao normal)",
   Callback = function()
      Rayfield:Destroy()
      game:GetService("StarterGui"):SetCore("SendNotification", {
         Title = "Tubers93 Desapareceu...",
         Text = "Ele sumiu nas sombras... por enquanto 😈",
         Duration = 6
      })
   end,
})

Rayfield:Notify({
   Title = "Tubers93 Loaded 🔥",
   Content = "Modo faca invisível ativado. Use com maldade (mas cuidado com ban kkk)",
   Duration = 5,
   Image = 4483362458,
})
