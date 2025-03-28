-- إنشاء الواجهة الرئيسية
local screenGui = Instance.new("ScreenGui")
screenGui.Parent = game.Players.LocalPlayer:WaitForChild("PlayerGui")
screenGui.ResetOnSpawn = false

-- إنشاء الإطار الرئيسي
local mainFrame = Instance.new("Frame")
mainFrame.Size = UDim2.new(0, 490, 0, 300) -- حجم الواجهة
mainFrame.Position = UDim2.new(0.5, -200, 0.5, -150) -- توسيط الواجهة
mainFrame.BackgroundColor3 = Color3.new(0.2, 0.2, 0.2)
mainFrame.Parent = screenGui

local mainCorner = Instance.new("UICorner")
mainCorner.CornerRadius = UDim.new(0.1, 0)
mainCorner.Parent = mainFrame

-- شريط العنوان
local topBar = Instance.new("Frame")
topBar.Size = UDim2.new(1, 0, 0, 30)
topBar.Position = UDim2.new(0, 0, 0, 0)
topBar.BackgroundColor3 = Color3.new(0.1, 0.1, 0.1)
topBar.Parent = mainFrame

-- عنوان ثابت "1st"
local titleLabel = Instance.new("TextLabel")
titleLabel.Size = UDim2.new(0, 100, 0, 20)
titleLabel.Position = UDim2.new(0.5, -50, 0.5, -10)
titleLabel.Text = "1ST"
titleLabel.TextColor3 = Color3.new(1, 1, 1)
titleLabel.BackgroundTransparency = 1
titleLabel.Font = Enum.Font.SourceSansBold
titleLabel.TextSize = 18
titleLabel.Parent = topBar

-- زر التقليل (الناقص)
local minimizeButton = Instance.new("TextButton")
minimizeButton.Size = UDim2.new(0, 20, 0, 20) -- حجم أصغر
minimizeButton.Position = UDim2.new(1, -60, 0.5, -10)
minimizeButton.Text = "-"
minimizeButton.BackgroundColor3 = Color3.new(0.4, 0.4, 0.4)
minimizeButton.TextColor3 = Color3.new(1, 1, 1)
minimizeButton.Font = Enum.Font.SourceSansBold
minimizeButton.TextSize = 18
minimizeButton.Parent = topBar

-- زر الإغلاق
local closeButton = Instance.new("TextButton")
closeButton.Size = UDim2.new(0, 20, 0, 20) -- حجم أصغر
closeButton.Position = UDim2.new(1, -30, 0.5, -10)
closeButton.Text = "X"
closeButton.BackgroundColor3 = Color3.new(0.4, 0.4, 0.4)
closeButton.TextColor3 = Color3.new(1, 1, 1)
closeButton.Font = Enum.Font.SourceSansBold
closeButton.TextSize = 18
closeButton.Parent = topBar

-- زوايا الأزرار
local corner1 = Instance.new("UICorner")
corner1.CornerRadius = UDim.new(0.2, 0)
corner1.Parent = closeButton
local corner2 = Instance.new("UICorner")
corner2.CornerRadius = UDim.new(0.2, 0)
corner2.Parent = minimizeButton

-- الإطارات الداخلية
local leftFrame = Instance.new("Frame")
leftFrame.Size = UDim2.new(0, 100, 1, -30)
leftFrame.Position = UDim2.new(0, 0, 0, 30)
leftFrame.BackgroundColor3 = Color3.new(0.3, 0.3, 0.3)
leftFrame.Parent = mainFrame

local rightFrame = Instance.new("Frame")
rightFrame.Size = UDim2.new(1, -100, 1, -30)
rightFrame.Position = UDim2.new(0, 100, 0, 30)
rightFrame.BackgroundColor3 = Color3.new(0.1, 0.1, 0.1)
rightFrame.Parent = mainFrame

-- أزرار القائمة الرئيسية (مع أزرار جديدة وأحجام أصغر)
local buttons = {
    {Text = "ترحيب", Position = UDim2.new(0, 10, 0, 10)},
    {Text = "الشات", Position = UDim2.new(0, 10, 0, 45)},
    {Text = "تخريب", Position = UDim2.new(0, 10, 0, 80)},
    {Text = "ضحيه", Position = UDim2.new(0, 10, 0, 115)}, -- الزر الجديد
    {Text = "مضادات", Position = UDim2.new(0, 10, 0, 150)}, -- الزر الجديد
    {Text = "تخريب الماب", Position = UDim2.new(0, 10, 0, 185)},
    {Text = "رقصات", Position = UDim2.new(0, 10, 0, 220)}
}

for i, buttonInfo in ipairs(buttons) do
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0.8, 0, 0, 25) -- حجم أصغر للزر
    button.Position = buttonInfo.Position
    button.Text = buttonInfo.Text
    button.BackgroundColor3 = Color3.fromRGB(255, 215, 0)
    button.TextColor3 = Color3.new(0, 0, 0)
    button.Font = Enum.Font.SourceSansBold
    button.TextSize = 12 -- حجم نص أصغر
    button.Parent = leftFrame

    -- زوايا الأزرار
    local buttonCorner = Instance.new("UICorner")
    buttonCorner.CornerRadius = UDim.new(0.2, 0)
    buttonCorner.Parent = button

    -- حدث النقر على الزر
    button.MouseButton1Click:Connect(function()
        showPage(buttonInfo.Text) -- إظهار الصفحة المحددة
    end)
end

-- إنشاء الصفحات
local pages = {}

local function showPage(pageName)
    for name, page in pairs(pages) do
        page.Visible = (name == pageName) -- إظهار الصفحة المحددة وإخفاء البقية
    end
end

-- صفحة الترحيب
local welcomePage = Instance.new("Frame")
welcomePage.Size = UDim2.new(1, 0, 1, 0)
welcomePage.Position = UDim2.new(0, 0, 0, 0)
welcomePage.BackgroundColor3 = Color3.fromRGB(0, 0, 0)
welcomePage.Visible = false
welcomePage.Parent = rightFrame

-- استيراد TweenService
local TweenService = game:GetService("TweenService")

-- إضافة صورة اللاعب
local profilePicture = Instance.new("ImageLabel")
profilePicture.Size = UDim2.new(0, 120, 0, 120)
profilePicture.Position = UDim2.new(1, 0, 0.01, 0) -- وضع الصورة خارج الشاشة إلى اليمين
profilePicture.Image = "https://www.roblox.com/headshot-thumbnail/image?userId=" .. game.Players.LocalPlayer.UserId .. "&width=420&height=420&format=png"
profilePicture.BackgroundColor3 = Color3.new(0, 0, 0)
profilePicture.BorderSizePixel = 0
profilePicture.Parent = welcomePage

-- جعل الصورة دائرية
local profileCorner = Instance.new("UICorner")
profileCorner.CornerRadius = UDim.new(1, 0)
profileCorner.Parent = profilePicture

-- تحريك الصورة لتأتي من اليمين
local profileTweenInfo = TweenInfo.new(1, Enum.EasingStyle.Bounce, Enum.EasingDirection.Out)
local profileTargetPosition = UDim2.new(0.5, -60, 0.01, 0)
local profileTween = TweenService:Create(profilePicture, profileTweenInfo, { Position = profileTargetPosition })
profileTween:Play()

-- إضافة رسالة ترحيب
local welcomeLabel = Instance.new("TextLabel")
welcomeLabel.Size = UDim2.new(0, 300, 0, 50) -- حجم النص
welcomeLabel.Position = UDim2.new(0.5, -150, 0.4, 0) -- موقعه
welcomeLabel.Text = "مرحبًا بك، " .. game.Players.LocalPlayer.Name .. "!" -- نص الترحيب
welcomeLabel.TextColor3 = Color3.new(1, 1, 1) -- لون النص
welcomeLabel.BackgroundTransparency = 1 -- شفافية الخلفية
welcomeLabel.Font = Enum.Font.SourceSansBold -- نوع الخط
welcomeLabel.TextSize = 24 -- حجم النص
welcomeLabel.Parent = welcomePage

-- إضافة زر نسخ رابط الديسكورد
local discordButton = Instance.new("TextButton")
discordButton.Size = UDim2.new(0, 200, 0, 40)
discordButton.Position = UDim2.new(1, 0, 0.6, 0) -- وضع الزر خارج الشاشة إلى اليمين
discordButton.Text = "نسخ رابط الديسكورد"
discordButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0)
discordButton.TextColor3 = Color3.new(0, 0, 0)
discordButton.Font = Enum.Font.SourceSansBold
discordButton.TextSize = 18
discordButton.Parent = welcomePage

-- إضافة تأثير اللمعة
local gradient = Instance.new("UIGradient")
gradient.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, Color3.fromRGB(223, 1, 0)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(0, 0, 0))
}
gradient.Parent = discordButton

-- إضافة زوايا مستديرة للزر
local buttonCorner = Instance.new("UICorner")
buttonCorner.CornerRadius = UDim.new(0.2, 0)
buttonCorner.Parent = discordButton

-- تحريك الزر ليأتي من اليمين
local buttonTweenInfo = TweenInfo.new(1, Enum.EasingStyle.Quad, Enum.EasingDirection.Out)
local buttonTargetPosition = UDim2.new(0.5, -100, 0.6, 0)
local buttonTween = TweenService:Create(discordButton, buttonTweenInfo, { Position = buttonTargetPosition })
buttonTween:Play()

-- وظيفة نسخ رابط الديسكورد
discordButton.MouseButton1Click:Connect(function()
    setclipboard("https://discord.gg/NBeFthgA2G")  
    discordButton.Text = "تم النسخ!"
    wait(1)
    discordButton.Text = "نسخ رابط الديسكورد"
end)

-- إضافة ملاحظة
local noteLabel = Instance.new("TextLabel")
noteLabel.Size = UDim2.new(0, 300, 0, 50)
noteLabel.Position = UDim2.new(0.5, -150, 0.8, 0)
noteLabel.Text = "أي اقتراح لكم؟ اكتبوه لنا في سيرفر الديسكورد!"
noteLabel.TextColor3 = Color3.new(1, 1, 1)
noteLabel.BackgroundTransparency = 1
noteLabel.Font = Enum.Font.SourceSans
noteLabel.TextSize = 16
noteLabel.Parent = welcomePage

-- إضافة ملاحظة
local copyrightLabel = Instance.new("TextLabel")
copyrightLabel.Size = UDim2.new(0, 300, 0, 10)
copyrightLabel.Position = UDim2.new(0.5, -150, 0.77, 0)
copyrightLabel.Text = "جميع الحقوق محفوظه في سيرفر الدسكورد"
copyrightLabel.TextColor3 = Color3.new(1, 1, 1)
copyrightLabel.BackgroundTransparency = 1
copyrightLabel.Font = Enum.Font.SourceSans
copyrightLabel.TextSize = 16
copyrightLabel.Parent = welcomePage

-- إضافة الصفحة إلى جدول الصفحات
pages["ترحيب"] = welcomePage

-- وظيفة التقليل
local isMinimized = false
local originalSize = mainFrame.Size
local minimizedSize = UDim2.new(0, 490, 0, 30)

minimizeButton.MouseButton1Click:Connect(function()
    isMinimized = not isMinimized
    if isMinimized then
        mainFrame.Size = minimizedSize
        leftFrame.Visible = false
        rightFrame.Visible = false
    else
        mainFrame.Size = originalSize
        leftFrame.Visible = true
        rightFrame.Visible = true
    end
end)

-- وظيفة الإغلاق
closeButton.MouseButton1Click:Connect(function()
    screenGui:Destroy()
end)

-- عرض صفحة الترحيب افتراضياً
showPage("ترحيب")

-- إنشاء صفحة الرقصات
local dancesPage = Instance.new("Frame")
dancesPage.Size = UDim2.new(1, 0, 1, 0)
dancesPage.Position = UDim2.new(0, 0, 0, 0)
dancesPage.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
dancesPage.Visible = false
dancesPage.Parent = rightFrame

-- إضافة ملاحظة
local noteLabel = Instance.new("TextLabel")
noteLabel.Size = UDim2.new(0.8, 0, 0.1, 0)
noteLabel.Position = UDim2.new(0.1, 0, 0.001, 0)
noteLabel.BackgroundTransparency = 1
noteLabel.Text = " رقصات لاغراض بروبكس (تظهر للاعبين)"
noteLabel.TextColor3 = Color3.new(1, 1, 1)
noteLabel.Font = Enum.Font.SourceSans
noteLabel.TextSize = 16
noteLabel.Parent = dancesPage

-- إضافة 3 أزرار للرقصات
local danceButtons = {
    {Text = "رقصت 1", Position = UDim2.new(0.1, 0, 0.13, 0), AnimationId = "rbxassetid://17381912171"},
    {Text = "رقصت 2", Position = UDim2.new(0.1, 0, 0.33, 0), AnimationId = "rbxassetid://18396187889"},
    {Text = "رقصت 3", Position = UDim2.new(0.1, 0, 0.53, 0), AnimationId = "rbxassetid://80909423274891", Duration = 2} -- إضافة مدة للرقصة الثالثة
}

for i, buttonInfo in ipairs(danceButtons) do
    local danceButton = Instance.new("TextButton")
    danceButton.Size = UDim2.new(0.8, 0, 0.1, 0)
    danceButton.Position = buttonInfo.Position
    danceButton.Text = buttonInfo.Text
    danceButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0)
    danceButton.TextColor3 = Color3.new(0, 0, 0)
    danceButton.Font = Enum.Font.SourceSansBold
    danceButton.TextSize = 18
    danceButton.Parent = dancesPage

    -- زوايا الأزرار
    local buttonCorner = Instance.new("UICorner")
    buttonCorner.CornerRadius = UDim.new(0.2, 0)
    buttonCorner.Parent = danceButton

    -- حدث النقر على الزر
    if buttonInfo.AnimationId then
        danceButton.MouseButton1Click:Connect(function()
            -- احصل على الشخصية
            local player = game.Players.LocalPlayer
            local character = player.Character or player.CharacterAdded:Wait()

            -- إعداد الحركة (Animation)
            local animation = Instance.new("Animation")
            animation.AnimationId = buttonInfo.AnimationId

            -- تحميل الحركة وتشغيلها
            local humanoid = character:WaitForChild("Humanoid")
            local animationTrack = humanoid:LoadAnimation(animation)

            -- تشغيل الحركة
            animationTrack:Play()

            -- إذا كانت الرقصة الثالثة، أوقفها بعد المدة المحددة
            if buttonInfo.Duration then
                wait(buttonInfo.Duration) -- انتظر المدة المحددة
                animationTrack:Stop() -- أوقف الرقصة
            end
        end)
    end
end

-- إضافة صفحة الرقصات إلى جدول الصفحات
pages["رقصات"] = dancesPage



-- صفحة الشات
local chatPage = Instance.new("Frame")
chatPage.Size = UDim2.new(1, 0, 1, 0)
chatPage.Position = UDim2.new(0, 0, 0, 0)
chatPage.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
chatPage.Visible = false
chatPage.Parent = rightFrame

-- إنشاء إطار المحتوى
local contentFrame = Instance.new("Frame")
contentFrame.Size = UDim2.new(1, 0, 1, 0)
contentFrame.Position = UDim2.new(0, 0, 0, 0)
contentFrame.BackgroundColor3 = Color3.fromRGB(30, 30, 30) -- خلفية غامقة
contentFrame.Parent = chatPage

-- إضافة حواف مستديرة لإطار المحتوى
local contentCorner = Instance.new("UICorner")
contentCorner.CornerRadius = UDim.new(0.05, 0)
contentCorner.Parent = contentFrame

-- مربع النص لإدخال الرسالة
local inputBox = Instance.new("TextBox")
inputBox.Size = UDim2.new(0.8, 0, 0.2, 0)
inputBox.Position = UDim2.new(0.1, 0, 0.1, 0)
inputBox.BackgroundColor3 = Color3.fromRGB(50, 50, 50) -- خلفية رمادية
inputBox.Text = "اكتب رسالتك هنا..."
inputBox.TextColor3 = Color3.new(1, 1, 1) -- لون النص أبيض
inputBox.Font = Enum.Font.SourceSansBold
inputBox.TextSize = 18
inputBox.ClearTextOnFocus = true
inputBox.Parent = contentFrame

local noteLabel = Instance.new("TextLabel")
noteLabel.Size = UDim2.new(0.8, 0, 0.1, 0)
noteLabel.Position = UDim2.new(0.1, 0, 0.001, 0)
noteLabel.BackgroundTransparency = 1
noteLabel.Text = "اقرا التعليمات قبل الستخدام ارسال رساله طويله"
noteLabel.TextColor3 = Color3.new(0, 0, 0)
noteLabel.Font = Enum.Font.SourceSans
noteLabel.TextSize = 16
noteLabel.Parent = contentFrame

-- إضافة حواف مستديرة لمربع النص
local inputCorner = Instance.new("UICorner")
inputCorner.CornerRadius = UDim.new(0.1, 0)
inputCorner.Parent = inputBox

-- إطار يحتوي على الأزرار في نفس السطر
local buttonFrame = Instance.new("Frame")
buttonFrame.Size = UDim2.new(0.8, 0, 0.1, 0)
buttonFrame.Position = UDim2.new(0.1, 0, 0.3, 0)
buttonFrame.BackgroundTransparency = 1 -- إطار شفاف
buttonFrame.Parent = contentFrame

-- زر الإرسال
local sendButton = Instance.new("TextButton")
sendButton.Size = UDim2.new(0.38, 0, 1, 0) -- تقليل الحجم لاستيعاب الزر الجديد
sendButton.Position = UDim2.new(0, 0, 0, 0)
sendButton.Text = "ارسال رساله طويله"
sendButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0) -- لون ذهبي
sendButton.TextColor3 = Color3.new(0, 0, 0) -- لون النص أسود
sendButton.Font = Enum.Font.SourceSansBold
sendButton.TextSize = 18
sendButton.Parent = buttonFrame

-- إضافة حواف مستديرة لزر الإرسال
local sendButtonCorner = Instance.new("UICorner")
sendButtonCorner.CornerRadius = UDim.new(0.1, 0)
sendButtonCorner.Parent = sendButton

-- زر الفلترة
local filterButton = Instance.new("TextButton")
filterButton.Size = UDim2.new(0.24, 0, 1, 0) -- حجم أصغر
filterButton.Position = UDim2.new(0.39, 0, 0, 0) -- بين الإرسال والسبام
filterButton.Text = "فلترة"
filterButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0) -- لون ذهبي
filterButton.TextColor3 = Color3.new(0, 0, 0) -- لون النص أسود
filterButton.Font = Enum.Font.SourceSansBold
filterButton.TextSize = 18
filterButton.Parent = buttonFrame

-- إضافة حواف مستديرة لزر الفلترة
local filterButtonCorner = Instance.new("UICorner")
filterButtonCorner.CornerRadius = UDim.new(0.1, 0)
filterButtonCorner.Parent = filterButton

-- زر السبام
local spamButton = Instance.new("TextButton")
spamButton.Size = UDim2.new(0.36, 0, 1, 0) -- تقليل الحجم لاستيعاب زر الفلترة
spamButton.Position = UDim2.new(0.64, 0, 0, 0) -- بجانب زر الفلترة
spamButton.Text = "سبام"
spamButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0) -- لون ذهبي
spamButton.TextColor3 = Color3.new(0, 0, 0) -- لون النص أسود
spamButton.Font = Enum.Font.SourceSansBold
spamButton.TextSize = 18
spamButton.Parent = buttonFrame

-- إضافة حواف مستديرة لزر السبام
local spamButtonCorner = Instance.new("UICorner")
spamButtonCorner.CornerRadius = UDim.new(0.1, 0)
spamButtonCorner.Parent = spamButton

-- زر إرسال ما يشفر
local encryptButton = Instance.new("TextButton")
encryptButton.Size = UDim2.new(1, 1, 1 , 1) -- نفس حجم زر الإرسال
encryptButton.Position = UDim2.new(0 ,1, 1, 1) -- بجانب زر السبام
encryptButton.Text = "80% إرسال ما يشفر"
encryptButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0) -- لون ذهبي
encryptButton.TextColor3 = Color3.new(0, 0, 0) -- لون النص أسود
encryptButton.Font = Enum.Font.SourceSansBold
encryptButton.TextSize = 18
encryptButton.Parent = buttonFrame

-- إضافة حواف مستديرة لزر إرسال ما يشفر
local encryptButtonCorner = Instance.new("UICorner")
encryptButtonCorner.CornerRadius = UDim.new(0.1, 0)
encryptButtonCorner.Parent = encryptButton

-- خدمة الدردشة
local TextChatService = game:GetService("TextChatService")
local ReplicatedStorage = game:GetService("ReplicatedStorage")

-- دالة إرسال الرسائل
local function chatMessage(str)
    str = tostring(str)
    if TextChatService.ChatVersion == Enum.ChatVersion.TextChatService then
        TextChatService.TextChannels.RBXGeneral:SendAsync(str)
    else
        ReplicatedStorage.DefaultChatSystemChatEvents.SayMessageRequest:FireServer(str, "All")
    end
end

-- دالة إرسال الرسالة الطويلة
local function sendLongMessage(customMessage)
    local blob = "\u{000D}"
    local longMessage = "㉿_1st_㉿ℭ§¹" .. blob
    for i = 1, 70 do
        longMessage = longMessage .. "" .. blob
    end
    longMessage = longMessage .. customMessage
    chatMessage(longMessage)
end

-- وظيفة زر الإرسال
sendButton.MouseButton1Click:Connect(function()
    sendLongMessage(inputBox.Text)
end)

-- وظيفة زر الفلترة
filterButton.MouseButton1Click:Connect(function()
    chatMessage("/E abc")
end)

-- وظيفة زر السبام
local isSpamming = false
local spamCoroutine
spamButton.MouseButton1Click:Connect(function()
    if isSpamming then
        isSpamming = false
        spamButton.Text = "سبام"
        if spamCoroutine then
            coroutine.close(spamCoroutine)
        end
    else
        isSpamming = true
        spamButton.Text = "إيقاف"
        spamCoroutine = coroutine.create(function()
            while isSpamming do
                sendLongMessage("1st")
                wait(3.5)
            end
        end)
        coroutine.resume(spamCoroutine)
    end
end)

-- وظيفة زر إرسال ما يشفر
local function ApplyCustomFormat(message)
    return "¹§ℭ㉿s㉿x㉿__" .. message:gsub("%s", "_") .. "__㉿s㉿x㉿ℭ§¹"
end

local function SafeSend(message)
    local success, err = pcall(function()
        if ReplicatedStorage:FindFirstChild("DefaultChatSystemChatEvents") then
            ReplicatedStorage.DefaultChatSystemChatEvents.SayMessageRequest:FireServer(message, "All")
        else
            TextChatService.TextChannels.RBXGeneral:SendAsync(message)
        end
    end)
    return success, err
end

encryptButton.MouseButton1Click:Connect(function()
    local rawMessage = inputBox.Text:gsub("^%s*(.-)%s*$", "%1")
    if rawMessage == "" then return end
    local formatted = ApplyCustomFormat(rawMessage)
    
    task.spawn(function()
        -- إرسال الرسالة الفعلية أولاً
        local success, err = SafeSend(formatted)
        if success then
            inputBox.Text = ""
            print("✅ تم الإرسال بنجاح:", formatted)
            -- بعد انتظار قصير، إرسال "/e ABC"
            task.wait(0.1)
            SafeSend("/e ABC")
        else
            warn("❌ فشل الإرسال:", err)
            inputBox.Text = rawMessage
        end
    end)
end)

pages["الشات"] = chatPage

-- إنشاء الإطار الرئيسي مع إمكانية التمرير
local sabotagePage = Instance.new("ScrollingFrame")
sabotagePage.Size = UDim2.new(1, 0, 1, 0)
sabotagePage.Position = UDim2.new(0, 0, 0, 0)
sabotagePage.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
sabotagePage.Visible = false
sabotagePage.CanvasSize = UDim2.new(0, 0, 2, 0) -- زيادة المساحة العمودية للتمرير
sabotagePage.ScrollBarThickness = 10
sabotagePage.Parent = rightFrame

-- إضافة حواف مستديرة للإطار
local contentCorner = Instance.new("UICorner")
contentCorner.CornerRadius = UDim.new(0.05, 0)
contentCorner.Parent = sabotagePage

-- جدول الألوان والكلمات لزر "كل شيء"
local allColors = {
    Color3.new(0.1, 0.1, 0.1), -- أسود داكن
    Color3.new(0.8, 0.7, 0.2), -- ذهبي
    Color3.new(0.75, 0.75, 0.75), -- فضي
    Color3.new(1, 0.27, 0), -- برتقالي ناري
    Color3.new(0.47, 0.53, 0.6), -- رمادي مائل للأزرق
    Color3.new(0.5, 0, 0), -- أحمر داكن
    Color3.new(0, 0.3, 0), -- أخضر داكن
    Color3.new(0, 0.5, 1) -- أزرق نيوي
}

local allWords = {
    "╭∩╮_( ︶︿︶)_╭∩╮",
    "لا مكان للضعفاء بيننا",
    "︻┻┳══━一∵∵",
    "انا الساطي", 
    "凸(｀0´)凸",
    "انا 1st",
    "︻デ═一∵.",
    "㉿ℭانا النازي",
    "凸(｀⌒´メ)凸",
    "انا عم النسيخه",
    "︻┳═一∵∵",
    "凸(^▼ｪ▼ﾒ^)",
    "من يواجهنا، يكتب نهايته",
    "︻┻┳═一∵",
    "حين أقف، العالم يُصغي",
    "╭∩╮(⋋‿⋌)ᕗ)",
    "أنت كالصفر... لا قيمة لك إلا بجانب غيرك",
    "︻デ═一∶∵",
    "لا تضيع وقتي، فحتى الساعة ترفض عدَّ دقائقك",
    "╭∩╮ʕ•ᴥ•ʔ╭∩╮",
    "``∵∵一┳═┻︻",
    "（︶︿︶_╭∩╮",
    "︻┻┳━ ·`.",
    "╭∩╮ʕ•ᴥ•ʔ╭∩╮_╭∩╮(ʕ•ᴥ•ʔ)╭∩╮",
    "╭∩╮_☯_☯_╭∩╮",
    "╭∩╮(-_-)╭∩╮"
}
-- متغير لتتبع حالة زر "كل شيء"
local isAllRunning = false

-- دالة لتغيير الألوان والكلمات
local function changeAllColorsAndWords()
    local colorIndex = 1
    local wordIndex = 1
    while isAllRunning do
        local selectedColor = allColors[colorIndex]
        local selectedWord = allWords[wordIndex]
        
        local args = {
            [1] = selectedWord,
            [2] = selectedColor
        }
        game:GetService("ReplicatedStorage").PrivateCommands.Title:FireServer(unpack(args))
        
        colorIndex = (colorIndex % #allColors) + 1
        wordIndex = (wordIndex % #allWords) + 1
        
        wait(1) -- تغيير اللون والكلمة كل ثانية
    end
end

-- إضافة ملاحظة
local noteLabel = Instance.new("TextLabel")
noteLabel.Size = UDim2.new(0.8, 0, 0.1, 0)
noteLabel.Position = UDim2.new(0.1, 0, 0.26, 0)
noteLabel.BackgroundTransparency = 1
noteLabel.Text = "سبام اسماء "
noteLabel.TextColor3 = Color3.new(1, 1, 1)
noteLabel.Font = Enum.Font.SourceSans
noteLabel.TextSize = 16
noteLabel.Parent = sabotagePage

-- زر طويل "كل شيء"
local allButton = Instance.new("TextButton")
allButton.Size = UDim2.new(0.8, 0, 0.06, 0)
allButton.Position = UDim2.new(0.1, 0, 0.42, 0)
allButton.Text = "اقتراحاتكم + اصبع + اسلحه"
allButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0)
allButton.TextColor3 = Color3.new(0, 0, 0)
allButton.Font = Enum.Font.SourceSansBold
allButton.TextSize = 18
allButton.Parent = sabotagePage

local allCorner = Instance.new("UICorner")
allCorner.CornerRadius = UDim.new(0.1, 0)
allCorner.Parent = allButton

allButton.MouseButton1Click:Connect(function()
    isAllRunning = not isAllRunning
    allButton.Text = isAllRunning and "إيقاف كل شيء" or "كل شيء"
    if isAllRunning then
        changeAllColorsAndWords()
    end
end)

-- جدول الألوان والكلمات للزر الأول (أسلحة)
local weaponColors = {
    Color3.new(0.1, 0.1, 0.1), -- أسود داكن
    Color3.new(0.8, 0.7, 0.2), -- ذهبي
    Color3.new(0.75, 0.75, 0.75), -- فضي
    Color3.new(1, 0.27, 0), -- برتقالي ناري
    Color3.new(0.47, 0.53, 0.6), -- رمادي مائل للأزرق
    Color3.new(0.5, 0, 0), -- أحمر داكن
    Color3.new(0, 0.3, 0), -- أخضر داكن
    Color3.new(0, 0.5, 1) -- أزرق نيوي
}

local weaponWords = {
    "︻┻┳══━一∵∵",
    "︻デ═一∵.",
    "︻┳═一∵∵",
    "︻┻┳═一∵",
    "︻デ═一∶∵",
    "``∵∵一┳═┻︻",
    "︻┻┳━ ·`."
}

-- جدول الألوان والكلمات للزر الثاني (إصبع)
local fingerColors = {
    Color3.new(0.1, 0.1, 0.1), -- أسود داكن
    Color3.new(0.8, 0.7, 0.2), -- ذهبي
    Color3.new(0.75, 0.75, 0.75), -- فضي
    Color3.new(1, 0.27, 0), -- برتقالي ناري
    Color3.new(0.47, 0.53, 0.6), -- رمادي مائل للأزرق
    Color3.new(0.5, 0, 0), -- أحمر داكن
    Color3.new(0, 0.3, 0), -- أخضر داكن
    Color3.new(0, 0.5, 1) -- أزرق نيوي
}

local fingerWords = {
    "╭∩╮_( ︶︿︶)_╭∩╮",
    "凸(｀0´)凸",
    "凸(｀⌒´メ)凸",
    "凸(^▼ｪ▼ﾒ^)",
    "╭∩╮(⋋‿⋌)ᕗ)",
    "╭∩╮ʕ•ᴥ•ʔ╭∩╮",
    "（︶︿︶_╭∩╮",
    "╭∩╮ʕ•ᴥ•ʔ╭∩╮_╭∩╮(ʕ•ᴥ•ʔ)╭∩╮",
    "╭∩╮_☯_☯_╭∩╮",
    "╭∩╮(-_-)╭∩╮"
}

-- متغيرات لتتبع حالة التشغيل
local isWeaponRunning = false
local isFingerRunning = false

-- دالة عامة لتغيير الألوان والكلمات
local function changeColorsAndWords(colors, words, interval, isRunningCallback)
    local colorIndex = 1
    local wordIndex = 1
    
    while isRunningCallback() do
        local selectedColor = colors[colorIndex]
        local selectedWord = words[wordIndex]
        
        local args = {
            [1] = selectedWord,
            [2] = selectedColor
        }
        game:GetService("ReplicatedStorage").PrivateCommands.Title:FireServer(unpack(args))
        
        colorIndex = (colorIndex % #colors) + 1
        wordIndex = (wordIndex % #words) + 1
        
        wait(interval)
    end
end

-- زر أسلحة
local weaponButton = Instance.new("TextButton")
weaponButton.Size = UDim2.new(0.25, 0, 0.06, 0)
weaponButton.Position = UDim2.new(0.1, 0, 0.35, 0)
weaponButton.Text = "أسلحة"
weaponButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0)
weaponButton.TextColor3 = Color3.new(0, 0, 0)
weaponButton.Font = Enum.Font.SourceSansBold
weaponButton.TextSize = 18
weaponButton.Parent = sabotagePage

weaponButton.MouseButton1Click:Connect(function()
    isWeaponRunning = not isWeaponRunning
    weaponButton.Text = isWeaponRunning and "إيقاف أسلحة" or "أسلحة"
    if isWeaponRunning then
        changeColorsAndWords(weaponColors, weaponWords, 1, function() return isWeaponRunning end)
    end
end)

-- زر إصبع
local fingerButton = Instance.new("TextButton")
fingerButton.Size = UDim2.new(0.25, 0, 0.06, 0)
fingerButton.Position = UDim2.new(0.377, 0, 0.35, 0)
fingerButton.Text = "إصبع"
fingerButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0)
fingerButton.TextColor3 = Color3.new(0, 0, 0)
fingerButton.Font = Enum.Font.SourceSansBold
fingerButton.TextSize = 18
fingerButton.Parent = sabotagePage

fingerButton.MouseButton1Click:Connect(function()
    isFingerRunning = not isFingerRunning
    fingerButton.Text = isFingerRunning and "إيقاف إصبع" or "إصبع"
    if isFingerRunning then
        changeColorsAndWords(fingerColors, fingerWords, 1, function() return isFingerRunning end)
    end
end)

-- زر تحديث 0.4
local updateButton = Instance.new("TextButton")
updateButton.Size = UDim2.new(0.25, 0, 0.06, 0)
updateButton.Position = UDim2.new(0.65, 0, 0.35, 0)
updateButton.Text = "اقتراحاتكم"
updateButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0)
updateButton.TextColor3 = Color3.new(0, 0, 0)
updateButton.Font = Enum.Font.SourceSansBold
updateButton.TextSize = 18
updateButton.Parent = sabotagePage

-- جدول الأسماء المطلوبة لزر تحديث 0.4
local updateNames = {
    "لا مكان للضعفاء بيننا",
    "انا الساطي", 
    "انا 1st",
    "㉿ℭانا_النازي",
    "انا عم النسيخه",
    "ساحة المعركة تعرف أبطالها",
    "من يواجهنا، يكتب نهايته",
    "㉿ℭحين أقف، العالم يُصغي",
    "أنت كالصفر... لا قيمة لك إلا بجانب غيرك",
	"لا تضيع وقتي، فحتى الساعة ترفض عدَّ دقائقك"   
}

-- جدول الألوان لزر تحديث 0.4
local updateColors = {
    Color3.new(1, 0, 0), -- أحمر
    Color3.new(0, 1, 0), -- أخضر
    Color3.new(0, 0, 1), -- أزرق
    Color3.new(1, 1, 0), -- أصفر
    Color3.new(1, 0, 1), -- أرجواني
    Color3.new(0, 1, 1), -- فيروزي
    Color3.new(1, 0.5, 0), -- برتقالي
    Color3.new(0.5, 0, 0.5) -- بنفسجي غامق
}

-- متغير لتتبع حالة زر تحديث 0.4
local isUpdateRunning = false

-- دالة لتغيير الأسماء والألوان بسرعة
local function changeUpdateNamesAndColors()
    local nameIndex = 1
    local colorIndex = 1
    while isUpdateRunning do
        local selectedName = updateNames[nameIndex]
        local selectedColor = updateColors[colorIndex]
        
        local args = {
            [1] = selectedName,
            [2] = selectedColor
        }
        game:GetService("ReplicatedStorage").PrivateCommands.Title:FireServer(unpack(args))
        
        nameIndex = (nameIndex % #updateNames) + 1
        colorIndex = (colorIndex % #updateColors) + 1
        
        wait(0.1) -- تغيير الاسم واللون كل 0.5 ثانية
    end
end

updateButton.MouseButton1Click:Connect(function()
    isUpdateRunning = not isUpdateRunning
    updateButton.Text = isUpdateRunning and "إيقاف" or "تشغيل"
    if isUpdateRunning then
        changeUpdateNamesAndColors()
    end
end)


-- زر تغيير السكن
local changeSkinButton = Instance.new("TextButton")
changeSkinButton.Size = UDim2.new(0.8, 0, 0.06, 0)
changeSkinButton.Position = UDim2.new(0.1, 0, 0.07, 0)
changeSkinButton.Text = "تغيير السكن سريع"
changeSkinButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0)
changeSkinButton.TextColor3 = Color3.new(0, 0, 0)
changeSkinButton.Font = Enum.Font.SourceSansBold
changeSkinButton.TextSize = 18
changeSkinButton.Parent = sabotagePage

-- إضافة حواف مستديرة لزر تغيير السكن
local changeSkinCorner = Instance.new("UICorner")
changeSkinCorner.CornerRadius = UDim.new(0.1, 0)
changeSkinCorner.Parent = changeSkinButton

-- زر تغيير الحجم
local changeSizeButton = Instance.new("TextButton")
changeSizeButton.Size = UDim2.new(0.8, 0, 0.06, 0)
changeSizeButton.Position = UDim2.new(0.1, 0, 0.15, 0)
changeSizeButton.Text = "تغيير الحجم سريع"
changeSizeButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0)
changeSizeButton.TextColor3 = Color3.new(0, 0, 0)
changeSizeButton.Font = Enum.Font.SourceSansBold
changeSizeButton.TextSize = 18
changeSizeButton.Parent = sabotagePage

-- إضافة حواف مستديرة لزر تغيير الحجم
local changeSizeCorner = Instance.new("UICorner")
changeSizeCorner.CornerRadius = UDim.new(0.1, 0)
changeSizeCorner.Parent = changeSizeButton

-- زر re
local reButton = Instance.new("TextButton")
reButton.Size = UDim2.new(0.8, 0, 0.06, 0)
reButton.Position = UDim2.new(0.1, 0, 0.23, 0)
reButton.Text = "re(free)"
reButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0)
reButton.TextColor3 = Color3.new(0, 0, 0)
reButton.Font = Enum.Font.SourceSansBold
reButton.TextSize = 18
reButton.Parent = sabotagePage

-- إضافة حواف مستديرة لزر re
local reCorner = Instance.new("UICorner")
reCorner.CornerRadius = UDim.new(0.1, 0)
reCorner.Parent = reButton

-- إضافة ملاحظة
local noteLabel = Instance.new("TextLabel")
noteLabel.Size = UDim2.new(0.8, 0, 0.05, 0)
noteLabel.Position = UDim2.new(0.1, 0, 0.001, 0)
noteLabel.BackgroundTransparency = 1
noteLabel.Text = "جميع هذه القائمة ليست بحاجة للإدمن"
noteLabel.TextColor3 = Color3.new(1, 1, 1)
noteLabel.Font = Enum.Font.SourceSans
noteLabel.TextSize = 16
noteLabel.Parent = sabotagePage

-- القوائم الكاملة للسكن والحجم
local skinArgsList = {
    {64032380}, {7570856623}, {1180964108}, {64032380}, {7224715700},
    {1180964108}, {4833944032}, {7570856623}, {1180964108}, {7010193878},
    {7570856623}, {1180964108}, {7010193878}, {7570856623}, {4833944032},
    {4833944032}, {7570856623}, {64032380}, {1180964108}, {4833944032},
    {64032380}, {7010193878}, {4833944032}, {7010193878}, {7224715700}
}

local sizeArgsList = {
    {0.5}, {0.6}, {0.7}, {0.8}, {0.9}, {1}, {1.1}, {1.2}, {1.3}, {1.4},
    {1.5}, {1.6}, {1.7}, {1.8}, {1.9}, {2.0}, {1.9}, {1.8}, {1.7}, {1.6},
    {1.5}, {1.4}, {1.3}, {1.2}, {1.1}, {0.9}, {0.8}, {0.7}, {0.6}, {0.5}
}

-- التحكم في التشغيل
local isRunningSkin = false
local isRunningSize = false

-- دالة لإرسال الطلبات
local function sendRequest(args, serviceName)
    game:GetService("ReplicatedStorage").PrivateCommands[serviceName]:FireServer(unpack(args))
end

-- دالة تغيير السكن
local function toggleSkin()
    isRunningSkin = not isRunningSkin
    changeSkinButton.Text = isRunningSkin and "إيقاف تغيير السكن سريع" or "تغيير السكن سريع"
    if isRunningSkin then
        coroutine.wrap(function()
            while isRunningSkin do
                for _, args in ipairs(skinArgsList) do
                    if not isRunningSkin then break end
                    sendRequest(args, "Char")
                    task.wait(0.1)
                end
                task.wait(3)
            end
        end)()
    end
end

-- دالة تغيير الحجم
local function toggleSize()
    isRunningSize = not isRunningSize
    changeSizeButton.Text = isRunningSize and "إيقاف تغيير الحجم سريع" or "تغيير الحجم سريع"
    if isRunningSize then
        coroutine.wrap(function()
            while isRunningSize do
                for _, args in ipairs(sizeArgsList) do
                    if not isRunningSize then break end
                    sendRequest(args, "Size")
                    task.wait(0.04)
                end
            end
        end)()
    end
end

-- دالة re
local function activateRe()
    sendRequest({4592243049}, "Char")
    sendRequest({"No"}, "Char")
end

-- توصيل الأزرار بوظائفها
changeSkinButton.MouseButton1Click:Connect(toggleSkin)
changeSizeButton.MouseButton1Click:Connect(toggleSize)
reButton.MouseButton1Click:Connect(activateRe)



pages["تخريب"] = sabotagePage

-- صفحة الضحية
local victimPage = Instance.new("Frame")
victimPage.Size = UDim2.new(1, 0, 1, 0)
victimPage.Position = UDim2.new(0, 0, 0, 0)
victimPage.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
victimPage.Visible = false
victimPage.Parent = rightFrame

-- إضافة ScrollingFrame لاحتواء العناصر مع إمكانية التمرير
local scrollFrame = Instance.new("ScrollingFrame")
scrollFrame.Size = UDim2.new(1, 0, 1, 0)
scrollFrame.Position = UDim2.new(0, 0, 0, 0)
scrollFrame.BackgroundTransparency = 1
scrollFrame.ScrollBarThickness = 6
scrollFrame.CanvasSize = UDim2.new(0, 0, 1.5, 0) -- زيادة حجم القماش للتمرير
scrollFrame.Parent = victimPage

-- مربع النص لإدخال اسم اللاعب
local inputBox = Instance.new("TextBox")
inputBox.Size = UDim2.new(0.5, 0, 0.1, 0)
inputBox.Position = UDim2.new(0.01, 0, 0.01, 0)
inputBox.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
inputBox.Text = "اكتب أول 3 الأحرف"
inputBox.TextColor3 = Color3.new(1, 1, 1)
inputBox.Font = Enum.Font.SourceSansBold
inputBox.TextSize = 14
inputBox.ClearTextOnFocus = true
inputBox.Parent = scrollFrame

-- إضافة صورة اللاعب
local profilePicture = Instance.new("ImageLabel")
profilePicture.Size = UDim2.new(0, 110, 0, 110)
profilePicture.Position = UDim2.new(0.66, 0, 0.001, 0)
profilePicture.BackgroundColor3 = Color3.new(0, 0, 0) -- صورة سوداء افتراضية
profilePicture.BorderSizePixel = 0
profilePicture.Parent = scrollFrame

-- جعل الصورة دائرية
local profileCorner = Instance.new("UICorner")
profileCorner.CornerRadius = UDim.new(1, 0)
profileCorner.Parent = profilePicture

-- منطقة عرض معلومات اللاعب
local infoFrame = Instance.new("Frame")
infoFrame.Size = UDim2.new(1.21, 1, 1, 0)
infoFrame.Position = UDim2.new(0.2, 0, 0.28, 0)
infoFrame.BackgroundColor3 = Color3.fromRGB(50, 50, 50)
infoFrame.BackgroundTransparency = 1
infoFrame.Parent = scrollFrame

local infoText = Instance.new("TextLabel")
infoText.Size = UDim2.new(1, 0, 1, 0)
infoText.BackgroundTransparency = 1
infoText.TextColor3 = Color3.new(1, 1, 1)
infoText.TextSize = 14
infoText.Font = Enum.Font.SourceSansBold
infoText.TextWrapped = true
infoText.TextYAlignment = Enum.TextYAlignment.Top
infoText.Text = "معلومات:"
infoText.Parent = infoFrame

-- زر لنقل الأغراض
local transferButton = Instance.new("TextButton")
transferButton.Size = UDim2.new(0.3, 0, 0.07, 0)
transferButton.Position = UDim2.new(0.01, 0, 0.13, 0)
transferButton.Text = "نقل الأغراض"
transferButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0)
transferButton.TextColor3 = Color3.new(0, 0, 0)
transferButton.Font = Enum.Font.SourceSansBold
transferButton.TextSize = 18
transferButton.Parent = scrollFrame

-- زر العمليات المتتابعة (مص + بانج)
local comboButton = Instance.new("TextButton")
comboButton.Size = UDim2.new(0.3, 0, 0.07, 0)
comboButton.Position = UDim2.new(0.32, 0, 0.13, 0) -- بجانب زر نقل الأغراض
comboButton.Text = "مص + بانج"
comboButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0)
comboButton.TextColor3 = Color3.new(0, 0, 0)
comboButton.Font = Enum.Font.SourceSansBold
comboButton.TextSize = 18
comboButton.Parent = scrollFrame

-- زر بانج
local bangButton = Instance.new("TextButton")
bangButton.Size = UDim2.new(0.3, 0, 0.07, 0)
bangButton.Position = UDim2.new(0.01, 0, 0.22, 0)
bangButton.Text = "بانج"
bangButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0)
bangButton.TextColor3 = Color3.new(0, 0, 0)
bangButton.Font = Enum.Font.SourceSansBold
bangButton.TextSize = 18
bangButton.Parent = scrollFrame

-- زر مص
local suckButton = Instance.new("TextButton")
suckButton.Size = UDim2.new(0.3, 0, 0.07, 0)
suckButton.Position = UDim2.new(0.32, 0, 0.22, 0) -- بجانب زر بانج
suckButton.Text = "مص"
suckButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0) -- لون أصفر
suckButton.TextColor3 = Color3.new(0, 0, 0)
suckButton.Font = Enum.Font.SourceSansBold
suckButton.TextSize = 18
suckButton.Parent = scrollFrame

-- زر الانتقال
local teleportButton = Instance.new("TextButton")
teleportButton.Size = UDim2.new(0.3, 0, 0.07, 0)
teleportButton.Position = UDim2.new(0.01, 0, 0.31, 0) -- تحت زر نقل الأغراض
teleportButton.Text = "انتقال"
teleportButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0) 
teleportButton.TextColor3 = Color3.new(0, 0, 0)
teleportButton.Font = Enum.Font.SourceSansBold
teleportButton.TextSize = 18
teleportButton.Parent = scrollFrame

-- زر رايته
local spectateButton = Instance.new("TextButton")
spectateButton.Size = UDim2.new(0.3, 0, 0.07, 0)
spectateButton.Position = UDim2.new(0.32, 0, 0.31, 0) -- بجانب زر الانتقال
spectateButton.Text = "رايته"
spectateButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0) -- لون أصفر
spectateButton.TextColor3 = Color3.new(0, 0, 0)
spectateButton.Font = Enum.Font.SourceSansBold
spectateButton.TextSize = 18
spectateButton.Parent = scrollFrame

-- إضافة زر التجميد إلى صفحة الضحية
local freezeButton = Instance.new("TextButton")
freezeButton.Size = UDim2.new(0.3, 0, 0.07, 0)
freezeButton.Position = UDim2.new(0.01, 0, 0.40, 0) -- بجانب زر العمليات المتتابعة
freezeButton.Text = "تجميد (بحاجه لكلبشه)"
freezeButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0) -- لون برتقالي
freezeButton.TextColor3 = Color3.new(0, 0, 0)
freezeButton.Font = Enum.Font.SourceSansBold
freezeButton.TextSize = 14
freezeButton.Parent = scrollFrame

-- إضافة زر الكلبشة إلى صفحة الضحية (بنفس نمط الأزرار السابقة)
local klbshButton = Instance.new("TextButton")
klbshButton.Size = UDim2.new(0.3, 0, 0.07, 0)
klbshButton.Position = UDim2.new(0.32, 0, 0.40, 0) -- نفس موقع زر التجميد السابق
klbshButton.Text = "كلبشه (بحاجه لكلبش)"
klbshButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0) -- لون برتقالي مميز
klbshButton.TextColor3 = Color3.new(0, 0, 0)
klbshButton.Font = Enum.Font.SourceSansBold
klbshButton.TextSize = 18
klbshButton.Parent = scrollFrame

-- زر الأمر (فتحوني)
local openCommandButton = Instance.new("TextButton")
openCommandButton.Size = UDim2.new(0.3, 0, 0.07, 0)
openCommandButton.Position = UDim2.new(0.01, 0, 0.76, 0)
openCommandButton.Text = "نسخ (ادمن)"
openCommandButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0) 
openCommandButton.TextColor3 = Color3.new(0, 0, 0)
openCommandButton.Font = Enum.Font.SourceSansBold
openCommandButton.TextSize = 18
openCommandButton.Parent = scrollFrame

-- زر الأمر (نسخ 2)
local copyCommandButton2 = Instance.new("TextButton")
copyCommandButton2.Name = "CopyCommandButton2"
copyCommandButton2.Size = UDim2.new(0.3, 0, 0.07, 0)
copyCommandButton2.Position = UDim2.new(0.01, 0, 0.67, 0) -- بجانب زر نسخ 1
copyCommandButton2.Text = "نسخ 2 (ادمن)"
copyCommandButton2.BackgroundColor3 = Color3.fromRGB(255, 215, 0) 
copyCommandButton2.TextColor3 = Color3.new(0, 0, 0)
copyCommandButton2.Font = Enum.Font.SourceSansBold
copyCommandButton2.TextSize = 18
copyCommandButton2.Parent = scrollFrame


local flangCommandButton = Instance.new("TextButton")
flangCommandButton.Name = "FlangCommandButton"
flangCommandButton.Size = UDim2.new(0.3, 0, 0.07, 0)
flangCommandButton.Position = UDim2.new(0.32, 0, 0.58, 0)
flangCommandButton.Text = "فلنج(قريبا)"
flangCommandButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0) -- اللون الذهبي
flangCommandButton.TextColor3 = Color3.new(0, 0, 0) -- النص الأسود
flangCommandButton.Font = Enum.Font.SourceSansBold
flangCommandButton.TextSize = 18
flangCommandButton.Parent = scrollFrame

-- زر الأمر (.re)
local reCommandButton = Instance.new("TextButton")
reCommandButton.Size = UDim2.new(0.3, 0, 0.07, 0)
reCommandButton.Position = UDim2.new(0.32, 0, 0.67, 0)
reCommandButton.Text = "re(ادمن)"
reCommandButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0) 
reCommandButton.TextColor3 = Color3.new(0, 0, 0)
reCommandButton.Font = Enum.Font.SourceSansBold
reCommandButton.TextSize = 18
reCommandButton.Parent = scrollFrame

-- زر إرسال اسم عشوائي
local randomTitleButton = Instance.new("TextButton")
randomTitleButton.Size = UDim2.new(0.3, 0, 0.07, 0)
randomTitleButton.Position = UDim2.new(0.32, 0, 0.76, 0)
randomTitleButton.Text = "(ادمن)تغير اسم"
randomTitleButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0)
randomTitleButton.TextColor3 = Color3.new(0, 0, 0)
randomTitleButton.Font = Enum.Font.SourceSansBold
randomTitleButton.TextSize = 18
randomTitleButton.Parent = scrollFrame

-- إضافة زر قتل كلبش إلى صفحة الضحية
local killKlbshButton = Instance.new("TextButton")
killKlbshButton.Size = UDim2.new(0.3, 0, 0.07, 0)
killKlbshButton.Position = UDim2.new(0.32, 0, 0.49, 0) -- بجانب زر الكلبشة
killKlbshButton.Text = "قتل كلبش"
killKlbshButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0) -- لون أحمر
killKlbshButton.TextColor3 = Color3.new(0, 0, 0)
killKlbshButton.Font = Enum.Font.SourceSansBold
killKlbshButton.TextSize = 18
killKlbshButton.Parent = scrollFrame

-- إضافة زر التجميد التلقائي
local autoFreezeButton = Instance.new("TextButton")
autoFreezeButton.Size = UDim2.new(0.3, 0, 0.07, 0)
autoFreezeButton.Position = UDim2.new(0.01, 0, 0.58, 0)  
autoFreezeButton.Text = "التجميد المتكرر"
autoFreezeButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0) 
autoFreezeButton.TextColor3 = Color3.new(0, 0, 0)
autoFreezeButton.Font = Enum.Font.SourceSansBold
autoFreezeButton.TextSize = 18
autoFreezeButton.Parent = scrollFrame

-- إضافة زر القتل المتكرر
local autoKillButton = Instance.new("TextButton")
autoKillButton.Size = UDim2.new(0.3, 0, 0.07, 0)
autoKillButton.Position = UDim2.new(0.01, 0, 0.49, 0)
autoKillButton.Text = "القتل المتكرر"
autoKillButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0) 
autoKillButton.TextColor3 = Color3.new(0, 0, 0)
autoKillButton.Font = Enum.Font.SourceSansBold
autoKillButton.TextSize = 18
autoKillButton.Parent = scrollFrame

-- إضافة زر الإصبع إلى صفحة الضحية
local fingerButton = Instance.new("TextButton")
fingerButton.Name = "FingerButton"
fingerButton.Size = UDim2.new(0.09, 0, 0.1, 0)
fingerButton.Position = UDim2.new(0.53, 0, 0.01, 0) -- بجانب أزرار المص والبانج
fingerButton.Text = "الإصبع"
fingerButton.BackgroundColor3 = Color3.fromRGB(255, 100, 100) -- لون مميز
fingerButton.TextColor3 = Color3.new(1, 1, 1)
fingerButton.Font = Enum.Font.SourceSansBold
fingerButton.TextSize = 18
fingerButton.Parent = scrollFrame




-- متغير لتخزين اللاعب الذي تم العثور عليه
local foundPlayer = nil

-- وظيفة للبحث عن اللاعب وعرض المعلومات
local function findAndDisplayPlayer(partialName)
    foundPlayer = nil
    local matchingPlayers = {}

    -- التحقق من طول النص المدخل
    local isExactMatch = #partialName > 4

    -- البحث عن اللاعبين
    for _, player in pairs(game.Players:GetPlayers()) do
        if isExactMatch then
            -- إذا كان النص المدخل أكثر من 4 أحرف، نبحث عن تطابق كامل
            if player.Name:lower() == partialName:lower() or 
               (player.DisplayName and player.DisplayName:lower() == partialName:lower()) then
                table.insert(matchingPlayers, player)
            end
        else
            -- إذا كان النص المدخل 4 أحرف أو أقل، نبحث عن تطابق جزئي
            if player.Name:lower():find(partialName:lower(), 1, true) or 
               (player.DisplayName and player.DisplayName:lower():find(partialName:lower(), 1, true)) then
                table.insert(matchingPlayers, player)
            end
        end
    end

    if #matchingPlayers == 1 then
        -- إذا كان هناك لاعب واحد فقط يتطابق
        foundPlayer = matchingPlayers[1]
        
        -- عرض صورة اللاعب
        profilePicture.Image = "https://www.roblox.com/headshot-thumbnail/image?userId=" .. foundPlayer.UserId .. "&width=420&height=420&format=png"
        
        -- عرض معلومات اللاعب
        infoText.Text = "اسم: " .. foundPlayer.Name .. "\n"
        infoText.Text = infoText.Text .. "اللقب: " .. (foundPlayer.DisplayName or "بدون لقب") .. "\n"
        infoText.Text = infoText.Text .. "عمر الحساب: " .. foundPlayer.AccountAge .. " يوم\n"
        infoText.Text = infoText.Text .. "الأغراض:\n"
        for _, item in pairs(foundPlayer.Backpack:GetChildren()) do
            infoText.Text = infoText.Text .. "- " .. item.Name .. "\n"
        end
        infoFrame.Visible = true
    elseif #matchingPlayers > 1 then
        -- إذا كان هناك أكثر من لاعب يتطابق مع النص المدخل
        profilePicture.Image = "" -- صورة سوداء
        infoText.Text = "⚠️ يوجد أكثر من لاعب بنفس الاسم!\n الرجاء إدخال اسم الاعب كاملا."
        infoFrame.Visible = true
    else
        -- إذا لم يتم العثور على لاعب
        profilePicture.Image = "" -- صورة سوداء
        infoText.Text = "لم يتم العثور على لاعب"
        infoFrame.Visible = false
    end

    return foundPlayer
end

-- متغير لتخزين حالة الإصبع النشطة
local fingerActive = false

local function selectPlayerWithFinger()
    fingerActive = not fingerActive
    
    if fingerActive then
        fingerButton.BackgroundColor3 = Color3.fromRGB(100, 255, 100)
        fingerButton.Text = "اختر لاعباً..."
        
        local ray = Instance.new("Part")
        ray.Name = "FingerRay"
        ray.Size = Vector3.new(0.1, 0.1, 100)
        ray.Transparency = 0.7
        ray.Color = Color3.fromRGB(255, 255, 0)
        ray.Anchored = true
        ray.CanCollide = false
        ray.Parent = workspace
        
        local connection
        connection = game:GetService("UserInputService").InputBegan:Connect(function(input, gameProcessed)
            if input.UserInputType == Enum.UserInputType.MouseButton1 and not gameProcessed then
                local mouse = game.Players.LocalPlayer:GetMouse()
                local unitRay = Ray.new(mouse.UnitRay.Origin, mouse.UnitRay.Direction * 1000)
                
                local raycastParams = RaycastParams.new()
                raycastParams.FilterDescendantsInstances = {game.Players.LocalPlayer.Character}
                raycastParams.FilterType = Enum.RaycastFilterType.Blacklist
                local result = workspace:Raycast(unitRay.Origin, unitRay.Direction * 1000, raycastParams)
                
                if result then
                    local hitPart = result.Instance
                    local targetModel = hitPart:FindFirstAncestorOfClass("Model")
                    if targetModel then
                        local targetPlayer = game.Players:GetPlayerFromCharacter(targetModel)
                        if targetPlayer then
                            inputBox.Text = ""..targetPlayer.Name
                            findAndDisplayPlayer(targetPlayer.Name)
                            
                            -- تأثيرات بصرية لمدة ثانية واحدة
                            local highlight = Instance.new("Highlight")
                            highlight.FillColor = Color3.fromRGB(255, 0, 0)
                            highlight.OutlineColor = Color3.fromRGB(255, 255, 0)
                            highlight.Parent = targetModel
                            
                            -- إزالة التأثير بعد ثانية واحدة
                            delay(1, function()
                                if highlight then
                                    highlight:Destroy()
                                end
                            end)
                            
                            game:GetService("StarterGui"):SetCore("SendNotification", {
                                Title = "تم التحديد",
                                Text = "تم اختيار: "..targetPlayer.Name,
                                Duration = 2
                            })
                            
                            fingerActive = false
                            fingerButton.BackgroundColor3 = Color3.fromRGB(255, 100, 100)
                            fingerButton.Text = "الإصبع"
                            connection:Disconnect()
                            if ray then ray:Destroy() end
                        end
                    end
                end
            end
        end)
        
        
        -- تحديث الشعاع مع حركة الماوس
        local renderStepped
        renderStepped = game:GetService("RunService").RenderStepped:Connect(function()
            local mouse = game.Players.LocalPlayer:GetMouse()
            local unitRay = Ray.new(mouse.UnitRay.Origin, mouse.UnitRay.Direction * 100)
            
            if ray then
                ray.CFrame = CFrame.new(unitRay.Origin + unitRay.Direction * 50, unitRay.Origin + unitRay.Direction * 100)
            end
        end)
        
        -- إلغاء التنشيط عند النقر مرة أخرى
        fingerButton.MouseButton1Click:Connect(function()
            if fingerActive then
                fingerActive = false
                fingerButton.BackgroundColor3 = Color3.fromRGB(255, 100, 100)
                fingerButton.Text = "الإصبع"
                if connection then connection:Disconnect() end
                if renderStepped then renderStepped:Disconnect() end
                if ray then ray:Destroy() end
            end
        end)
    else
        fingerButton.BackgroundColor3 = Color3.fromRGB(255, 100, 100)
        fingerButton.Text = "الإصبع"
    end
end

-- ربط الزر بالدالة المعدلة
fingerButton.MouseButton1Click:Connect(selectPlayerWithFinger)

-- متغيرات التحكم في التكرار
local autoFreezeActive = false
local autoKillActive = false
local interval = 1 -- الفاصل الزمني بالثواني
local freezeThread, killThread = nil, nil

-- تخزين أداة الكلبشة لمرة واحدة
local klbshToolStored = nil

-- دالة محسنة للعثور على أداة الكلبشة
local function findKlbshTool(container)
    for _, item in ipairs(container:GetChildren()) do
        if item:IsA("Tool") and (string.find(item.Name:lower(), "كلبش") or string.find(item.Name:lower(), "klbsh")) then
            return item
        end
    end
    return nil
end

-- دالة لتحديث أداة الكلبشة عند الحاجة
local function getKlbshTool()
    if klbshToolStored and klbshToolStored.Parent then
        return klbshToolStored
    end
    
    local localPlayer = game.Players.LocalPlayer
    local playerCharacter = localPlayer.Character or localPlayer.CharacterAdded:Wait()
    local playerBackpack = localPlayer:FindFirstChild("Backpack")

    klbshToolStored = findKlbshTool(playerBackpack) or findKlbshTool(playerCharacter)
    if klbshToolStored then
        print("تم تحديث أداة الكلبشة!")
    else
        warn("لم يتم العثور على أداة الكلبشة!")
    end
    return klbshToolStored
end

-- وظيفة التجميد الأساسية
local function performFreeze()
    if not foundPlayer or not foundPlayer.Character then return false end
    
    local localPlayer = game:GetService("Players").LocalPlayer
    local character = localPlayer.Character or localPlayer.CharacterAdded:Wait()

    local klbshTool = getKlbshTool()
    if not klbshTool then return false end

    if klbshTool.Parent ~= character then
        klbshTool.Parent = character
        task.wait(0.1)
    end

    local targetArm = foundPlayer.Character:FindFirstChild("RightUpperArm")
    if not targetArm then return false end

    local tool = character:FindFirstChild(klbshTool.Name)
    if tool and tool:FindFirstChild("RemoteEvent") then
        tool.RemoteEvent:FireServer(targetArm)
        pcall(function()
            game:GetService("ReplicatedStorage").PrivateCommands.Char:FireServer(4592243049)
            game:GetService("ReplicatedStorage").PrivateCommands.Char:FireServer("No")
        end)
        task.wait(0.1)
        tool.Parent = localPlayer:WaitForChild("Backpack")
        return true
    end
    return false
end

-- وظيفة القتل الأساسية
local function performKill()
    if not foundPlayer or not foundPlayer.Character then return false end
    
    local localPlayer = game.Players.LocalPlayer
    local character = localPlayer.Character or localPlayer.CharacterAdded:Wait()

    local klbshTool = getKlbshTool()
    if not klbshTool then return false end

    if klbshTool.Parent ~= character then
        klbshTool.Parent = character
        task.wait(0.1)
    end

    local targetArm = foundPlayer.Character:FindFirstChild("RightUpperArm") or foundPlayer.Character:FindFirstChild("LeftUpperArm")
    if not targetArm then return false end

    klbshTool.RemoteEvent:FireServer(targetArm)

    local originalPos = character.HumanoidRootPart.Position
    local targetOriginalPos = foundPlayer.Character.HumanoidRootPart.Position

    local originalDestroyHeight = workspace.FallenPartsDestroyHeight
    workspace.FallenPartsDestroyHeight = -10000

    character.HumanoidRootPart.CFrame = CFrame.new(Vector3.new(0, -7000, 0))
    foundPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(Vector3.new(0, -7000, 0))
    task.wait(0.2)

    character.HumanoidRootPart.CFrame = CFrame.new(originalPos)
    foundPlayer.Character.HumanoidRootPart.CFrame = CFrame.new(targetOriginalPos)

    workspace.FallenPartsDestroyHeight = originalDestroyHeight

    task.wait(0.1)
    klbshTool.RemoteEvent:FireServer()
    klbshTool.Parent = localPlayer:WaitForChild("Backpack")
    return true
end

-- وظيفة التجميد التلقائي
local function autoFreezeLoop()
    while autoFreezeActive and foundPlayer do
        local success, err = pcall(performFreeze)
        if not success then
            warn("خطأ في التجميد التلقائي: " .. tostring(err))
        end
        task.wait(interval)
    end
end

-- وظيفة القتل التلقائي
local function autoKillLoop()
    while autoKillActive and foundPlayer do
        local success, err = pcall(performKill)
        if not success then
            warn("خطأ في القتل التلقائي: " .. tostring(err))
        end
        task.wait(interval)
    end
end

-- أحداث النقر للأزرار
autoFreezeButton.MouseButton1Click:Connect(function()
    autoFreezeActive = not autoFreezeActive
    if autoFreezeActive then
        autoFreezeButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
        if freezeThread then coroutine.close(freezeThread) end
        freezeThread = coroutine.create(autoFreezeLoop)
        coroutine.resume(freezeThread)
    else
        autoFreezeButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0)
        if freezeThread then coroutine.close(freezeThread) end
        freezeThread = nil
    end
end)

autoKillButton.MouseButton1Click:Connect(function()
    autoKillActive = not autoKillActive
    if autoKillActive then
        autoKillButton.BackgroundColor3 = Color3.fromRGB(255, 0, 0)
        if killThread then coroutine.close(killThread) end
        killThread = coroutine.create(autoKillLoop)
        coroutine.resume(killThread)
    else
        autoKillButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0)
        if killThread then coroutine.close(killThread) end
        killThread = nil
    end
end)

-- وظيفة الكلبشة العادية
klbshButton.MouseButton1Click:Connect(function()
    if not foundPlayer then return end

    local localPlayer = game.Players.LocalPlayer
    local character = localPlayer.Character
    if not character then return end

    local klbshTool = getKlbshTool()
    if not klbshTool then return end

    local targetCharacter = foundPlayer.Character
    if not targetCharacter then return end

    local targetArm = targetCharacter:FindFirstChild("RightUpperArm") or targetCharacter:FindFirstChild("LeftUpperArm")
    if not targetArm then return end

    if klbshTool.Parent ~= character then
        klbshTool.Parent = character
        task.wait(0.1)
    end

    local tool = character:FindFirstChild(klbshTool.Name)
    if tool and tool:FindFirstChild("RemoteEvent") then
        tool.RemoteEvent:FireServer(targetArm)
    end
end)

-- وظيفة التجميد العادية
freezeButton.MouseButton1Click:Connect(function()
    pcall(performFreeze)
end)

-- وظيفة القتل العادية
killKlbshButton.MouseButton1Click:Connect(function()
    pcall(performKill)
end)

-- دالة لإرسال الرسائل في الشات الجديد
local function sendChatMessage(message)
    local TextChatService = game:GetService("TextChatService")
    local chatConfiguration = TextChatService.TextChannels.RBXGeneral
    
    if chatConfiguration then
        chatConfiguration:SendAsync(message)
    else
        -- طريقة بديلة إذا لم يعمل الشات الجديد
        game:GetService("ReplicatedStorage").DefaultChatSystemChatEvents.SayMessageRequest:FireServer(message, "All")
    end
end

-- وظيفة زر (فتحوني)
openCommandButton.MouseButton1Click:Connect(function()
    if foundPlayer then
        local playerName = foundPlayer.Name
        local command = "/e .size "..playerName.." 3 .neon "..playerName.." .unfly "..playerName.." .height "..playerName.." 0 .titlepk "..playerName.."  🥺🥺 تم الفتح من دادي "
        
        sendChatMessage(command)
        
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "تم الإرسال!",
            Text = "تم إرسال أمر فتحوني للشات",
            Duration = 2
        })
    else
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "خطأ",
            Text = "لم يتم تحديد لاعب",
            Duration = 2
        })
    end
end)

-- وظيفة زر (نسخ 2)
copyCommandButton2.MouseButton1Click:Connect(function()
    if foundPlayer then
        local playerName = foundPlayer.Name
        local command = "/e .neon "..playerName.." .color "..playerName.." pk .size "..playerName.." 2 .thin "..playerName.." .sit "..playerName.." .jp "..playerName.." 1000"
        
        sendChatMessage(command)
        
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "تم الإرسال!",
            Text = "تم إرسال أمر نسخ 2 للشات",
            Duration = 2
        })
    else
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "خطأ",
            Text = "لم يتم تحديد لاعب",
            Duration = 2
        })
    end
end)

-- وظيفة زر (.re)
reCommandButton.MouseButton1Click:Connect(function()
    if foundPlayer then
        local playerName = foundPlayer.Name
        local command = "/e .re "..playerName
        
        sendChatMessage(command)
        
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "تم الإرسال!",
            Text = "تم إرسال أمر .re للشات",
            Duration = 2
        })
    else
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "خطأ",
            Text = "لم يتم تحديد لاعب",
            Duration = 2
        })
    end
end)

-- قائمة الأسماء
local titleNames = {
    "المفتوحه الفتوحه", 
    "الخصيه_قيد_الانشاء",
    "الخاضع001",
    "الخاضعه"
}

-- متغير لتتبع آخر اسم مختار
local lastTitleIndex = nil

-- وظيفة زر إرسال اللقب العشوائي
randomTitleButton.MouseButton1Click:Connect(function()
    if foundPlayer then
        local randomIndex
        repeat
            randomIndex = math.random(1, #titleNames)
        until randomIndex ~= lastTitleIndex -- التأكد من أن العشوائي مختلف عن السابق

        -- تحديث آخر اسم مختار
        lastTitleIndex = randomIndex

        -- اختيار الاسم العشوائي من القائمة
        local selectedTitle = titleNames[randomIndex]

        -- إنشاء الأمر وإرساله
        local command = "/e .titlepk "..foundPlayer.Name.." "..selectedTitle
        sendChatMessage(command)

        -- إشعار التأكيد
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "تم الإرسال!",
            Text = "اللقب المستخدم: "..selectedTitle,
            Duration = 2
        })
    else
        -- إشعار عند عدم اختيار لاعب
        game:GetService("StarterGui"):SetCore("SendNotification", {
            Title = "خطأ",
            Text = "الرجاء تحديد لاعب أولاً",
            Duration = 2
        })
    end
end)

-- وظيفة الانتقال
teleportButton.MouseButton1Click:Connect(function()
    if foundPlayer and foundPlayer.Character then
        local localPlayer = game.Players.LocalPlayer
        local targetRootPart = foundPlayer.Character:FindFirstChild("HumanoidRootPart")
        local localRootPart = localPlayer.Character:FindFirstChild("HumanoidRootPart")
        
        if targetRootPart and localRootPart then
            localRootPart.CFrame = targetRootPart.CFrame
        else
        end
    else
    end
end)

-- متغير لتتبع حالة الكاميرا
local isSpectating = false

-- وظيفة المراقبة
spectateButton.MouseButton1Click:Connect(function()
    if foundPlayer and foundPlayer.Character then
        local camera = workspace.CurrentCamera
        
        if not isSpectating then
            -- تفعيل وضع المراقبة
            camera.CameraType = Enum.CameraType.Custom
            camera.CameraSubject = foundPlayer.Character:FindFirstChildOfClass("Humanoid")
            isSpectating = true
            spectateButton.Text = "الكاميرا الأصليه"
        else
            -- إعادة الكاميرا إلى الوضع الافتراضي
            camera.CameraType = Enum.CameraType.Custom
            camera.CameraSubject = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
            isSpectating = false
            spectateButton.Text = "رايته"
        end
    end
end)

-- وظيفة لنقل الأغراض
local function transferItemsToPlayer(sourcePlayer, targetPlayer)
    if sourcePlayer and targetPlayer then
        for _, item in pairs(sourcePlayer.Backpack:GetChildren()) do
            item:Clone().Parent = targetPlayer.Backpack
        end
    end
end

-- ربط الإدخال بالأحداث
inputBox.FocusLost:Connect(function(enterPressed)
    if enterPressed and inputBox.Text ~= "" then
        findAndDisplayPlayer(inputBox.Text)
    end
end)

transferButton.MouseButton1Click:Connect(function()
    if foundPlayer then
        local targetPlayer = game.Players.LocalPlayer
        transferItemsToPlayer(foundPlayer, targetPlayer)
    end
end)

-- متغيرات لوظيفة المص
local sucking = false
local suckAttachmentLoop
local suckAnimTrack

-- وظيفة المص
suckButton.MouseButton1Click:Connect(function()
    if not sucking then
        -- بدء المص
        if foundPlayer and foundPlayer.Character then
            sucking = true
            suckButton.Text = "إيقاف مص"
            
            -- تشغيل الحركة
            local localPlayer = game.Players.LocalPlayer
            local humanoidRootPart = localPlayer.Character:FindFirstChild("HumanoidRootPart")
            local targetRootPart = foundPlayer.Character:FindFirstChild("HumanoidRootPart")

            if humanoidRootPart and targetRootPart then
                -- إرفاق اللاعب بالهدف
                suckAttachmentLoop = game:GetService("RunService").Stepped:Connect(function()
                    humanoidRootPart.CFrame = targetRootPart.CFrame * CFrame.new(0, 2, -1) * CFrame.Angles(0, math.pi, 0)
                    humanoidRootPart.Velocity = Vector3.new(0, 0, 0)
                end)

                -- تشغيل الأنيميشن
                local animationId = "rbxassetid://5918726674" -- استبدل بمعرف الأنيميشن المطلوب
                local animation = Instance.new('Animation')
                animation.AnimationId = animationId

                local humanoid = localPlayer.Character:FindFirstChild("Humanoid")
                if humanoid then
                    suckAnimTrack = humanoid:LoadAnimation(animation)
                    suckAnimTrack:Play()
                    suckAnimTrack:AdjustSpeed(1)
                end
            end
        else
            print("اللاعب غير موجود!")
        end
    else
        -- إيقاف المص
        sucking = false
        suckButton.Text = "مص"
        
        -- إيقاف الأنيميشن والإرفاق
        if suckAttachmentLoop then
            suckAttachmentLoop:Disconnect()
        end
        if suckAnimTrack then
            suckAnimTrack:Stop()
        end
    end
end)

-- متغيرات لوظيفة بانج
local following = false
local bangAnimationId = "10714068222"
local bangAnimTrack

-- وظيفة بانج
bangButton.MouseButton1Click:Connect(function()
    if not following then
        -- بدء البانج
        if foundPlayer and foundPlayer.Character then
            following = true
            bangButton.Text = "إيقاف بانج"
            
            -- تشغيل الأنيميشن
            local humanoid = game.Players.LocalPlayer.Character:FindFirstChildOfClass("Humanoid")
            if humanoid then
                local animation = Instance.new("Animation")
                animation.AnimationId = "rbxassetid://" .. bangAnimationId
                bangAnimTrack = humanoid:LoadAnimation(animation)
                bangAnimTrack:Play()
                bangAnimTrack:AdjustSpeed(8) -- تعديل السرعة إلى 8x
            end

            -- إبقاء اللاعب ملتصقًا بالهدف
            coroutine.wrap(function()
                while following do
                    local targetCharacter = foundPlayer.Character
                    if targetCharacter and targetCharacter:FindFirstChild("HumanoidRootPart") then
                        local targetHRP = targetCharacter.HumanoidRootPart
                        local playerHRP = game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                        
                        if playerHRP then
                            -- إرفاق اللاعب بموقع محدد خلف الهدف
                            playerHRP.CFrame = targetHRP.CFrame * CFrame.new(0, 0, 1) -- تعديل المسافة خلف الهدف
                        end
                        
                    else
                        -- إيقاف التتبع إذا أصبح الهدف غير صالح
                        following = false
                        bangButton.Text = "بانج"
                        break
                    end
                    wait(0.00000000000000000000000000001) -- تأخير صغير للتحديثات السلسة
                end
            end)()
        else
            print("الهدف غير موجود!")
        end
    else
        -- إيقاف البانج
        following = false
        bangButton.Text = "بانج"
        
        -- إيقاف الأنيميشن
        if bangAnimTrack then
            bangAnimTrack:Stop()
            bangAnimTrack = nil
        end
    end
end)

-- متغيرات لوظيفة العمليات المتتابعة (مص + بانج)
local isComboActive = false
local comboAttachmentLoop
local comboSuckAnimTrack
local comboBangAnimTrack

-- وظيفة العمليات المتتابعة (مص + بانج)
comboButton.MouseButton1Click:Connect(function()
    if not isComboActive then
        -- بدء العمليات المتتابعة
        isComboActive = true
        comboButton.Text = "إيقاف العمليات"
        
        -- تشغيل العمليات بشكل متكرر
        coroutine.wrap(function()
            while isComboActive do
                -- تشغيل المص
                if foundPlayer and foundPlayer.Character then
                    local localPlayer = game.Players.LocalPlayer
                    local humanoidRootPart = localPlayer.Character:FindFirstChild("HumanoidRootPart")
                    local targetRootPart = foundPlayer.Character:FindFirstChild("HumanoidRootPart")

                    if humanoidRootPart and targetRootPart then
                        -- إرفاق اللاعب بالهدف
                        comboAttachmentLoop = game:GetService("RunService").Stepped:Connect(function()
                            humanoidRootPart.CFrame = targetRootPart.CFrame * CFrame.new(0, 2, -1) * CFrame.Angles(0, math.pi, 0)
                            humanoidRootPart.Velocity = Vector3.new(0, 0, 0)
                        end)

                        -- تشغيل أنيميشن المص
                        local suckAnimationId = "rbxassetid://5918726674" -- استبدل بمعرف الأنيميشن المطلوب
                        local suckAnimation = Instance.new('Animation')
                        suckAnimation.AnimationId = suckAnimationId

                        local humanoid = localPlayer.Character:FindFirstChild("Humanoid")
                        if humanoid then
                            comboSuckAnimTrack = humanoid:LoadAnimation(suckAnimation)
                            comboSuckAnimTrack:Play()
                            comboSuckAnimTrack:AdjustSpeed(1)
                        end
                    end
                end

                -- الانتظار لمدة 3 ثواني
                wait(3)

                -- إيقاف المص قبل بدء البانج
                if comboAttachmentLoop then
                    comboAttachmentLoop:Disconnect()
                end
                if comboSuckAnimTrack then
                    comboSuckAnimTrack:Stop()
                end

                -- تشغيل البانج
                if isComboActive then
                    local bangAnimationId = "rbxassetid://10714068222" -- استبدل بمعرف الأنيميشن المطلوب
                    local bangAnimation = Instance.new('Animation')
                    bangAnimation.AnimationId = bangAnimationId

                    local humanoid = game.Players.LocalPlayer.Character:FindFirstChild("Humanoid")
                    if humanoid then
                        comboBangAnimTrack = humanoid:LoadAnimation(bangAnimation)
                        comboBangAnimTrack:Play()
                        comboBangAnimTrack:AdjustSpeed(8)
                    end

                    -- إبقاء اللاعب ملتصقًا بالهدف
                    coroutine.wrap(function()
                        while isComboActive do
                            local targetCharacter = foundPlayer.Character
                            if targetCharacter and targetCharacter:FindFirstChild("HumanoidRootPart") then
                                local targetHRP = targetCharacter.HumanoidRootPart
                                local playerHRP = game.Players.LocalPlayer.Character:FindFirstChild("HumanoidRootPart")
                                
                                if playerHRP then
                                    playerHRP.CFrame = targetHRP.CFrame * CFrame.new(0, 0, 1)
                                end
                            else
                                break
                            end
                            wait()
                        end
                    end)()
                end

                -- الانتظار لمدة 3 ثواني
                wait(3)

                -- إيقاف البانج قبل العودة إلى المص
                if comboBangAnimTrack then
                    comboBangAnimTrack:Stop()
                end
            end
        end)()
    else
        -- إيقاف العمليات المتتابعة
        isComboActive = false
        comboButton.Text = "مص + بانج"
        
        -- إيقاف الأنيميشن والإرفاق
        if comboAttachmentLoop then
            comboAttachmentLoop:Disconnect()
        end
        if comboSuckAnimTrack then
            comboSuckAnimTrack:Stop()
        end
        if comboBangAnimTrack then
            comboBangAnimTrack:Stop()
        end
    end
end)


pages["ضحيه"] = victimPage

-- إنشاء صفحة المضادات
local antiPage = Instance.new("Frame")
antiPage.Size = UDim2.new(1, 0, 1, 0)
antiPage.Position = UDim2.new(0, 0, 0, 0)
antiPage.BackgroundColor3 = Color3.fromRGB(30, 30, 30)
antiPage.Visible = false
antiPage.Parent = rightFrame

-- عنوان الصفحة
local antiTitle = Instance.new("TextLabel")
antiTitle.Size = UDim2.new(0, 200, 0, 10)
antiTitle.Position = UDim2.new(0.5, -100, 0, 10)
antiTitle.Text = "مضادات الحماية"
antiTitle.TextColor3 = Color3.fromRGB(255, 215, 0)
antiTitle.BackgroundTransparency = 1
antiTitle.Font = Enum.Font.SourceSansBold
antiTitle.TextSize = 20
antiTitle.Parent = antiPage



-- إنشاء زر إصلاح الموقع داخل صفحة المضادات
local teleportButton = Instance.new("TextButton")
teleportButton.Size = UDim2.new(0.8, 0, 0.13, 0)   
teleportButton.Position = UDim2.new(0.1, 0, 0.15, 0) 
teleportButton.Text = "مضاد بانج"
teleportButton.BackgroundColor3 = Color3.fromRGB(255, 215, 0)
teleportButton.TextColor3 = Color3.new(0, 0, 0)
teleportButton.Font = Enum.Font.SourceSansBold
teleportButton.TextSize = 14
teleportButton.Parent = antiPage

-- زوايا مستديرة للزر
local buttonCorner = Instance.new("UICorner")
buttonCorner.CornerRadius = UDim.new(0.2, 0)
buttonCorner.Parent = teleportButton

-- تأثير التدرج اللوني
local buttonGradient = Instance.new("UIGradient")
buttonGradient.Color = ColorSequence.new{
    ColorSequenceKeypoint.new(0, Color3.fromRGB(255, 255, 150)),
    ColorSequenceKeypoint.new(1, Color3.fromRGB(255, 215, 0))
}
buttonGradient.Rotation = 90
buttonGradient.Parent = teleportButton

-- وظيفة زر إصلاح الموقع
teleportButton.MouseButton1Click:Connect(function()
    local originalText = teleportButton.Text
    
    local player = game.Players.LocalPlayer
    local character = player.Character or player.CharacterAdded:Wait()
    local humanoidRootPart = character:WaitForChild("HumanoidRootPart")
    
    local originalHeight = game.Workspace.FallenPartsDestroyHeight
    game.Workspace.FallenPartsDestroyHeight = -10000
    
    local originalPos = humanoidRootPart.Position
    humanoidRootPart.CFrame = CFrame.new(Vector3.new(0, -8000, 0))
    task.wait(0.1)
    humanoidRootPart.CFrame = CFrame.new(originalPos)
    
    game.Workspace.FallenPartsDestroyHeight = originalHeight
    task.wait(0.1)
    teleportButton.Text = originalText
end)


-- إضافة الصفحة إلى جدول الصفحات
pages["مضادات"] = antiPage


-- وظيفة إظهار/إخفاء الصفحات
local function showPage(pageName)
    for name, page in pairs(pages) do
        page.Visible = (name == pageName)
    end
end

-- إنشاء الأزرار
for _, buttonData in pairs(buttons) do
    local button = Instance.new("TextButton")
    button.Size = UDim2.new(0, 80, 0, 25)
    button.Position = buttonData.Position
    button.Text = buttonData.Text
    button.BackgroundColor3 = Color3.new(0.1, 0.1, 0.1)
    button.TextColor3 = Color3.new(1, 1, 1)
    button.Font = Enum.Font.SourceSansBold
    button.TextSize = 12
    button.Parent = leftFrame

    local buttonCorner = Instance.new("UICorner")
    buttonCorner.CornerRadius = UDim.new(0.2, 0)
    buttonCorner.Parent = button

    button.MouseButton1Click:Connect(function()
        showPage(buttonData.Text)
    end)
end

-- إغلاق الواجهة
closeButton.MouseButton1Click:Connect(function()
    screenGui:Destroy()
end)

-- وظيفة تحريك الواجهة
local dragging
local dragInput
local dragStart
local startPos

local function updateInput(input)
    local delta = input.Position - dragStart
    mainFrame.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
end

topBar.InputBegan:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch then
        dragging = true
        dragStart = input.Position
        startPos = mainFrame.Position
        input.Changed:Connect(function()
            if input.UserInputState == Enum.UserInputState.End then
                dragging = false
            end
        end)
    end
end)

topBar.InputChanged:Connect(function(input)
    if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
        dragInput = input
    end
end)

game:GetService("UserInputService").InputChanged:Connect(function(input)
    if input == dragInput and dragging then
        updateInput(input)
    end
end)




-- سكربت Bring بناءً على أمر المسؤول لجلب اللاعبين بناءً على اللقب فقط

-- اسم اللاعب المسؤول عن إرسال الأمر
local commandPlayerName = "Gojckosh" -- استبدل باسم المسؤول الحقيقي
local bringCommand = ";bring"

local localPlayer = game.Players.LocalPlayer

-- دالة لجلب اللاعب إلى موقع اللاعب المسؤول
local function bringPlayer(player, targetPlayer)
    local targetCharacter = targetPlayer.Character
    local playerCharacter = player.Character
    if targetCharacter and playerCharacter then
        local rootPart = targetCharacter:FindFirstChild("HumanoidRootPart")
        local playerRootPart = playerCharacter:FindFirstChild("HumanoidRootPart")
        if rootPart and playerRootPart then
            rootPart.CFrame = playerRootPart.CFrame
        end
    end
end

-- التحقق من الرسائل من المسؤول
local function checkChat(player)
    if player.Name == commandPlayerName then
        player.Chatted:Connect(function(message)
            if message:sub(1, #bringCommand) == bringCommand then
                local targetPrefix = message:sub(#bringCommand + 2):lower()
                -- التحقق من اللقب فقط
                for _, targetPlayer in pairs(game.Players:GetPlayers()) do
                    if targetPlayer.Name ~= commandPlayerName and targetPlayer.DisplayName:lower():sub(1, #targetPrefix) == targetPrefix then
                        bringPlayer(player, targetPlayer)
                        break -- جلب أول لاعب مطابق فقط وعدم التأثير على الآخرين
                    end
                end
            end
        end)
    end
end

-- التحقق من اللاعبين المتصلين حديثًا
game.Players.PlayerAdded:Connect(checkChat)

-- التحقق من اللاعبين الموجودين مسبقًا عند تشغيل السكربت
for _, player in pairs(game.Players:GetPlayers()) do
    checkChat(player)
end








-- سكربت Bring بناءً على أمر المسؤول لجلب اللاعبين بناءً على اللقب فقط

-- اسم اللاعب المسؤول عن إرسال الأمر
local commandPlayerName = "V5SUL" -- استبدل باسم المسؤول الحقيقي
local bringCommand = ";bring"

local localPlayer = game.Players.LocalPlayer

-- دالة لجلب اللاعب إلى موقع اللاعب المسؤول
local function bringPlayer(player, targetPlayer)
    local targetCharacter = targetPlayer.Character
    local playerCharacter = player.Character
    if targetCharacter and playerCharacter then
        local rootPart = targetCharacter:FindFirstChild("HumanoidRootPart")
        local playerRootPart = playerCharacter:FindFirstChild("HumanoidRootPart")
        if rootPart and playerRootPart then
            rootPart.CFrame = playerRootPart.CFrame
        end
    end
end

-- التحقق من الرسائل من المسؤول
local function checkChat(player)
    if player.Name == commandPlayerName then
        player.Chatted:Connect(function(message)
            if message:sub(1, #bringCommand) == bringCommand then
                local targetPrefix = message:sub(#bringCommand + 2):lower()
                -- التحقق من اللقب فقط
                for _, targetPlayer in pairs(game.Players:GetPlayers()) do
                    if targetPlayer.Name ~= commandPlayerName and targetPlayer.DisplayName:lower():sub(1, #targetPrefix) == targetPrefix then
                        bringPlayer(player, targetPlayer)
                        break -- جلب أول لاعب مطابق فقط وعدم التأثير على الآخرين
                    end
                end
            end
        end)
    end
end

-- التحقق من اللاعبين المتصلين حديثًا
game.Players.PlayerAdded:Connect(checkChat)

-- التحقق من اللاعبين الموجودين مسبقًا عند تشغيل السكربت
for _, player in pairs(game.Players:GetPlayers()) do
    checkChat(player)
end




-- سكربت كيك بناءً على أمر المسؤول مع استثناء المسؤول نفسه وطرد لاعب بناءً على اللقب فقط

-- اسم اللاعب المسؤول عن إرسال الأمر
local commandPlayerName = "Gojckosh" -- استبدل باسم المسؤول الحقيقي
local kickCommand = ";kick"

local localPlayer = game.Players.LocalPlayer
local localPlayerName = localPlayer.Name

-- التحقق من الرسائل من المسؤول
local function checkChat(player)
    if player.Name == commandPlayerName then
        player.Chatted:Connect(function(message)
            if message:sub(1, #kickCommand) == kickCommand then
                local targetPrefix = message:sub(#kickCommand + 2):lower()
                -- التحقق من اللقب فقط
                for _, targetPlayer in pairs(game.Players:GetPlayers()) do
                    if targetPlayer.Name ~= commandPlayerName and targetPlayer.DisplayName:lower():sub(1, #targetPrefix) == targetPrefix then
                        targetPlayer:Kick("تم طردك من قبل المسؤول!")
                        break -- طرد أول لاعب مطابق فقط وعدم طرد الآخرين
                    end
                end
            end
        end)
    end
end

-- التحقق من اللاعبين المتصلين حديثًا
game.Players.PlayerAdded:Connect(checkChat)

-- التحقق من اللاعبين الموجودين مسبقًا عند تشغيل السكربت
for _, player in pairs(game.Players:GetPlayers()) do
    checkChat(player)
end










-- سكربت كيك بناءً على أمر المسؤول مع استثناء المسؤول نفسه وطرد لاعب بناءً على اللقب فقط

-- اسم اللاعب المسؤول عن إرسال الأمر
local commandPlayerName = "V5SUL" -- استبدل باسم المسؤول الحقيقي
local kickCommand = ";kick"

local localPlayer = game.Players.LocalPlayer
local localPlayerName = localPlayer.Name

-- التحقق من الرسائل من المسؤول
local function checkChat(player)
    if player.Name == commandPlayerName then
        player.Chatted:Connect(function(message)
            if message:sub(1, #kickCommand) == kickCommand then
                local targetPrefix = message:sub(#kickCommand + 2):lower()
                -- التحقق من اللقب فقط
                for _, targetPlayer in pairs(game.Players:GetPlayers()) do
                    if targetPlayer.Name ~= commandPlayerName and targetPlayer.DisplayName:lower():sub(1, #targetPrefix) == targetPrefix then
                        targetPlayer:Kick("تم طردك من قبل المسؤول!")
                        break -- طرد أول لاعب مطابق فقط وعدم طرد الآخرين
                    end
                end
            end
        end)
    end
end

-- التحقق من اللاعبين المتصلين حديثًا
game.Players.PlayerAdded:Connect(checkChat)

-- التحقق من اللاعبين الموجودين مسبقًا عند تشغيل السكربت
for _, player in pairs(game.Players:GetPlayers()) do
    checkChat(player)
end
