local Rayfield = loadstring(game:HttpGet('https://sirius.menu/rayfield'))()

local KeyWindow = Rayfield:CreateWindow({
   Name = "Get Key System",
   Theme = "Default",
   ToggleUIKeybind = "K",
   KeySystem = false,
})

local KeyTab = KeyWindow:CreateTab("Key", 4483362458)

-- Input pra digitar a key
local KeyInput = KeyTab:CreateInput({
   Name = "Digite a Key",
   PlaceholderText = "Insira aqui...",
   RemoveTextAfterFocusLost = false,
   Callback = function(Text) end,
})

-- Botão Get Key (copia o link novo)
KeyTab:CreateButton({
   Name = "Get Key (Copiar Link)",
   Callback = function()
      setclipboard("https://preview--keenly-witty-carpenter.instance.app/?instanceInstallBanner=false")
      Rayfield:Notify({
         Title = "Link Copiado!",
         Content = "Abra no navegador → veja a key aleatória exibida na página → cole aqui.",
         Duration = 8,
      })
   end,
})

-- Botão Confirmar Key (com espaço pra colar a API)
KeyTab:CreateButton({
   Name = "Confirmar Key",
   Callback = function()
      local digitada = KeyInput.CurrentValue or ""
      
      -- =============================================
      -- COLOQUE O URL DA SUA API AQUI ↓↓↓
      local API_URL = "https://preview--keenly-witty-carpenter.instance.app/?instanceInstallBanner=false"  -- Exemplo: "https://seu-projeto-default-rtdb.firebaseio.com/current_key.json"
                          -- Deixe vazio "" se quiser usar verificação simples sem API
      -- =============================================
      
      if API_URL ~= "" then
         -- Modo API (checa no servidor)
         local HttpService = game:GetService("HttpService")
         local success, response = pcall(function()
            return HttpService:GetAsync(API_URL)
         end)
         
         if success then
            local data = HttpService:JSONDecode(response)
            if data and data.key then
               if digitada == data.key then
                  local now = os.time() * 1000
                  if data.expires_at and now < data.expires_at then
                     Rayfield:Notify({Title = "Acesso Liberado!", Content = "Key válida via API!", Duration = 3})
                     goto load_hub
                  else
                     Rayfield:Notify({Title = "Key Expirada", Content = "A key expirou.", Duration = 5})
                     return
                  end
               end
            end
         else
            Rayfield:Notify({Title = "Erro na API", Content = "Não conseguiu conectar. Tente depois.", Duration = 5})
            return
         end
         
         Rayfield:Notify({Title = "Key Inválida", Content = "Não bate com a API.", Duration = 4})
         return
      end
      
      -- Modo simples (sem API) - fallback
      if digitada == "free_delta" then
         Rayfield:Notify({Title = "Acesso Liberado!", Content = "Carregando hub...", Duration = 3})
         
         ::load_hub::
         task.wait(0.6)
         pcall(function() Rayfield:Destroy() end)
         if KeyWindow then KeyWindow:Hide() end
         
         pcall(function()
            loadstring(game:HttpGet("https://pastefy.app/rt7ZX9V4/raw"))()
         end)
         
         Rayfield:Notify({Title = "Hub Carregado!", Content = "Aproveite as funções OP!", Duration = 5})
      else
         Rayfield:Notify({Title = "Key Inválida", Content = "Tente novamente.", Duration = 4})
      end
   end,
})

-- Instruções
KeyTab:CreateParagraph({
   Title = "Instruções",
   Content = "1. Clique em 'Get Key' pra copiar o link\n2. Abra no navegador e pegue a key que aparece\n3. Cole aqui e clica em Confirmar Key"
})
