local Window = Rayfield:CreateWindow({
    Name = "Anime Vanguards Hub",
    LoadingTitle = "Anime Vanguards Hub",
    LoadingSubtitle = "By YHateMonkeez",
    ConfigurationSaving = {
        Enabled = true,
        FolderName = nil, -- Leave nil if you don't want to save
        FileName = "AV Hub"
    },
    Discord = {
        Enabled = false,
        Invite = "noinvitelink", -- Discord invite code
        RememberJoins = true
    },
    KeySystem = false
})
 
--// Create Tabs
local MainTab = Window:CreateTab("Main", 4483362458) -- Tab with an icon
 
--// Initialize rollback selection
local SelectedRollback = "Both" -- Default selection
 
--// Rollback Selection Dropdown
local RollbackDropdown = MainTab:CreateDropdown({
    Name = "Select Rollback Type",
    Options = {"Trait Rerolls", "Gems", "Both"},
    CurrentOption = "Both",
    Flag = "RollbackSelection",
    Callback = function(Selected)
        if Selected then
            SelectedRollback = Selected
            print("Selected rollback: " .. SelectedRollback)
        else
            print("Error: No rollback option selected!")
        end
    end
})
 
--// Rollback Toggle
local isRollbackActive = false
 
local RollbackToggle = MainTab:CreateToggle({
    Name = "Enable Rollback",
    CurrentValue = false,
    Flag = "RollbackToggle",
    Callback = function(Value)
        isRollbackActive = Value
 
        if isRollbackActive then
            local leaderstats = game.Players.LocalPlayer:FindFirstChild("leaderstats")
            if leaderstats then
                -- Rollback Trait Rerolls
                if SelectedRollback == "Trait Rerolls" or SelectedRollback == "Both" then
                    local traitRerolls = leaderstats:FindFirstChild("Trait Rerolls")
                    if traitRerolls then
                        traitRerolls.Value = 0
                        print("Trait Rerolls reset!")
                    else
                        print("Error: 'Trait Rerolls' stat not found!")
                    end
                end
 
                -- Rollback Gems
                if SelectedRollback == "Gems" or SelectedRollback == "Both" then
                    local gems = leaderstats:FindFirstChild("Gems")
                    if gems then
                        gems.Value = 0
                        print("Gems reset!")
                    else
                        print("Error: 'Gems' stat not found!")
                    end
                end
            else
                print("Error: leaderstats not found!")
            end
 
            print("Rollback Activated")
        else
            print("Rollback Deactivated")
        end
    end
})
 
 
 
 
--// Rejoin Button
local RejoinButton = MainTab:CreateButton({
    Name = "Rejoin Server",
    Callback = function()
        game:GetService("TeleportService"):Teleport(game.PlaceId, game.Players.LocalPlayer)
    end
})
 
print("Rayfield UI Loaded Successfully")
