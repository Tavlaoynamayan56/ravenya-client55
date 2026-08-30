-- RVY Client - Geliştirici Test Paneli (Roblox Studio İçin)
local oyuncu = game.Players.LocalPlayer
local runService = game:GetService("RunService")

-- 1. ARAYÜZ (GUI) OLUŞTURMA
local screenGui = Instance.new("ScreenGui")
screenGui.Name = "RVYClientUI"
screenGui.Parent = oyuncu:WaitForChild("PlayerGui")
screenGui.ResetOnSpawn = false

local anaCerceve = Instance.new("Frame")
anaCerceve.Size = UDim2.new(0, 200, 0, 250)
anaCerceve.Position = UDim2.new(0, 20, 0, 20)
anaCerceve.BackgroundColor3 = Color3.fromRGB(75, 0, 130) -- Koyu Mor Tema
anaCerceve.BorderSizePixel = 2
anaCerceve.Parent = screenGui

local baslik = Instance.new("TextLabel")
baslik.Size = UDim2.new(1, 0, 0, 40)
baslik.BackgroundColor3 = Color3.fromRGB(48, 0, 84)
baslik.TextColor3 = Color3.new(1, 1, 1)
baslik.Text = "RVY Client"
baslik.Font = Enum.Font.GothamBold
baslik.TextSize = 18
baslik.Parent = anaCerceve

-- Buton Oluşturma Fonksiyonu
local function butonOlustur(isim, yPozisyonu)
    local btn = Instance.new("TextButton")
    btn.Size = UDim2.new(0.9, 0, 0, 35)
    btn.Position = UDim2.new(0.05, 0, 0, yPozisyonu)
    btn.BackgroundColor3 = Color3.fromRGB(105, 0, 180)
    btn.TextColor3 = Color3.new(1, 1, 1)
    btn.Text = isim
    btn.Font = Enum.Font.Gotham
    btn.TextSize = 14
    btn.Parent = anaCerceve
    return btn
end

local btnHiz = butonOlustur("Hız (Speed)", 50)
local btnIsinlan = butonOlustur("Sandığa Işınlan", 95)
local btnNoclip = butonOlustur("Noclip (Aç/Kapat)", 140)
local btnUcus = butonOlustur("Zıplama Gücü (Yerçekimi)", 185)

-- 2. MEKANİKLER VE İŞLEVLER

-- Hız Artırma
btnHiz.MouseButton1Click:Connect(function()
    local karakter = oyuncu.Character
    if karakter and karakter:FindFirstChild("Humanoid") then
        karakter.Humanoid.WalkSpeed = 100
        print("Hız artırıldı!")
    end
end)

-- Sandığa Işınlanma (Workspace'te "HedefSandik" adında bir Part olmalı)
btnIsinlan.MouseButton1Click:Connect(function()
    local karakter = oyuncu.Character
    local sandik = workspace:FindFirstChild("HedefSandik") 
    
    if karakter and karakter:FindFirstChild("HumanoidRootPart") then
        if sandik then
            karakter.HumanoidRootPart.CFrame = sandik.CFrame + Vector3.new(0, 5, 0) -- Sandığın biraz üstüne ışınlar
        else
            warn("Haritada 'HedefSandik' adında bir obje bulunamadı!")
        end
    end
end)

-- Noclip (Duvarlardan Geçme)
local noclipAktif = false
local noclipBaglantisi = nil

btnNoclip.MouseButton1Click:Connect(function()
    noclipAktif = not noclipAktif
    local karakter = oyuncu.Character
    
    if noclipAktif then
        btnNoclip.BackgroundColor3 = Color3.fromRGB(0, 200, 0) -- Açıkken yeşil yap
        -- Karakterin parçalarının çarpışmasını sürekli kapatmak için döngü
        noclipBaglantisi = runService.Stepped:Connect(function()
            if karakter then
                for _, parca in pairs(karakter:GetDescendants()) do
                    if parca:IsA("BasePart") and parca.CanCollide == true then
                        parca.CanCollide = false
                    end
                end
            end
        end)
    else
        btnNoclip.BackgroundColor3 = Color3.fromRGB(105, 0, 180) -- Kapalıysa mor yap
        if noclipBaglantisi then
            noclipBaglantisi:Disconnect()
            noclipBaglantisi = nil
        end
    end
end)

-- Uçma / Zıplama Modu (Gerçek uçma motoru uzundur, burada yerçekimi/zıplama hilesi kullanıyoruz)
local ucusAktif = false
btnUcus.MouseButton1Click:Connect(function()
    ucusAktif = not ucusAktif
    local karakter = oyuncu.Character
    if karakter and karakter:FindFirstChild("Humanoid") then
        if ucusAktif then
            workspace.Gravity = 50 -- Yerçekimini azalt (Normali 196.2)
            karakter.Humanoid.JumpPower = 100
            btnUcus.BackgroundColor3 = Color3.fromRGB(0, 200, 0)
        else
            workspace.Gravity = 196.2
            karakter.Humanoid.JumpPower = 50
            btnUcus.BackgroundColor3 = Color3.fromRGB(105, 0, 180)
        end
    end
end)
