-- Time Bomb 👑 Script
-- Developer: كاسبر الشمري

local Players = game:GetService("Players")
local LocalPlayer = Players.LocalPlayer
local PlayerGui = LocalPlayer:WaitForChild("PlayerGui")
local RunService = game:GetService("RunService")

-- إزالة أي واجهة قديمة لنفس السكربت لتجنب التكرار
if PlayerGui:FindFirstChild("TimeBombGUI") then
    PlayerGui.TimeBombGUI:Destroy()
end

local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "TimeBombGUI"
ScreenGui.ResetOnSpawn = false
ScreenGui.Parent = PlayerGui

-- النافذة الرئيسية باللون الأسود
local MainFrame = Instance.new("Frame")
MainFrame.Name = "MainFrame"
MainFrame.Size = UDim2.new(0, 320, 0, 420)
MainFrame.Position = UDim2.new(0.5, -160, 0.5, -210)
MainFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
MainFrame.BorderSizePixel = 0
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Parent = ScreenGui

local UICorner = Instance.new("UICorner")
UICorner.CornerRadius = UDim.new(0, 12)
UICorner.Parent = MainFrame

-- اسم السكربت (فوق على اليسار)
local TitleLabel = Instance.new("TextLabel")
TitleLabel.Size = UDim2.new(0, 180, 0, 35)
TitleLabel.Position = UDim2.new(0, 15, 0, 12)
TitleLabel.BackgroundTransparency = 1
TitleLabel.Text = "Time Bomb 👑"
TitleLabel.TextColor3 = Color3.fromRGB(255, 255, 255)
TitleLabel.TextSize = 20
TitleLabel.Font = Enum.Font.GothamBold
TitleLabel.TextXAlignment = Enum.TextXAlignment.Left
TitleLabel.Parent = MainFrame

-- اسم المطور (تحت اسم السكربت بشوي باللون الأحمر - سيختفي عند التصغير)
local DevLabel = Instance.new("TextLabel")
DevLabel.Size = UDim2.new(0, 200, 0, 30)
DevLabel.Position = UDim2.new(0, 15, 0, 48)
DevLabel.BackgroundTransparency = 1
DevLabel.Text = "المطور : كاسبر الشمري"
DevLabel.TextColor3 = Color3.fromRGB(220, 40, 40)
DevLabel.TextSize = 14
DevLabel.Font = Enum.Font.GothamBold
DevLabel.TextXAlignment = Enum.TextXAlignment.Left
DevLabel.Parent = MainFrame

-- أزرار التحكم (فوق على اليمين: تصغير '-' ، قفل '🔒' ، سلة مهملات '🗑️')
local isLocked = false

-- زر القمامة (حذف السكربت)
local TrashBtn = Instance.new("TextButton")
TrashBtn.Size = UDim2.new(0, 30, 0, 30)
TrashBtn.Position = UDim2.new(1, -35, 0, 15)
TrashBtn.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
TrashBtn.Text = "🗑️"
TrashBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
TrashBtn.TextSize = 14
TrashBtn.Parent = MainFrame
Instance.new("UICorner", TrashBtn).CornerRadius = UDim.new(0, 6)

TrashBtn.MouseButton1Click:Connect(function()
    ScreenGui:Destroy()
end)

-- قفل تثبيت الواجهة الرئيسية
local LockBtn = Instance.new("TextButton")
LockBtn.Size = UDim2.new(0, 30, 0, 30)
LockBtn.Position = UDim2.new(1, -70, 0, 15)
LockBtn.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
LockBtn.Text = "🔒"
LockBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
LockBtn.TextSize = 14
LockBtn.Parent = MainFrame
Instance.new("UICorner", LockBtn).CornerRadius = UDim.new(0, 6)

LockBtn.MouseButton1Click:Connect(function()
    isLocked = not isLocked
    MainFrame.Draggable = not isLocked
    LockBtn.BackgroundColor3 = isLocked and Color3.fromRGB(180, 40, 40) or Color3.fromRGB(40, 40, 40)
end)

-- زر تصغير الشاشة '-'
local MinimizeBtn = Instance.new("TextButton")
MinimizeBtn.Size = UDim2.new(0, 30, 0, 30)
MinimizeBtn.Position = UDim2.new(1, -105, 0, 15)
MinimizeBtn.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
MinimizeBtn.Text = "-"
MinimizeBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
MinimizeBtn.TextSize = 18
MinimizeBtn.Font = Enum.Font.GothamBold
MinimizeBtn.Parent = MainFrame
Instance.new("UICorner", MinimizeBtn).CornerRadius = UDim.new(0, 6)

local minimized = false
MinimizeBtn.MouseButton1Click:Connect(function()
    minimized = not minimized
    for _, child in ipairs(MainFrame:GetChildren()) do
        if child ~= TitleLabel and child ~= MinimizeBtn and child ~= TrashBtn and child ~= LockBtn and child.ClassName ~= "UICorner" then
            child.Visible = not minimized
        end
    end
    MainFrame.Size = minimized and UDim2.new(0, 320, 0, 55) or UDim2.new(0, 320, 0, 420)
end)

-- متغيرات لمنع التكرار السريع
local korbloxBusy = false
local headlessBusy = false

-- زر كوربلوكس : رجل مقطوعه
local KorbloxBtn = Instance.new("TextButton")
KorbloxBtn.Size = UDim2.new(1, -30, 0, 45)
KorbloxBtn.Position = UDim2.new(0, 15, 0, 95)
KorbloxBtn.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
KorbloxBtn.Text = "Korblox : رجل مقطوعه"
KorbloxBtn.TextColor3 = Color3.fromRGB(0, 0, 0)
KorbloxBtn.TextSize = 15
KorbloxBtn.Font = Enum.Font.GothamBold
KorbloxBtn.Parent = MainFrame
Instance.new("UICorner", KorbloxBtn).CornerRadius = UDim.new(0, 8)

KorbloxBtn.MouseButton1Click:Connect(function()
    if korbloxBusy then return end
    korbloxBusy = true
    KorbloxBtn.Text = "خلاص اشتغل ✅"
    pcall(function()
        loadstring(game:HttpGet("https://scriptblox.com/raw/Universal-Script-Korblox-All-145374"))()
    end)
    task.wait(2)
    KorbloxBtn.Text = "Korblox : رجل مقطوعه"
    korbloxBusy = false
end)

-- زر Headless : راس مخفي
local HeadlessBtn = Instance.new("TextButton")
HeadlessBtn.Size = UDim2.new(1, -30, 0, 45)
HeadlessBtn.Position = UDim2.new(0, 15, 0, 150)
HeadlessBtn.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
HeadlessBtn.Text = "Headless : راس مخفي"
HeadlessBtn.TextColor3 = Color3.fromRGB(0, 0, 0)
HeadlessBtn.TextSize = 15
HeadlessBtn.Font = Enum.Font.GothamBold
HeadlessBtn.Parent = MainFrame
Instance.new("UICorner", HeadlessBtn).CornerRadius = UDim.new(0, 8)

HeadlessBtn.MouseButton1Click:Connect(function()
    if headlessBusy then return end
    headlessBusy = true
    HeadlessBtn.Text = "خلاص اشتغل ✅"
    pcall(function()
        loadstring(game:HttpGet("https://scriptblox.com/raw/Universal-Script-Headless-(R6R15)-224493"))()
    end)
    task.wait(2)
    HeadlessBtn.Text = "Headless : راس مخفي"
    headlessBusy = false
end)

-- زر Auto 💣 في القائمة الرئيسية
local AutoMainBtn = Instance.new("TextButton")
AutoMainBtn.Size = UDim2.new(1, -30, 0, 45)
AutoMainBtn.Position = UDim2.new(0, 15, 0, 205)
AutoMainBtn.BackgroundColor3 = Color3.fromRGB(255, 255, 255)
AutoMainBtn.Text = "Auto 💣"
AutoMainBtn.TextColor3 = Color3.fromRGB(0, 0, 0)
AutoMainBtn.TextSize = 15
AutoMainBtn.Font = Enum.Font.GothamBold
AutoMainBtn.Parent = MainFrame
Instance.new("UICorner", AutoMainBtn).CornerRadius = UDim.new(0, 8)

-- القائمة الجديدة (بدون اسم نهائياً، بجانب الثلاث شرطات عند علامة روبلوكس، تحتها ببارين)
local SubAutoFrame = Instance.new("Frame")
SubAutoFrame.Name = "SubAutoFrame"
SubAutoFrame.Size = UDim2.new(0, 220, 0, 80)
SubAutoFrame.Position = UDim2.new(0, 10, 0, 65)
SubAutoFrame.BackgroundColor3 = Color3.fromRGB(20, 20, 20)
SubAutoFrame.BorderSizePixel = 0
SubAutoFrame.Visible = false
SubAutoFrame.Active = true
SubAutoFrame.Draggable = true
SubAutoFrame.Parent = ScreenGui
Instance.new("UICorner", SubAutoFrame).CornerRadius = UDim.new(0, 8)

-- زر قفل القائمة الجديدة (فوق على اليمين - مفتوح 🔓 أو مسمر 🔒)
local subIsLocked = false
local SubLockBtn = Instance.new("TextButton")
SubLockBtn.Size = UDim2.new(0, 25, 0, 25)
SubLockBtn.Position = UDim2.new(1, -30, 0, 8)
SubLockBtn.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
SubLockBtn.Text = "🔓"
SubLockBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
SubLockBtn.TextSize = 12
SubLockBtn.Parent = SubAutoFrame
Instance.new("UICorner", SubLockBtn).CornerRadius = UDim.new(0, 6)

SubLockBtn.MouseButton1Click:Connect(function()
    subIsLocked = not subIsLocked
    SubAutoFrame.Draggable = not subIsLocked
    if subIsLocked then
        SubLockBtn.Text = "🔒"
        SubLockBtn.BackgroundColor3 = Color3.fromRGB(180, 40, 40)
    else
        SubLockBtn.Text = "🔓"
        SubLockBtn.BackgroundColor3 = Color3.fromRGB(40, 40, 40)
    end
end)

-- زر Auto Bomb داخل القائمة الجديدة
local autoBombActive = false
local AutoBombBtn = Instance.new("TextButton")
AutoBombBtn.Size = UDim2.new(1, -45, 0, 40)
AutoBombBtn.Position = UDim2.new(0, 10, 0, 30)
AutoBombBtn.BackgroundColor3 = Color3.fromRGB(180, 30, 30)
AutoBombBtn.Text = "Auto Bomb : Off"
AutoBombBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
AutoBombBtn.TextSize = 14
AutoBombBtn.Font = Enum.Font.GothamBold
AutoBombBtn.Parent = SubAutoFrame
Instance.new("UICorner", AutoBombBtn).CornerRadius = UDim.new(0, 6)

AutoBombBtn.MouseButton1Click:Connect(function()
    autoBombActive = not autoBombActive
    if autoBombActive then
        AutoBombBtn.BackgroundColor3 = Color3.fromRGB(40, 180, 40)
        AutoBombBtn.Text = "Auto Bomb : On"
    else
        AutoBombBtn.BackgroundColor3 = Color3.fromRGB(180, 30, 30)
        AutoBombBtn.Text = "Auto Bomb : Off"
    end
end)

-- إظهار/إخفاء القائمة الجديدة عند الضغط على زر Auto ْم الرئيسي
AutoMainBtn.MouseButton1Click:Connect(function()
    SubAutoFrame.Visible = not SubAutoFrame.Visible
end)

-- نظام الأوتو بومب الذكي (استهداف أقرب خصم فقط وبشرط وجود القنبلة معك)
RunService.RenderStepped:Connect(function()
    if not autoBombActive then return end
    
    local character = LocalPlayer.Character
    if not character or not character:FindFirstChild("HumanoidRootPart") then return end
    
    -- شرط أساسي: التأكد أن القنبلة معك (في اليد أو الحقيبة)
    local backpack = LocalPlayer:FindFirstChild("Backpack")
    local hasBomb = (character:FindFirstChild("TimeBomb") or character:FindFirstChild("Bomb") or 
                     (backpack and (backpack:FindFirstChild("TimeBomb") or backpack:FindFirstChild("Bomb"))))
    
    if not hasBomb then return end
    
    local closestEnemy = nil
    local shortestDistance = math.huge
    local myPos = character.HumanoidRootPart.Position
    
    -- البحث عن أقرب خصم ضمن الشروط الصارمة
    for _, player in ipairs(Players:GetPlayers()) do
        if player ~= LocalPlayer and player.Character and player.Character:FindFirstChild("HumanoidRootPart") then
            -- استبعاد أفراد فريقك
            local sameTeam = false
            if LocalPlayer.Team and player.Team and LocalPlayer.Team == player.Team then
                sameTeam = true
            end
            
            if not sameTeam then
                local hrp = player.Character.HumanoidRootPart
                -- التحقق أن الخصم داخل حدود الخريطة/القيم الطبيعية
                if math.abs(hrp.Position.X) < 1500 and math.abs(hrp.Position.Z) < 1500 then
                    local distance = (hrp.Position - myPos).Magnitude
                    if distance < shortestDistance then
                        shortestDistance = distance
                        closestEnemy = hrp
                    end
                end
            end
        end
    end
    
    -- التوجه نحو أقرب خصم تم العثور عليه
    if closestEnemy then
        character.HumanoidRootPart.CFrame = closestEnemy.CFrame
    end
end)