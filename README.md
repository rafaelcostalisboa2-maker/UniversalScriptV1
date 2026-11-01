-- 1. SERVIÇOS
local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local HttpService = game:GetService("HttpService")
local LocalPlayer = Players.LocalPlayer

-- LOGO SCRIPTLAND: usado somente no botão flutuante.
-- Imagem externa precisa ser baixada e carregada como asset local pelo executor.
local LogoURL = "https://i.ibb.co/Yx5FDGs/Scripts-Land.png"
local LogoImage = nil
pcall(function()
    local assetLoader = getcustomasset or getsynasset
    if type(assetLoader) == "function" and type(writefile) == "function" then
        local imageData = game:HttpGet(LogoURL)
        assert(type(imageData) == "string" and #imageData > 100, "Não foi possível baixar a logo")
        writefile("ScriptLandLogo.png", imageData)
        LogoImage = assetLoader("ScriptLandLogo.png")
    end
end)

-- 2. Panda Auth PUSL-V4
-- A biblioteca é carregada uma vez e usada pelo botão VERIFICAR KEY.
local PUSL = nil
local pandaLoadOk, pandaLoadResult = pcall(function()
    return loadstring(game:HttpGet("https://secure.pandauth.com/pv4/lib"))()
end)
if pandaLoadOk and type(pandaLoadResult) == "table" and type(pandaLoadResult.configure) == "function" then
    PUSL = pandaLoadResult
    local configureOk = pcall(function()
        PUSL.configure({ serviceId = "scriptland" })
    end)
    if not configureOk then
        warn("[Panda] Não foi possível configurar o Panda Auth V4.")
        PUSL = nil
    end
else
    warn("[Panda] Biblioteca PUSL-V4 não carregou. A verificação de key não estará disponível.")
end

-- 3. FUNÇÃO DO SEU HUB ORIGINAL
local function IniciarHubOriginal()
    local TweenService = game:GetService("TweenService")
local Players = game:GetService("Players")
local HttpService = game:GetService("HttpService")
local LocalPlayer = Players.LocalPlayer

-- [SISTEMA DE ARQUIVOS PARA FAVORITOS]
local FavFile = "SFZ_Favorites.json"

-- Inicializa o arquivo de favoritos se não existir
if not isfile(FavFile) then
    writefile(FavFile, HttpService:JSONEncode({}))
end

local function GetFavorites()
    local success, content = pcall(function() return readfile(FavFile) end)
    if success then
        return HttpService:JSONDecode(content)
    end
    return {}
end

local function ToggleFavorite(scriptName, gameName)
    local favs = GetFavorites()
    if not favs[gameName] then favs[gameName] = {} end
    
    local index = table.find(favs[gameName], scriptName)
    if index then
        table.remove(favs[gameName], index)
        if #favs[gameName] == 0 then favs[gameName] = nil end
        writefile(FavFile, HttpService:JSONEncode(favs))
        return false -- Removido
    else
        table.insert(favs[gameName], scriptName)
        writefile(FavFile, HttpService:JSONEncode(favs))
        return true -- Adicionado
    end
end

-- [[ DATABASE ATUALIZADA - V3.5 ]]
local Database = {
    [1] = {
        Name = "Scripts Aleatórios", Icon = "⚙️",
        Key = {}, 
        NoKey = {
            ["Aim Bot Jogos de Tiro"] = function() loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Aimbot-Mobile-34677"))() end,
            ["Emotes"] = function() loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-7yd7-I-Emote-Script-48024"))() end,
            ["Aim Bot + ESP"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/agresiv111/script/refs/heads/main/main.lua"))() end,
            ["Shift Lock"] = function() loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Shift-Lock-by-Jorge03IsGamer-54009"))() end,
            ["Fly"] = function() loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Fly-gui-54742"))() end,
            ["Hitbox Expander"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/example-prog/Hitbox-Expander/refs/heads/main/RScripter"))() end,
        }
    },
    [2] = {
        Name = "Blox Fruits", Icon = "🍎",
        Key = {
            ["Kncrypt"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/3345-c-a-t-s-u-s/Kncrypt/refs/heads/main/sources/BloxFruit.lua"))() end,
            ["OMG Hub"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/Omgshit/Scripts/main/MainLoader.lua"))() end,
            ["Arceney"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/Yumiara/Python/refs/heads/main/BloxFruit-XYZ.lua"))() end,
            ["Hoho Hub BF"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/acsu123/HOHO_H/main/Loading_UI"))() end,
            ["Solix Hub"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/debunked69/Solixreworkkeysystem/refs/heads/main/solix%20new%20keyui.lua"))() end,
            ["Thunder Z"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/ThunderZ-05/HUB/main/TestKey"))() end,
            ["Auto Hop Fruit"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/Dev-BlueX/BlueX-Hub/refs/heads/main/Main.lua"))() end,
        },
        NoKey = {
            ["Auto Bounty (Hermanos Hub)"] = function() local script_mode = "PVP" -- PVP, FARM
loadstring(game:HttpGet("https://raw.githubusercontent.com/hermanos-dev/hermanos-hub/refs/heads/main/Loader.lua"))() end,
  
            ["Speed Hub BF"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/AhmadV99/Speed-Hub-X/main/Speed%20Hub%20X.lua"))() end,
            ["Night Hub Farm"] = function()loadstring(game:HttpGet("https://raw.githubusercontent.com/NSHWShadow/MidNightHub/refs/heads/main/Loader/TesterScript.lua"))() end,
            ["Quantum Onyx"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/flazhy/QuantumOnyx/refs/heads/main/QuantumOnyx.lua"))() end,
            ["Redz Hub"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/luraobermeyer-jpg/redzhub/refs/heads/main/redzhub.lua.txt"))() end,
        }
    },
    [3] = {
        Name = "King Legacy", Icon = "👑",
        Key = {
            ["OMG Hub"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/Omgshit/Scripts/refs/heads/main/FarmingFlags"))() end,
            ["Hyper Hub"] = function() repeat wait() until game:IsLoaded() loadstring(game:HttpGet("https://raw.githubusercontent.com/DookDekDEE/Hyper/main/script.lua"))() end,
            ["Legends Handles Hub"] = function() loadstring(game:HttpGet(('https://pastefy.app/3fQ9psgV/raw'),true))() end,
            ["Hoho Hub KL"] = function() loadstring(game:HttpGet('https://raw.githubusercontent.com/acsu123/HOHO_H/main/Loading_UI'))() end,
            ["Faziam Hub"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/ZaRdoOx/Fazium-files/main/Loader"))() end,
            ["Auto Fish KL"] = function() loadstring(game:HttpGet("https://api.junkie-development.de/api/v1/luascripts/public/042ab4ec0ef175451b3fd805ee7205ff95b1b5ca7541d4be9678087b58169ab3/download"))() end,
            ["Rob Hub"] = function() loadstring(game:HttpGet('https://raw.githubusercontent.com/artas01/robscript/refs/heads/main/loader.lua'))() end,
        },
        NoKey = {
            ["Tsuo Hub"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/Tsuo7/TsuoHub/main/king%20legacy"))() end,
            ["BTProject"] = function() loadstring(game:HttpGet('https://raw.githubusercontent.com/OxyCoder32/prueba-script/refs/heads/main/BTProject'))() end,
        }
    },
    [4] = {
        Name = "Dungeon Heroes", Icon = "🛡️",
        Key = {},
        NoKey = {
            ["Valor Hub"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/eselfins31/Valor-Hub/main/Dungeon%20Heroes/Unified_protected.lua", true))() end,
        }
    },
    [5] = {
        Name = "Tsunami vs Brainrots", Icon = "🌊",
        Key = {
            ["Rift Hub"] = function() loadstring(game:HttpGet("https://rifton.top/loader.lua"))() end,
        },
        NoKey = {
            ["TvsB Hub"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/gumanba/Scripts/refs/heads/main/EscapeTsunamiForBrainrots", true))() end,
        }
    },
    [6] = {
        Name = "Steal An Egg", Icon = "🥚",
        Key = {["Ajjans Hub"] = function() loadstring(game:HttpGet("https://api.luarmor.net/files/v4/loaders/359e97f8618e9008afe5f496184ebb7c.lua"))() end,["OMG Hub"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/Omgshit/Scripts/main/MainLoader.lua"))() end, },
        NoKey = {
            ["Chilli Hub V1"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/tienkhanh1/Chilli-Hub-Script/refs/heads/main/StealAnEgg"))() end,
        ["Chilli Hub V5"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/ronnei/hihi/refs/heads/main/chillihubv5.lua"))() end,                         ["Miranda"] = function() loadstring(game:HttpGet("https://api.luarmor.net/files/v4/loaders/7891557d7950ed56a7d1d8f57b66ad4d.lua"))() end,                                   ["Miranda AFK"] = function() loadstring(game:HttpGet("https://api.luarmor.net/files/v4/loaders/6b07a458832f08b2314f706f14723212.lua"))()
 end, ["Lennon Hub"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/lennonxscripts/lennonhubv4/refs/heads/main/stealanegg"))() end,                 ["Lennon Hub AFK"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/lennonxscripts/lennonfarmv2/refs/heads/main/stealanegg"))()   end }
    },
    [7] = {
        Name = "Pet Simulator 99", Icon = "🐾",
        Key = { ["Zap Hub"] = function() loadstring(game:HttpGet('https://zaphub.xyz/Exec'))() end },
        NoKey = {}
    },
    [8] = {
        Name = "PETS GO", Icon = "🐶",
        Key = { ["Zap Hub"] = function() loadstring(game:HttpGet('https://zaphub.xyz/Exec'))() end },
        NoKey = {}
    },
    [9] = { 
        Name = "Steal a Brainrot", Icon = "👽",
        Key = {
            ["Overflow"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/OverflowBGSI/Overflow/refs/heads/main/loader.txt"))() end,
            ["Senju"] = function() loadstring(game:HttpGet("https://pastebin.com/raw/wk11PpEw"))() end,
            ["Trax Spawner"] = function() loadstring(game:HttpGet("https://gitlab.com/traxscriptss/traxscriptss/-/raw/main/visual2.lua"))() end,
            ["Luminum Hub"] = function() loadstring(game:HttpGet("http://luminon.top/loader.lua"))() end,   
        },
        NoKey = {
            ["Lurk Hack V4"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/egor2078f/lurkhackv4/refs/heads/main/main.lua", true))() end,
            ["Dofug"] = function() loadstring(game:HttpGet("https://gist.githubusercontent.com/UCT-hub/b8fcd843274469d860f91b041eb7f52f/raw/7d491ea8078224e31b8850192bd3f2da37acec8f/UCTHUBDOFUG"))() end,
            ["Ajjans Hub"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/onliengamerop/Steal-a-brainrot/refs/heads/main/Protected_3771863424757750.lua.txt"))() end,
            ["Liphyr"] = function() loadstring(game:HttpGet("https://pastefy.app/9fgffG4l/raw"))() end,
        }
    },
    [10] = {
        Name = "The Forge", Icon = "⛏️",
        Key = { 
            ["Nousigi Hub"] = function() loadstring(game:HttpGet("https://nousigi.com/loader.lua"))() end, 
            ["Zenith Hub"] = function() loadstring(game:HttpGet("https://zenithhub.cloud/panel/script"))() end,
            ["Lunor Hub"] = function() loadstring(game:HttpGet("https://lunor.dev/loader"))() end,
            ["Chyo Hub"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/kaisenlmao/loader/refs/heads/main/chiyo.lua"))() end,
            ["NS Hub Forge"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/OhhMyGehlee/sh/refs/heads/main/a"))() end,
            ["Solix Hub"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/meobeo8/a/a/a"))() end,
            ["AirFlow Hub"] = function() loadstring(game:HttpGet("https://airflowscript.com/loader"))() end,
            ["Voidw0rld"] = function() loadstring(game:HttpGet("https://api.luarmor.net/files/v3/loaders/280c3c5ae0ed18010fea0d86c424fdb5.lua"))() end,
        },
        NoKey = { 
            ["Haze Hub"] = function() loadstring(game:HttpGet("https://haze.wtf/api/script"))() end, 
            ["Polluted Hub"] = function() loadstring(game:HttpGet("https://api.luarmor.net/files/v3/loaders/ecfcccea43f60fa4c46009f854c06a52.lua"))() end,
            ["Shaizy Hub"] = function() loadstring(game:HttpGet("https://api.luarmor.net/files/v3/loaders/d29f750a5d2c74070b792230ccde0f69.lua"))() end,
        }
    },
    [11] = {
        Name = "Brookhaven", Icon = "🏠",
        Key = { 
            ["Cartola Hub BH"] = function() loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Cartola-hub-brookhaven-57407"))() end,
            ["Demon Hub v2"] = function() loadstring(game:HttpGet("https://pastefy.app/vn8cfnLw/raw"))() end,
        },
        NoKey = { 
            ["Drip client"] = function() loadstring(game:HttpGet("https://rawscripts.net/raw/Brookhaven-RP-Drip-Client-51784"))() end, 
            ["CO0LKID Hub"] = function() loadstring(game:HttpGet("https://rawscripts.net/raw/Brookhaven-RP-C00LKIDD-HUB-By-lkzin-69221"))() end,
            ["Nevliz Hub"] = function() loadstring(game:HttpGet("https://rawscripts.net/raw/Brookhaven-RP-4-scripts-Bypass-FE-68746"))() end,
            ["Coquette Hub BH"] = function() loadstring(game:HttpGet("https://ghostbin.axel.org/paste/8z4hy/raw"))() end,
        }
    },
    [12] = {
        Name = "Volleyball Legends", Icon = "🏐",
        Key = {
            ["Napoleon Hub ⚠️:98%"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/raydjs/napoleonHub/refs/heads/main/src.lua"))() end,
            ["Rinns Hub VL ⚠️:98%"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/SkibidiCen/MainMenu/main/Code"))() end,
            ["Axolotl ⚠️:98%"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/notjohnnylol/boiazuresotuff/refs/heads/main/loader"))() end,
            ["Omg Hub ⚠️:98%"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/Omgshit/Scripts/main/MainLoader.lua"))() end,
        },
        NoKey = {
            ["Sigma Hub ⚠️:98%"] = function() loadstring(game:HttpGet('https://raw.githubusercontent.com/Xm2iufas09ijmF/sigma-hub/refs/heads/main/temp.lua'))() end,
            ["Hitbox Expander VL ⚠️:98%"] = function() loadstring(game:HttpGet("https://rawscripts.net/raw/UPD-Volleyball-Legends-Hitbox-expander-NO-KEY-63949"))() end,
        }
    },
    [13] = {
        Name = "99 Noites", Icon = "🌲",
        Key = {
            ["H4x"] = function() loadstring(game:HttpGet("https://H4xScripts.xyz/loader"))() end,
        },
        NoKey = {
            ["Void ware"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/VapeVoidware/VW-Add/main/nightsintheforest.lua",true))() end,
            ["Foxname"] = function() loadstring(game:HttpGet("https://rawscripts.net/raw/99-Nights-in-the-Forest-Foxname-Hub-57131"))() end,
        }
    },
    [14] = {
        Name = "Ficsh", Icon = "🎣",
        Key = { ["Space Hub"] = function() loadstring(game:HttpGet('https://raw.githubusercontent.com/Space-RB/Script/refs/heads/main/loader.lua'))() end },
        NoKey = { 
            ["Eclipse"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/yolobradda/eclipsefisch/refs/heads/main/eclipsefisch"))() end, 
            ["Disch Hub"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/hakariqScripts/disch2/refs/heads/main/disch%20script"))() end,
            ["AeroWare"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/cayden305/Scripts/refs/heads/main/FischObfuscated.lua"))() end,
        }
    },
    [15] = {
        Name = "Forsaken", Icon = "🎭",
        Key = { 
            ["Moon Hub"] = function() loadstring(game:HttpGet('https://raw.githubusercontent.com/m00ndiety/Moondiety/refs/heads/main/Loader'))() end,
            ["NS Hub"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/OhhMyGehlee/sak/refs/heads/main/for"))() end,
            ["Coquette Hub FK"] = function() loadstring(game:HttpGet("https://ghostbin.axel.org/paste/5sppg/raw"))() end,
        },
        NoKey = { ["SNT Hub"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/Snowt69/SNT-HUB/refs/heads/main/Forsaken"))() end }
    },
    [16] = {
        Name = "Murder Mystery 2", Icon = "🔪",
        Key = { ["Capybara Hub"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/BaconScrr/Murder-Mystery-2/refs/heads/main/Capybara%20Hub"))() end },
        NoKey = { 
            ["Yarhm"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/Joystickplays/psychic-octo-invention/main/source/yarhm/1.20/yarhm.lua"))() end,
            ["MM2 Hub"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/wave-code-top/xhub/refs/heads/main/xhub.lua", true))() end 
        }
    },
    [17] = {
        Name = "Blade Ball", Icon = "🗡️",
        Key = {},
        NoKey = { 
            ["NodeX Hub"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/NodeX-Enc/NodeX/refs/heads/main/Main.lua"))() end,
            ["ArgonX Hub"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/AgentX771/ArgonHubX/main/Loader.lua"))() end,
            ["Argon Hub"] = function() loadstring(game:HttpGet("https://rawscripts.net/raw/Universal-Script-Argon-Hub-X-KEYLESS-57532"))() end,
        }
    },
    [18] = {
        Name = "Blue Lock", Icon = "⚽",
        Key = { 
            ["Rinns Hub BL"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/SkibidiCen/MainMenu/main/Code"))() end,
        },
        NoKey = {}
    },
    [19] = {
        Name = "Slap Battles", Icon = "🥊",
        Key = {
            ["Ronix Hub"] = function() loadstring(game:HttpGet("https://rawscripts.net/raw/Slap-Battles-Best-Script-OP-GUI-Slap-Aura-85516"))() end,
            ["SB Hub (Win)"] = function() loadstring(game:HttpGet("https://rawscripts.net/raw/UPDATE-Slap-Battles-INSTANT-WIN-l-Kraken-Abyss-Auto-Win-l-God-Mod-l-Full-86843"))() end,
            ["Nagi Hub"] = function() loadstring(game:HttpGet("https://rawscripts.net/raw/UPDATE-Slap-Battles-Slap-Battle-50314"))() end,
        },
        NoKey = {
            ["Project Astro SB"] = function() loadstring(game:HttpGet("https://rawscripts.net/raw/HALLOWEEN-Slap-Battles-Project-Astro-Reborn-Slap-Battle-60628"))() end,
            ["Sisyphus Prime"] = function() loadstring(game:HttpGet("https://rawscripts.net/raw/UPDATE-Slap-Battles-Slap-Battle-55319"))() end,
            ["SB Hub v2_2"] = function() loadstring(game:HttpGet("https://rawscripts.net/raw/UPDATE-Slap-Battles-Slap-battles-script-NO-KEY-51094"))() end,
            ["SB Hub Admin"] = function() loadstring(game:HttpGet("https://rawscripts.net/raw/Slap-Battles-Edgelord-Admin-38263"))() end,
        }
    },
    [20] = {
        Name = "Build a Boat", Icon = "🛶",
        Key = { ["BABFT Hub"] = function() loadstring(game:HttpGet('https://raw.githubusercontent.com/TheRealAsu/BABFT/refs/heads/main/Loader.lua'))() end },
        NoKey = { ["Roubar Construções"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/max2007killer/auto-build-not-limit/main/buildaboatv2obs.txt", true))() end }
    },
    [21] = {
        Name = "Grow a Garden", Icon = "🌴",
        Key = { 
            ["Ronix Hub"] = function() loadstring(game:HttpGet("https://rawscripts.net/raw/Grow-a-Garden-Best-Autofarm-Script-GUI-73698"))() end,
            ["Speed Hub GG"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/AhmadV99/Speed-Hub-X/main/Speed%20Hub%20X.lua"))() end
        },
        NoKey = {}
    },
    [22] = {
        Name = "Campos de Batalha", Icon = "👊",
        Key = {},
        NoKey = { ["Aim Bot-Aim Lock"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/Cyborg883/CombatGUI/refs/heads/main/TSBCombatGUI"))() end }
    },
    [23] = {
        Name = "Death Ball", Icon = "💀",
        Key = { ["Native Hub"] = function() loadstring(game:HttpGet("https://getnative.cc/script/loader"))() end },
        NoKey = {}
    },
    [24] = {
        Name = "Dead Rails", Icon = "🚂",
        Key = {},
        NoKey = { ["DR Hub"] = function() loadstring(game:HttpGet("https://raw.githubusercontent.com/gumanba/Scripts/refs/heads/main/DeadRails", true))() end }
    },
    [25] = {
        Name = "Ninja Legends", Icon = "🥷",
        Key = {},
        NoKey = {
            ["Proxima Hub"] = function()
                loadstring(game:HttpGet("https://raw.githubusercontent.com/TrixAde/Proxima-Hub/main/Main.lua"))()
            end,
            ["Ninja Hero Hub"] = function()
                loadstring(game:HttpGet("https://rawscripts.net/raw/Ninja-Legends-Ninja-Hero-Hub-2656"))()
            end
        }
    },
    [26] = {
        Name = "Jujutsu Shenanigans", Icon = "☯︎",
        Key = {
            ["DeadScripter"] = function()
                loadstring(game:HttpGet("https://raw.githubusercontent.com/DeadScripter/Deadhub/refs/heads/main/DeadLoader.lua"))()
            end,
            ["Jujutsu Shenanigans"] = function()
                loadstring(game:HttpGet('https://raw.githubusercontent.com/grebblylaort/Jujutsu-Shenanigans-FREE_NO_KEY/main/main.lua'))()
            end
        },
        NoKey = {
            ["Plutonium"] = function()
                loadstring(game:HttpGet("https://raw.githubusercontent.com/PawsThePaw/Plutonium.AA/main/Plutonium.Loader.lua", true))()
            end,
            ["TBO"] = function()
                loadstring(game:HttpGet("https://raw.githubusercontent.com/cool5013/TBO/main/TBOscript"))()
            end
        }
    },
    [27] = {
        Name = "Lendas da Velocidade", Icon = "⚡",
        Key = {
            ["Legends of Speed (KEY: calar1)"] = function()
                loadstring(game:HttpGet("https://rawscripts.net/raw/Legends-Of-Speed-OP-INFINITE-LEVEL-FARM-STEPS-FAST-UPDATED-31535"))()
            end
        },
        NoKey = {}
    },
    [28] = {
        Name = "Hide and Seek", Icon = "👁️",
        Key = {},
        NoKey = {
            ["Milk Script"] = function()
                pcall(function()
                    loadstring(game:HttpGet("https://raw.githubusercontent.com/usemilk/Milk-script/main/main.lua", true))()
                end)
            end
        }
    }
}

-- [PARTE 2: CRIAÇÃO DA UI — VERSÃO FINAL PADRONIZADA + ATUALIZAÇÕES]
local ScreenGui = Instance.new("ScreenGui", LocalPlayer.PlayerGui)
ScreenGui.Name = "SFZ_V3_Final"
ScreenGui.ResetOnSpawn = false

local function Notify(title, msg)
    local NotifFrame = Instance.new("Frame", ScreenGui)
    NotifFrame.Size = UDim2.new(0, 220, 0, 60)
    NotifFrame.Position = UDim2.new(1, 10, 1, -70)
    NotifFrame.BackgroundColor3 = Color3.fromRGB(45, 0, 80)
    Instance.new("UICorner", NotifFrame).CornerRadius = UDim.new(0, 10)
    local ns = Instance.new("UIStroke", NotifFrame)
    ns.Color = Color3.fromRGB(110, 0, 190)
    ns.Thickness = 2
    
    local t = Instance.new("TextLabel", NotifFrame)
    t.Text = title; t.Size = UDim2.new(1, -20, 0, 25); t.Position = UDim2.new(0, 10, 0, 5)
    t.BackgroundTransparency = 1; t.TextColor3 = Color3.new(1,1,1); t.Font = Enum.Font.GothamBold; t.TextSize = 13; t.TextXAlignment = Enum.TextXAlignment.Left
    
    local m = Instance.new("TextLabel", NotifFrame)
    m.Text = msg; m.Size = UDim2.new(1, -20, 0, 25); m.Position = UDim2.new(0, 10, 0, 30)
    m.BackgroundTransparency = 1; m.TextColor3 = Color3.fromRGB(200, 200, 200); m.Font = Enum.Font.Gotham; m.TextSize = 11; m.TextXAlignment = Enum.TextXAlignment.Left; m.TextWrapped = true

    NotifFrame:TweenPosition(UDim2.new(1, -230, 1, -70), "Out", "Back", 0.5, true)
    task.delay(3, function()
        if NotifFrame then
            NotifFrame:TweenPosition(UDim2.new(1, 10, 1, -70), "In", "Back", 0.5, true)
            task.wait(0.5); NotifFrame:Destroy()
        end
    end)
end

local MainFrame = Instance.new("Frame", ScreenGui)
MainFrame.Size = UDim2.new(0, 620, 0, 380)
MainFrame.Position = UDim2.new(0.5, -310, 0.5, -190)
MainFrame.BackgroundColor3 = Color3.fromRGB(25, 0, 45)
MainFrame.BorderSizePixel = 0
MainFrame.ClipsDescendants = true
MainFrame.Visible = false 
Instance.new("UICorner", MainFrame).CornerRadius = UDim.new(0, 15)

--- // BORDA DO PAINEL PADRONIZADA // ---
local MainStroke = Instance.new("UIStroke", MainFrame)
MainStroke.Color = Color3.fromRGB(120, 0, 210) 
MainStroke.Thickness = 2.5
MainStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border

local TopBar = Instance.new("Frame", MainFrame)
TopBar.Size = UDim2.new(1, 0, 0, 45)
TopBar.BackgroundColor3 = Color3.fromRGB(45, 0, 80)
TopBar.ZIndex = 10
Instance.new("UICorner", TopBar).CornerRadius = UDim.new(0, 15)

local Title = Instance.new("TextLabel", TopBar)
Title.Size = UDim2.new(1, -300, 1, 0)
Title.Position = UDim2.new(0, 0, 0, 0)
Title.BackgroundTransparency = 1
Title.Text = "ScriptLand Hub Script Universal | Português (BR)"
Title.TextColor3 = Color3.new(1,1,1)
Title.Font = Enum.Font.GothamBold; Title.TextSize = 13; Title.TextXAlignment = Enum.TextXAlignment.Left; Title.ZIndex = 11

local Holder = Instance.new("Frame", MainFrame)
Holder.Size = UDim2.new(1, 0, 1, -45); Holder.Position = UDim2.new(0, 0, 0, 45); Holder.BackgroundTransparency = 1

local Sidebar = Instance.new("ScrollingFrame", Holder)
Sidebar.Size = UDim2.new(0, 200, 1, -10); Sidebar.Position = UDim2.new(0, 10, 0, 5); Sidebar.BackgroundTransparency = 1; Sidebar.ScrollBarThickness = 2
Sidebar.CanvasSize = UDim2.new(0, 0, 0, 1400)
local SideLayout = Instance.new("UIListLayout", Sidebar); SideLayout.Padding = UDim.new(0, 8)

local Content = Instance.new("Frame", Holder)
Content.Size = UDim2.new(1, -230, 1, -10); Content.Position = UDim2.new(0, 220, 0, 5); Content.BackgroundColor3 = Color3.fromRGB(35, 0, 60)
Instance.new("UICorner", Content)

local TabArea = Instance.new("Frame", Content)
TabArea.Size = UDim2.new(0.4, 0, 1, 0); TabArea.BackgroundTransparency = 1

local ScriptList = Instance.new("ScrollingFrame", Content)
ScriptList.Size = UDim2.new(0.6, -10, 1, -10); ScriptList.Position = UDim2.new(0.4, 5, 0, 5); ScriptList.BackgroundTransparency = 1; ScriptList.ScrollBarThickness = 2
local ListLayout = Instance.new("UIListLayout", ScriptList); ListLayout.Padding = UDim.new(0, 5)

--- // ATUALIZAÇÃO: BOTÃO INVISÍVEL PARA REDIMENSIONAR // ---
local ResizeBtn = Instance.new("TextButton", MainFrame)
ResizeBtn.Name = "ResizeBtn"
ResizeBtn.Size = UDim2.new(0, 30, 0, 30)
ResizeBtn.Position = UDim2.new(1, -30, 1, -30) -- Canto inferior direito
ResizeBtn.BackgroundTransparency = 1
ResizeBtn.Text = ""
ResizeBtn.ZIndex = 100

-- ///////////////////////////////////////////////////////
-- BLOCO ATUALIZADO: SISTEMA DE CARREGAMENTO, FAVORITOS E POSIÇÃO DO "VAZIO"
-- ///////////////////////////////////////////////////////

local function ShowExecuteConfirmation(scriptName, executeFunc)
    if ScreenGui:FindFirstChild("ConfirmExecFrame") then ScreenGui.ConfirmExecFrame:Destroy() end
    local ConfirmFrame = Instance.new("Frame", ScreenGui)
    ConfirmFrame.Name = "ConfirmExecFrame"
    ConfirmFrame.Size = UDim2.new(0, 350, 0, 180); ConfirmFrame.Position = UDim2.new(0.5, -175, 0.5, -90); ConfirmFrame.BackgroundColor3 = Color3.fromRGB(35, 0, 60)
    ConfirmFrame.ZIndex = 5000; Instance.new("UICorner", ConfirmFrame).CornerRadius = UDim.new(0, 15)
    
    local UIGradient = Instance.new("UIGradient", ConfirmFrame)
    UIGradient.Color = ColorSequence.new({ColorSequenceKeypoint.new(0, Color3.fromRGB(80, 0, 150)), ColorSequenceKeypoint.new(1, Color3.fromRGB(35, 0, 60))})
    UIGradient.Rotation = 90
    local Stroke = Instance.new("UIStroke", ConfirmFrame); Stroke.Color = Color3.fromRGB(120, 0, 210); Stroke.Thickness = 2

    local TitleC = Instance.new("TextLabel", ConfirmFrame)
    TitleC.Text = "Executar"; TitleC.Size = UDim2.new(1, -20, 0, 30); TitleC.Position = UDim2.new(0, 15, 0, 10)
    TitleC.TextColor3 = Color3.new(1,1,1); TitleC.Font = Enum.Font.GothamBold; TitleC.TextSize = 22; TitleC.TextXAlignment = Enum.TextXAlignment.Left; TitleC.BackgroundTransparency = 1; TitleC.ZIndex = 5001

    local Msg = Instance.new("TextLabel", ConfirmFrame)
    Msg.Text = "Você deseja realmente executar esse script?\n("..scriptName..")"
    Msg.Size = UDim2.new(1, -30, 0, 80); Msg.Position = UDim2.new(0, 15, 0, 45); Msg.TextColor3 = Color3.fromRGB(220, 220, 220)
    Msg.Font = Enum.Font.Gotham; Msg.TextSize = 15; Msg.TextWrapped = true; Msg.TextXAlignment = Enum.TextXAlignment.Left; Msg.TextYAlignment = Enum.TextYAlignment.Top; Msg.BackgroundTransparency = 1; Msg.ZIndex = 5001

    local YesBtn = Instance.new("TextButton", ConfirmFrame)
    YesBtn.Text = "Sim"; YesBtn.Size = UDim2.new(0, 100, 0, 40); YesBtn.Position = UDim2.new(0.2, 0, 0.8, -10); YesBtn.TextColor3 = Color3.fromRGB(100, 255, 100); YesBtn.Font = Enum.Font.GothamBold; YesBtn.TextSize = 18; YesBtn.BackgroundTransparency = 1; YesBtn.ZIndex = 5001

    local NoBtn = Instance.new("TextButton", ConfirmFrame)
    NoBtn.Text = "Não"; NoBtn.Size = UDim2.new(0, 100, 0, 40); NoBtn.Position = UDim2.new(0.5, 30, 0.8, -10); NoBtn.TextColor3 = Color3.fromRGB(255, 100, 100); NoBtn.Font = Enum.Font.GothamBold; NoBtn.TextSize = 18; NoBtn.BackgroundTransparency = 1; NoBtn.ZIndex = 5001

    YesBtn.MouseButton1Click:Connect(function() ConfirmFrame:Destroy(); Notify("EXECUTANDO", "Ativando: "..scriptName); pcall(executeFunc) end)
    NoBtn.MouseButton1Click:Connect(function() ConfirmFrame:Destroy() end)
end

local function LoadScripts(tbl, gameData)
    for _, v in pairs(ScriptList:GetChildren()) do 
        if v:IsA("Frame") or v:IsA("TextLabel") or v:IsA("TextButton") or v:IsA("UIPadding") then v:Destroy() end 
    end
    
    local count = 0
    if tbl then for _ in pairs(tbl) do count = count + 1 end end
    
    if count == 0 then
        local Padding = Instance.new("UIPadding", ScriptList)
        Padding.PaddingTop = UDim.new(0, 5)

        local EmptyMsg = Instance.new("TextLabel", ScriptList)
        EmptyMsg.AutoLocalize = false -- Adicionado
        EmptyMsg.Size = UDim2.new(1, -10, 0, 30)
        EmptyMsg.BackgroundTransparency = 1
        EmptyMsg.Text = "🚫 VAZIO..."
        EmptyMsg.TextColor3 = Color3.new(1,1,1)
        EmptyMsg.Font = Enum.Font.GothamBold
        EmptyMsg.TextSize = 14
        EmptyMsg.TextTransparency = 0.4
        EmptyMsg.TextXAlignment = Enum.TextXAlignment.Center
    else
        for name, data in pairs(tbl) do
            local executeFunc = type(data) == "function" and data or data.func
            local originGame = type(data) == "table" and data.originalGameName or gameData.Name

            local ItemFrame = Instance.new("Frame", ScriptList)
            ItemFrame.Size = UDim2.new(1, -10, 0, 35); ItemFrame.BackgroundTransparency = 1
            
            local b = Instance.new("TextButton", ItemFrame)
            b.AutoLocalize = false -- BLOQUEIA TRADUÇÃO DO "FLY"
            b.Size = UDim2.new(0.82, 0, 1, 0); b.BackgroundColor3 = Color3.fromRGB(110, 0, 190); b.Text = name; 
            b.TextColor3 = Color3.new(1,1,1); b.Font = Enum.Font.GothamBold; b.TextSize = 14
            Instance.new("UICorner", b).CornerRadius = UDim.new(0, 8)
            b.MouseButton1Click:Connect(function() ShowExecuteConfirmation(name, executeFunc) end)

            local favBtn = Instance.new("TextButton", ItemFrame)
            favBtn.AutoLocalize = false -- Adicionado
            favBtn.Size = UDim2.new(0.15, 0, 1, 0); favBtn.Position = UDim2.new(0.85, 0, 0, 0); favBtn.BackgroundColor3 = Color3.fromRGB(60, 0, 110)
            
            local function UpdateStar()
                local favs = GetFavorites()
                local isFav = favs[originGame] and table.find(favs[originGame], name)
                favBtn.Text = isFav and "⭐" or "☆"
            end
            UpdateStar()
            
            favBtn.TextColor3 = Color3.new(1, 1, 0); favBtn.TextSize = 18
            Instance.new("UICorner", favBtn).CornerRadius = UDim.new(0, 8)

            favBtn.MouseButton1Click:Connect(function()
                local added = ToggleFavorite(name, originGame)
                UpdateStar()
                Notify("FAVORITOS", added and "Adicionado: "..name or "Removido: "..name)
                if not added and gameData.Name == "Favoritos" then
                    ItemFrame:Destroy()
                    local remaining = 0
                    for _, child in pairs(ScriptList:GetChildren()) do if child:IsA("Frame") then remaining = remaining + 1 end end
                    if remaining == 0 then LoadScripts({}, {Name = "Favoritos"}) end
                end
            end)
        end
    end
end

local function OpenGame(data)
    -- LIMPEZA: Remove scripts da direita ao trocar de jogo (essencial para o que você pediu)
    for _, v in pairs(ScriptList:GetChildren()) do 
        if v:IsA("Frame") or v:IsA("TextLabel") or v:IsA("TextButton") or v:IsA("UIPadding") then v:Destroy() end 
    end

    for _, v in pairs(TabArea:GetChildren()) do if v:IsA("TextButton") or v:IsA("TextLabel") then v:Destroy() end end
    local StatusLabel = Instance.new("TextLabel", TabArea)
    StatusLabel.Size = UDim2.new(1, -10, 0, 30); StatusLabel.Position = UDim2.new(0, 5, 0, 5); StatusLabel.BackgroundTransparency = 1; StatusLabel.Text = "Você está em: " .. data.Name; StatusLabel.TextColor3 = Color3.fromRGB(220, 220, 220); StatusLabel.Font = Enum.Font.GothamMedium; StatusLabel.TextSize = 11; StatusLabel.TextWrapped = true

    local function createTab(txt, y, col, tbl)
        local btn = Instance.new("TextButton", TabArea)
        btn.Size = UDim2.new(1, -10, 0, 50); btn.Position = UDim2.new(0, 5, 0, y); btn.Text = txt; btn.BackgroundColor3 = col; btn.TextColor3 = Color3.new(1,1,1); btn.TextSize = 13; btn.Font = Enum.Font.GothamBold
        Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 10)
        btn.MouseButton1Click:Connect(function() LoadScripts(tbl, data) end)
    end
    createTab("COM KEY 🔑", 45, Color3.fromRGB(50, 150, 90), data.Key)
    createTab("SEM KEY ❌", 105, Color3.fromRGB(160, 50, 50), data.NoKey)
end

local FavTabBtn = Instance.new("TextButton", Sidebar)
FavTabBtn.Size = UDim2.new(1, -10, 0, 45); FavTabBtn.BackgroundColor3 = Color3.fromRGB(200, 160, 0); FavTabBtn.Text = "⭐ MEUS FAVORITOS"; FavTabBtn.TextColor3 = Color3.new(0,0,0); FavTabBtn.Font = Enum.Font.GothamBold; FavTabBtn.TextSize = 13; FavTabBtn.LayoutOrder = -1; Instance.new("UICorner", FavTabBtn)

FavTabBtn.MouseButton1Click:Connect(function()
    -- Limpa tudo ao abrir favoritos
    for _, v in pairs(ScriptList:GetChildren()) do if v:IsA("Frame") or v:IsA("TextLabel") or v:IsA("TextButton") or v:IsA("UIPadding") then v:Destroy() end end
    for _, v in pairs(TabArea:GetChildren()) do if v:IsA("TextButton") or v:IsA("TextLabel") then v:Destroy() end end
    
    local StatusLabel = Instance.new("TextLabel", TabArea)
    StatusLabel.Size = UDim2.new(1, -10, 0, 30); StatusLabel.Position = UDim2.new(0, 5, 0, 5); StatusLabel.BackgroundTransparency = 1; StatusLabel.Text = "Seus Scripts Favoritos"; StatusLabel.TextColor3 = Color3.fromRGB(255, 215, 0); StatusLabel.Font = Enum.Font.GothamBold; StatusLabel.TextSize = 12; StatusLabel.TextWrapped = true
    
    local allFavs = GetFavorites(); local favListTbl = {}
    for gName, scripts in pairs(allFavs) do
        for _, gData in pairs(Database) do 
            if gData.Name == gName then 
                for _, sName in pairs(scripts) do 
                    local func = gData.Key[sName] or gData.NoKey[sName]
                    if func then favListTbl[sName] = {func = func, originalGameName = gName} end 
                end 
            end 
        end
    end
    LoadScripts(favListTbl, {Name = "Favoritos"})
    Notify("LISTA", "Carregando seus favoritos...")
end)

for i = 1, #Database do
    local info = Database[i]
    if info then
        local btn = Instance.new("TextButton", Sidebar)
        btn.AutoLocalize = false -- IMPEDE TRADUÇÃO DOS NOMES DOS JOGOS
        btn.Size = UDim2.new(1, -10, 0, 40); btn.BackgroundColor3 = Color3.fromRGB(75, 0, 130); btn.Text = info.Icon .. " " .. info.Name; btn.TextColor3 = Color3.new(1,1,1); btn.Font = Enum.Font.GothamBold; btn.TextSize = 13
        Instance.new("UICorner", btn); btn.MouseButton1Click:Connect(function() OpenGame(info) end)
    end
end

-- [PARTE 5: CONTROLES DO TOPO, BUSCA, ARRASTE E REDIMENSIONAMENTO]

-- 1. FUNÇÃO DO AVISO DE FECHAR (COM TRAVA DE SEGURANÇA E DESIGN ORIGINAL)
local function ShowCloseConfirmation()
    if ScreenGui:FindFirstChild("ConfirmCloseFrame") then 
        ScreenGui.ConfirmCloseFrame:Destroy() 
    end

    local ConfirmFrame = Instance.new("Frame", ScreenGui)
    ConfirmFrame.Name = "ConfirmCloseFrame"
    ConfirmFrame.Size = UDim2.new(0, 350, 0, 180)
    ConfirmFrame.Position = UDim2.new(0.5, -175, 0.5, -90)
    ConfirmFrame.BackgroundColor3 = Color3.fromRGB(35, 0, 60)
    ConfirmFrame.BorderSizePixel = 0
    ConfirmFrame.ZIndex = 5000 
    Instance.new("UICorner", ConfirmFrame).CornerRadius = UDim.new(0, 15)

    local UIGradient = Instance.new("UIGradient", ConfirmFrame)
    UIGradient.Color = ColorSequence.new({
        ColorSequenceKeypoint.new(0, Color3.fromRGB(80, 0, 150)), 
        ColorSequenceKeypoint.new(1, Color3.fromRGB(35, 0, 60))
    })
    UIGradient.Rotation = 90

    local Stroke = Instance.new("UIStroke", ConfirmFrame)
    Stroke.Color = Color3.fromRGB(120, 0, 210)
    Stroke.Thickness = 2

    local TitleC = Instance.new("TextLabel", ConfirmFrame)
    TitleC.Text = "Fechar Hub"; TitleC.Size = UDim2.new(1, -20, 0, 30); TitleC.Position = UDim2.new(0, 15, 0, 10)
    TitleC.TextColor3 = Color3.new(1, 1, 1); TitleC.Font = Enum.Font.GothamBold; TitleC.TextSize = 20
    TitleC.TextXAlignment = Enum.TextXAlignment.Left; TitleC.BackgroundTransparency = 1; TitleC.ZIndex = 5001

    local Msg = Instance.new("TextLabel", ConfirmFrame)
    Msg.Text = "Você realmente deseja fechar o Universal ScriptLand Hub?\nSerá necessário reexecutar para usá-lo novamente."
    Msg.Size = UDim2.new(1, -30, 0, 80); Msg.Position = UDim2.new(0, 15, 0, 45)
    Msg.TextColor3 = Color3.fromRGB(220, 220, 220); Msg.Font = Enum.Font.Gotham; Msg.TextSize = 15
    Msg.TextWrapped = true; Msg.TextXAlignment = Enum.TextXAlignment.Left; Msg.TextYAlignment = Enum.TextYAlignment.Top
    Msg.BackgroundTransparency = 1; Msg.ZIndex = 5001

    local ConfirmBtn = Instance.new("TextButton", ConfirmFrame)
    ConfirmBtn.Text = "Confirmar"; ConfirmBtn.Size = UDim2.new(0, 100, 0, 40); ConfirmBtn.Position = UDim2.new(0.2, 0, 0.8, -10)
    ConfirmBtn.TextColor3 = Color3.fromRGB(255, 50, 50); ConfirmBtn.Font = Enum.Font.GothamBold; ConfirmBtn.TextSize = 16
    ConfirmBtn.BackgroundTransparency = 1; ConfirmBtn.ZIndex = 5001

    local CancelBtn = Instance.new("TextButton", ConfirmFrame)
    CancelBtn.Text = "Cancelar"; CancelBtn.Size = UDim2.new(0, 100, 0, 40); CancelBtn.Position = UDim2.new(0.5, 30, 0.8, -10)
    CancelBtn.TextColor3 = Color3.fromRGB(255, 255, 255); CancelBtn.Font = Enum.Font.GothamBold; CancelBtn.TextSize = 16
    CancelBtn.BackgroundTransparency = 1; CancelBtn.ZIndex = 5001

    ConfirmBtn.MouseButton1Click:Connect(function() ScreenGui:Destroy() end)
    CancelBtn.MouseButton1Click:Connect(function() ConfirmFrame:Destroy() end)
end

-- 2. LUPA (BARRA DE BUSCA)
local SearchBar = Instance.new("TextBox", TopBar)
SearchBar.Size = UDim2.new(0, 140, 0, 28); SearchBar.Position = UDim2.new(1, -240, 0, 8)
SearchBar.PlaceholderText = "🔍 Buscar Jogo..."; SearchBar.Text = ""
SearchBar.BackgroundColor3 = Color3.fromRGB(60, 0, 110); SearchBar.TextColor3 = Color3.new(1,1,1)
SearchBar.Font = Enum.Font.Gotham; SearchBar.TextSize = 12; SearchBar.ZIndex = 15
Instance.new("UICorner", SearchBar).CornerRadius = UDim.new(0, 8)

SearchBar:GetPropertyChangedSignal("Text"):Connect(function()
    local searchText = SearchBar.Text:lower()
    for _, btn in pairs(Sidebar:GetChildren()) do
        if btn:IsA("TextButton") then
            btn.Visible = btn.Text:lower():find(searchText) ~= nil
        end
    end
end)

-- 3. BOTÕES DO TOPO (X E —)
local function CreateTopBtn(txt, pos, color, func)
    local btn = Instance.new("TextButton", TopBar)
    btn.Size = UDim2.new(0, 32, 0, 32); btn.Position = pos; btn.Text = txt
    btn.BackgroundColor3 = color; btn.TextColor3 = Color3.new(1,1,1)
    btn.Font = Enum.Font.GothamBold; btn.ZIndex = 15
    Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 8)
    btn.MouseButton1Click:Connect(func)
end

CreateTopBtn("X", UDim2.new(1, -40, 0, 6), Color3.fromRGB(220, 50, 50), ShowCloseConfirmation)

CreateTopBtn("—", UDim2.new(1, -80, 0, 6), Color3.fromRGB(60, 60, 180), function()
    if Holder.Visible then
        Holder.Visible = false
        MainFrame:TweenSize(UDim2.new(0, MainFrame.Size.X.Offset, 0, 45), "Out", "Quart", 0.3, true)
    else
        Holder.Visible = true
        MainFrame:TweenSize(UDim2.new(0, MainFrame.Size.X.Offset, 0, 380), "Out", "Quart", 0.3, true)
    end
end)

-- 4. SISTEMA DE ARRASTE E REDIMENSIONAMENTO (ATUALIZADO)
local dragToggle, dragStart, startPos
local resizing = false
local resizeStartPos, startSize

-- Lógica de Início (Arraste ou Resize)
TopBar.InputBegan:Connect(function(input)
    if (input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch) and not resizing then
        dragToggle = true; dragStart = input.Position; startPos = MainFrame.Position
    end
end)

ResizeBtn.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        resizing = true; resizeStartPos = input.Position; startSize = MainFrame.Size
        dragToggle = false
    end
end)

-- Lógica de Movimento
game:GetService("UserInputService").InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
        if dragToggle then
            local delta = input.Position - dragStart
            MainFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
        elseif resizing then
            local delta = input.Position - resizeStartPos
            MainFrame.Size = UDim2.new(0, math.max(450, startSize.X.Offset + delta.X), 0, math.max(250, startSize.Y.Offset + delta.Y))
        end
    end
end)

-- Lógica de Finalização
game:GetService("UserInputService").InputEnded:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragToggle = false
        resizing = false
    end
end)

-- [PARTE 6: MENSAGEM DE DISCORD E FINALIZAÇÃO — VERSÃO ATUALIZADA POR RAFAEL]
local function ShowDiscordInvite()
    if ScreenGui:FindFirstChild("DiscordInviteFrame") then ScreenGui.DiscordInviteFrame:Destroy() end
    local InviteFrame = Instance.new("Frame", ScreenGui)
    InviteFrame.Name = "DiscordInviteFrame"; InviteFrame.Size = UDim2.new(0, 400, 0, 220); InviteFrame.Position = UDim2.new(0.5, -200, 0.5, -110); InviteFrame.BackgroundColor3 = Color3.fromRGB(10, 0, 20); InviteFrame.ZIndex = 9000
    Instance.new("UICorner", InviteFrame).CornerRadius = UDim.new(0, 15)
    
    local Stroke = Instance.new("UIStroke", InviteFrame)
    Stroke.Color = Color3.fromRGB(120, 0, 210)
    Stroke.Thickness = 2

    local TitleD = Instance.new("TextLabel", InviteFrame)
    TitleD.AutoLocalize = false
    TitleD.Text = "Discord & Amizade"; TitleD.Size = UDim2.new(1, -40, 0, 40); TitleD.Position = UDim2.new(0, 20, 0, 15); TitleD.TextColor3 = Color3.new(1,1,1); TitleD.Font = Enum.Font.GothamBold; TitleD.TextSize = 18; TitleD.TextXAlignment = Enum.TextXAlignment.Left; TitleD.BackgroundTransparency = 1; TitleD.ZIndex = 9001

    local MsgD = Instance.new("TextLabel", InviteFrame)
    MsgD.AutoLocalize = false
    -- MENSAGEM QUE VOCÊ PEDIU
    MsgD.Text = "Clique em ok para copiar o link do nosso servidor e depois cole no seu navegador"; 
    MsgD.Size = UDim2.new(1, -40, 0, 80); MsgD.Position = UDim2.new(0, 20, 0, 55); MsgD.TextColor3 = Color3.fromRGB(200, 200, 200); MsgD.Font = Enum.Font.Gotham; MsgD.TextSize = 15; MsgD.TextXAlignment = Enum.TextXAlignment.Left; MsgD.TextWrapped = true; MsgD.BackgroundTransparency = 1; MsgD.ZIndex = 9001

    local OkBtn = Instance.new("TextButton", InviteFrame)
    OkBtn.AutoLocalize = false
    OkBtn.Text = "OK!"; OkBtn.Size = UDim2.new(0, 140, 0, 40); OkBtn.Position = UDim2.new(0.5, -70, 0.85, -15); OkBtn.BackgroundColor3 = Color3.fromRGB(110, 0, 190); OkBtn.TextColor3 = Color3.new(1, 1, 1); OkBtn.Font = Enum.Font.GothamBold; OkBtn.TextSize = 18; OkBtn.ZIndex = 9001; Instance.new("UICorner", OkBtn).CornerRadius = UDim.new(0, 10)

    -- OK AGORA COPIA O SEU NOME drezin.21
    OkBtn.MouseButton1Click:Connect(function() 
        if setclipboard then 
            setclipboard("https://discord.gg/fjxS6CJ8GS") 
            Notify("COPIADO", "Entre no Discord do ScriptLand Hub para saber mais") 
        end 
        InviteFrame:Destroy() 
    end)
end

local FloatBtn = Instance.new("ImageButton", ScreenGui)
FloatBtn.Size = UDim2.new(0, 45, 0, 45)
FloatBtn.Position = UDim2.new(0, 15, 0.5, -22)
FloatBtn.BackgroundColor3 = Color3.fromRGB(45, 0, 80)
FloatBtn.ZIndex = 200
FloatBtn.Image = LogoImage or ""
FloatBtn.ScaleType = Enum.ScaleType.Fit
FloatBtn.ImageTransparency = LogoImage and 0 or 1
FloatBtn.Visible = false
Instance.new("UICorner", FloatBtn).CornerRadius = UDim.new(1, 0)

-- Se o executor não suportar assets locais, mostra uma marca simples em vez de um botão vazio.
if not LogoImage then
    local LogoFallback = Instance.new("TextLabel", FloatBtn)
    LogoFallback.Name = "LogoFallback"
    LogoFallback.Size = UDim2.new(1, 0, 1, 0)
    LogoFallback.BackgroundTransparency = 1
    LogoFallback.Text = "SL"
    LogoFallback.TextColor3 = Color3.fromRGB(0, 220, 255)
    LogoFallback.Font = Enum.Font.GothamBlack
    LogoFallback.TextSize = 17
    LogoFallback.ZIndex = 201
end

local FloatStroke = Instance.new("UIStroke", FloatBtn)
FloatStroke.Color = Color3.fromRGB(120, 0, 210)
FloatStroke.Thickness = 2.5

FloatBtn.Active = true; FloatBtn.Draggable = true

FloatBtn.MouseButton1Click:Connect(function()
    if not MainFrame.Visible then
        Holder.Visible = true 
        MainFrame.Size = UDim2.new(0, 0, 0, 0)
        MainFrame.Visible = true
        MainFrame:TweenSize(UDim2.new(0, 620, 0, 380), "Out", "Back", 0.5, true)
    else 
        MainFrame:TweenSize(UDim2.new(0, 0, 0, 0), "In", "Back", 0.4, true)
        task.wait(0.4)
        MainFrame.Visible = false
        MainFrame.Size = UDim2.new(0, 620, 0, 380) 
    end
end)

local IntroFrame = Instance.new("Frame", ScreenGui)
IntroFrame.Size = UDim2.new(0, 350, 0, 80); IntroFrame.Position = UDim2.new(0.5, -175, 0.5, -40); IntroFrame.BackgroundColor3 = Color3.fromRGB(35, 0, 60); IntroFrame.ZIndex = 500; Instance.new("UICorner", IntroFrame).CornerRadius = UDim.new(0, 15)

local IntroStroke = Instance.new("UIStroke", IntroFrame)
IntroStroke.Color = Color3.fromRGB(120, 0, 210)
IntroStroke.Thickness = 3

local IntroText = Instance.new("TextLabel", IntroFrame)
IntroText.Size = UDim2.new(1, 0, 1, 0); IntroText.BackgroundTransparency = 1; 
-- TÍTULO DA INTRO ATUALIZADO
IntroText.Text = "Carregando Script Universal Hub..."; 
IntroText.TextColor3 = Color3.new(1, 1, 1); IntroText.Font = Enum.Font.GothamBold; IntroText.TextSize = 18; IntroText.ZIndex = 501

task.spawn(function()
    local startTime = tick()
    while tick() - startTime < 3 do
        local pulse = 1 + (0.06 * math.sin(tick() * 4)) 
        IntroFrame.Size = UDim2.new(0, 350 * pulse, 0, 80 * pulse); IntroFrame.Position = UDim2.new(0.5, -(350 * pulse)/2, 0.5, -(80 * pulse)/2)
        task.wait()
    end
    TweenService:Create(IntroFrame, TweenInfo.new(0.6), {BackgroundTransparency = 1}):Play()
    TweenService:Create(IntroStroke, TweenInfo.new(0.6), {Transparency = 1}):Play()
    TweenService:Create(IntroText, TweenInfo.new(0.6), {TextTransparency = 1}):Play()
    task.wait(0.6); IntroFrame:Destroy(); FloatBtn.Visible = true; MainFrame.Size = UDim2.new(0, 0, 0, 0); MainFrame.Visible = true; MainFrame:TweenSize(UDim2.new(0, 620, 0, 380), "Out", "Back", 0.6, true)
    
    -- NOTIFICAÇÃO AO ABRIR
    Notify("HUB ATIVO", "Bem-vindo ao Script Universal do ScriptLand Hub!")
    task.delay(1, ShowDiscordInvite) 
end)
    print("Script Universal Hub Iniciado!")
end 

-- // 4. INTERFACE DA JANELA DE KEY (RESTAURADA AO ESTILO ORIGINAL) // --
local KeyGui = Instance.new("ScreenGui", LocalPlayer.PlayerGui)
KeyGui.Name = "SistemaDeKey_ScriptLand"

local KeyMain = Instance.new("Frame", KeyGui)
KeyMain.Size = UDim2.new(0, 340, 0, 260)
KeyMain.Position = UDim2.new(0.5, -170, 0.5, -130)
KeyMain.BackgroundColor3 = Color3.fromRGB(25, 0, 45)
KeyMain.BorderSizePixel = 0
Instance.new("UICorner", KeyMain).CornerRadius = UDim.new(0, 15)

-- Borda Roxa da Janela Principal
local MainStroke = Instance.new("UIStroke", KeyMain)
MainStroke.Color = Color3.fromRGB(120, 0, 210)
MainStroke.Thickness = 2.5
MainStroke.ApplyStrokeMode = Enum.ApplyStrokeMode.Border

-- Função de Notificação Original (Com Animação Back e Borda Roxa)
local function CustomNotify(title, msg, isError, customColor)
    local NotifFrame = Instance.new("Frame", KeyGui)
    NotifFrame.Size = UDim2.new(0, 220, 0, 60)
    NotifFrame.Position = UDim2.new(1, 10, 1, -70) -- Começa fora da tela
    NotifFrame.BackgroundColor3 = Color3.fromRGB(45, 0, 80)
    Instance.new("UICorner", NotifFrame).CornerRadius = UDim.new(0, 10)
    
    local ns = Instance.new("UIStroke", NotifFrame)
    -- Lógica de cor da borda: Se houver cor custom (sucesso), usa ela. Se erro, vermelho. Senão, azul padrão.
    ns.Color = customColor or (isError and Color3.fromRGB(255, 50, 50) or Color3.fromRGB(0, 0, 255))
    ns.Thickness = 2
    
    local t = Instance.new("TextLabel", NotifFrame)
    t.Text = title; t.Size = UDim2.new(1, -20, 0, 25); t.Position = UDim2.new(0, 10, 0, 5)
    t.BackgroundTransparency = 1; t.TextColor3 = Color3.new(1,1,1); t.Font = Enum.Font.GothamBold; t.TextSize = 13; t.TextXAlignment = Enum.TextXAlignment.Left
    
    local m = Instance.new("TextLabel", NotifFrame)
    m.Text = msg; m.Size = UDim2.new(1, -20, 0, 25); m.Position = UDim2.new(0, 10, 0, 30)
    m.BackgroundTransparency = 1; m.TextColor3 = Color3.fromRGB(200, 200, 200); m.Font = Enum.Font.Gotham; m.TextSize = 11; m.TextXAlignment = Enum.TextXAlignment.Left

    -- Animação de entrada (Slide para a esquerda)
    NotifFrame:TweenPosition(UDim2.new(1, -230, 1, -70), "Out", "Back", 0.5, true)
    
    task.delay(3, function()
        if NotifFrame then
            -- Animação de saída (Slide para a direita)
            NotifFrame:TweenPosition(UDim2.new(1, 10, 1, -70), "In", "Back", 0.5, true)
            task.wait(0.5); NotifFrame:Destroy()
        end
    end)
end

local KeyTitle = Instance.new("TextLabel", KeyMain)
KeyTitle.Size = UDim2.new(1, 0, 0, 50)
KeyTitle.Text = "SISTEMA DE KEY"
KeyTitle.TextColor3 = Color3.new(1,1,1)
KeyTitle.Font = Enum.Font.GothamBold; KeyTitle.TextSize = 18; KeyTitle.BackgroundTransparency = 1

local KeyInput = Instance.new("TextBox", KeyMain)
KeyInput.Size = UDim2.new(0, 280, 0, 45)
KeyInput.Position = UDim2.new(0.5, -140, 0.22, 0)
KeyInput.PlaceholderText = "Digite a Key aqui..."
KeyInput.Text = ""
KeyInput.BackgroundColor3 = Color3.fromRGB(45, 0, 80)
KeyInput.TextColor3 = Color3.new(1,1,1)
KeyInput.Font = Enum.Font.Gotham; KeyInput.TextSize = 14
Instance.new("UICorner", KeyInput)

local InputStroke = Instance.new("UIStroke", KeyInput)
InputStroke.Color = Color3.fromRGB(80, 0, 150)
InputStroke.Thickness = 1.5

-- PROVEDOR ÚNICO DE KEY: LOOTLABS
local SelectedProvider = "LootLabs"
local ProviderLabel = Instance.new("TextLabel", KeyMain)
ProviderLabel.Size = UDim2.new(1, -20, 0, 30)
ProviderLabel.Position = UDim2.new(0, 10, 0.48, 0)
ProviderLabel.BackgroundTransparency = 1
ProviderLabel.Text = "PROVEDOR DE KEY: LOOTLABS"
ProviderLabel.TextColor3 = Color3.fromRGB(220, 200, 255)
ProviderLabel.Font = Enum.Font.GothamBold
ProviderLabel.TextSize = 13

-- BOTÃO VERIFICAR KEY
local CheckBtn = Instance.new("TextButton", KeyMain)
CheckBtn.Size = UDim2.new(0, 145, 0, 40)
CheckBtn.Position = UDim2.new(0, 15, 0.75, 0)
CheckBtn.Text = "VERIFICAR KEY"
CheckBtn.BackgroundColor3 = Color3.fromRGB(110, 0, 190)
CheckBtn.TextColor3 = Color3.new(1,1,1); CheckBtn.Font = Enum.Font.GothamBold; CheckBtn.TextSize = 12
Instance.new("UICorner", CheckBtn)

-- BOTÃO PEGAR KEY
GetKeyBtn = Instance.new("TextButton", KeyMain)
GetKeyBtn.Size = UDim2.new(0, 145, 0, 40)
GetKeyBtn.Position = UDim2.new(0, 180, 0.75, 0)
GetKeyBtn.Text = "PEGAR LOOTLABS"
GetKeyBtn.BackgroundColor3 = Color3.fromRGB(60, 0, 110)
GetKeyBtn.TextColor3 = Color3.new(1,1,1); GetKeyBtn.Font = Enum.Font.GothamBold; GetKeyBtn.TextSize = 12
Instance.new("UICorner", GetKeyBtn)

-- LINK ÚNICO DO LOOTLABS
local ProviderUrls = {
    ["LootLabs"] = "https://dash.pandauth.com/getkey/scriptland?hwid=testing76898363",
}

GetKeyBtn.Text = "PEGAR LOOTLABS"

GetKeyBtn.MouseButton1Click:Connect(function()
    local keyUrl = ProviderUrls[SelectedProvider]
    if type(setclipboard) == "function" then
        local ok = pcall(function() setclipboard(keyUrl) end)
        if ok then
            CustomNotify("LINK COPIADO", "Cole no navegador para pegar sua key.", false)
        else
            CustomNotify("LINK PARA PEGAR KEY", keyUrl, false)
        end
    else
        CustomNotify("LINK PARA PEGAR KEY", keyUrl, false)
    end
end)

CheckBtn.MouseButton1Click:Connect(function()
    local enteredKey = tostring(KeyInput.Text or ""):gsub("^%s+", ""):gsub("%s+$", "")
    if enteredKey == "" then
        CustomNotify("ERRO", "Digite sua key primeiro.", true)
        return
    end

    CheckBtn.Active = false
    CheckBtn.Text = "VERIFICANDO..."

    if not PUSL or type(PUSL.validate) ~= "function" then
        CheckBtn.Active = true
        CheckBtn.Text = "VERIFICAR KEY"
        CustomNotify("ERRO", "A biblioteca Panda Auth V4 não carregou neste executor.", true)
        return
    end

    local ok, result = pcall(function()
        return PUSL.validate(enteredKey)
    end)

    CheckBtn.Active = true
    CheckBtn.Text = "VERIFICAR KEY"

    if not ok or type(result) ~= "table" then
        CustomNotify("ERRO", "Não foi possível verificar a key no Panda Auth V4.", true)
        return
    end

    if result.success == true then
        local successColor = Color3.fromRGB(50, 255, 50)
        CustomNotify("KEY VERIFICADA", "Acesso concedido!", false, successColor)
        task.wait(1.5)
        KeyGui:Destroy()
        IniciarHubOriginal()
    else
        local keyUrl = nil
        pcall(function()
            keyUrl = PUSL.getKeyUrl()
        end)
        if keyUrl and tostring(keyUrl) ~= "" then
            CustomNotify("KEY INVÁLIDA", "Pegue uma key válida. Link: " .. tostring(keyUrl), true)
        else
            CustomNotify("KEY INVÁLIDA", "Entre no Discord e pegue uma key válida.", true)
        end
        KeyInput.Text = ""
    end
end)
