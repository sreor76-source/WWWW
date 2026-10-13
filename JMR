-- Services
local Players = game:GetService("Players")
local UserInputService = game:GetService("UserInputService")
local LocalPlayer = Players.LocalPlayer

-- Create GUI
local ScreenGui = Instance.new("ScreenGui")
ScreenGui.Name = "SmartTargetSkinChanger"
local successParent, _ = pcall(function() ScreenGui.Parent = game:GetService("CoreGui") end)
if not successParent then ScreenGui.Parent = LocalPlayer:WaitForChild("PlayerGui") end

local MainFrame = Instance.new("Frame")
MainFrame.Size = UDim2.new(0, 300, 0, 420)
MainFrame.Position = UDim2.new(0.5, -150, 0.5, -210)
MainFrame.BackgroundColor3 = Color3.fromRGB(15, 15, 20)
MainFrame.BorderSizePixel = 2
MainFrame.BorderColor3 = Color3.fromRGB(150, 50, 255)
MainFrame.Active = true
MainFrame.Draggable = true
MainFrame.Parent = ScreenGui

Instance.new("UICorner", MainFrame).CornerRadius = UDim.new(0, 8)

-- Title
local Title = Instance.new("TextLabel")
Title.Size = UDim2.new(1, 0, 0, 40)
Title.Text = "تغيير سكن الهدف (اضغط L للإخفاء)"
Title.TextColor3 = Color3.fromRGB(255, 255, 255)
Title.BackgroundColor3 = Color3.fromRGB(25, 25, 30)
Title.Font = Enum.Font.GothamBold
Title.TextSize = 13
Title.Parent = MainFrame

-- TextBox for Skin ID
local UserIdInput = Instance.new("TextBox")
UserIdInput.Size = UDim2.new(0.9, 0, 0, 38)
UserIdInput.Position = UDim2.new(0.05, 0, 0.12, 0)
UserIdInput.PlaceholderText = "أدخل ID السكن المطلوب..."
UserIdInput.Text = ""
UserIdInput.BackgroundColor3 = Color3.fromRGB(35, 35, 42)
UserIdInput.TextColor3 = Color3.fromRGB(255, 255, 255)
UserIdInput.Font = Enum.Font.Gotham
UserIdInput.TextSize = 13
UserIdInput.ClearTextOnFocus = false
UserIdInput.Parent = MainFrame

Instance.new("UICorner", UserIdInput).CornerRadius = UDim.new(0, 6)

-- Label for Player List
local ListLabel = Instance.new("TextLabel")
ListLabel.Size = UDim2.new(0.9, 0, 0, 25)
ListLabel.Position = UDim2.new(0.05, 0, 0.23, 0)
ListLabel.BackgroundTransparency = 1
ListLabel.Text = "اختر اللاعب المراد تغيير شكله:"
ListLabel.TextColor3 = Color3.fromRGB(200, 200, 200)
ListLabel.Font = Enum.Font.Gotham
ListLabel.TextSize, ListLabel.TextXAlignment = 12, Enum.TextXAlignment.Right
ListLabel.Parent = MainFrame

-- Scrolling Player List
local PlayerList = Instance.new("ScrollingFrame")
PlayerList.Size = UDim2.new(0.9, 0, 0, 180)
PlayerList.Position = UDim2.new(0.05, 0, 0.30, 0)
PlayerList.BackgroundColor3 = Color3.fromRGB(20, 20, 25)
PlayerList.CanvasSize = UDim2.new(0, 0, 0, 0)
PlayerList.ScrollBarThickness = 4
PlayerList.Parent = MainFrame

Instance.new("UICorner", PlayerList).CornerRadius = UDim.new(0, 6)

local UIListLayout = Instance.new("UIListLayout")
UIListLayout.Padding = UDim.new(0, 3)
UIListLayout.Parent = PlayerList

local selectedPlayer = nil

local function UpdatePlayerList()
	for _, child in pairs(PlayerList:GetChildren()) do
		if child:IsA("TextButton") then child:Destroy() end
	end
	
	local players = Players:GetPlayers()
	PlayerList.CanvasSize = UDim2.new(0, 0, 0, #players * 35)
	
	for _, player in pairs(players) do
		local btn = Instance.new("TextButton")
		btn.Size = UDim2.new(1, 0, 0, 32)
		btn.Text = player.Name
		btn.BackgroundColor3 = Color3.fromRGB(35, 35, 42)
		btn.TextColor3 = Color3.fromRGB(220, 220, 220)
		btn.Font = Enum.Font.Gotham
		btn.TextSize = 13
		btn.Parent = PlayerList
		
		Instance.new("UICorner", btn).CornerRadius = UDim.new(0, 4)
		
		btn.MouseButton1Click:Connect(function()
			selectedPlayer = player
			Title.Text = "الهدف: " .. player.Name
			for _, b in pairs(PlayerList:GetChildren()) do
				if b:IsA("TextButton") then b.BackgroundColor3 = Color3.fromRGB(35, 35, 42) end
			end
			btn.BackgroundColor3 = Color3.fromRGB(120, 40, 200)
			btn.TextColor3 = Color3.fromRGB(255, 255, 255)
		end)
	end
end

UpdatePlayerList()
Players.PlayerAdded:Connect(UpdatePlayerList)
Players.PlayerRemoving:Connect(UpdatePlayerList)

-- Apply Button
local ApplyBtn = Instance.new("TextButton")
ApplyBtn.Size = UDim2.new(0.9, 0, 0, 42)
ApplyBtn.Position = UDim2.new(0.05, 0, 0.77, 0)
ApplyBtn.Text = "تطبيق السكن على الهدف المحدد"
ApplyBtn.BackgroundColor3 = Color3.fromRGB(120, 40, 200)
ApplyBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
ApplyBtn.Font = Enum.Font.GothamBold
ApplyBtn.TextSize, ApplyBtn.Parent = 13, MainFrame

Instance.new("UICorner", ApplyBtn).CornerRadius = UDim.new(0, 6)

-- Close Button
local CloseBtn = Instance.new("TextButton")
CloseBtn.Size = UDim2.new(0, 25, 0, 25)
CloseBtn.Position = UDim2.new(1, -30, 0, 5)
CloseBtn.Text = "X"
CloseBtn.BackgroundColor3 = Color3.fromRGB(180, 40, 40)
CloseBtn.TextColor3 = Color3.fromRGB(255, 255, 255)
CloseBtn.Font = Enum.Font.GothamBold
CloseBtn.TextSize = 12
CloseBtn.BorderSizePixel = 0
CloseBtn.Parent = MainFrame

Instance.new("UICorner", CloseBtn).CornerRadius = UDim.new(0, 4)

CloseBtn.MouseButton1Click:Connect(function()
	ScreenGui:Destroy()
end)

-- Apply Logic
ApplyBtn.MouseButton1Click:Connect(function()
	local targetId = tonumber(UserIdInput.Text)
	if not targetId then 
		Title.Text = "خطأ: أدخل الـ ID بشكل صحيح!" 
		return 
	end
	if not selectedPlayer or not selectedPlayer.Character then 
		Title.Text = "خطأ: اختر لاعباً من القائمة أولاً!" 
		return 
	end
	
	Title.Text = "جاري التعديل على الهدف..."
	
	task.spawn(function()
		local char = selectedPlayer.Character
		if not char then 
			Title.Text = "خطأ: شخصية اللاعب غير موجودة!" 
			return 
		end
		
		local humanoid = char:FindFirstChildOfClass("Humanoid")
		local torso = char:FindFirstChild("UpperTorso") or char:FindFirstChild("Torso")
		
		if not humanoid or not torso then 
			Title.Text = "خطأ: بيانات الشخصية ناقصة!" 
			return 
		end
		
		-- إنشاء نموذج وهمي وسحب المظهر منه بالـ ID الخارجي
		local success, dummyModel = pcall(function()
			local desc = Players:GetHumanoidDescriptionFromUserId(targetId)
			return Players:CreateHumanoidModelFromDescription(desc, humanoid.RigType)
		end)
		
		if success and dummyModel then
			-- 1. مسح الملابس والإكسسوارات القديمة للهدف
			for _, item in pairs(char:GetChildren()) do
				if item:IsA("Accessory") or item:IsA("Shirt") or item:IsA("Pants") or item:IsA("ShirtGraphic") or item:IsA("BodyColors") then
					item:Destroy()
				end
			end
			
			-- 2. نسخ الملابس والألوان الجديدة
			for _, item in pairs(dummyModel:GetChildren()) do
				if item:IsA("BodyColors") or item:IsA("Shirt") or item:IsA("Pants") or item:IsA("ShirtGraphic") then
					item:Clone().Parent = char
				end
			end
			
			-- 3. معالجة الرأس مع الحفاظ على اسم اللاعب والصحة
			local dummyHead = dummyModel:FindFirstChild("Head")
			local targetHead = char:FindFirstChild("Head")
			
			if dummyHead and targetHead then
				for _, child in pairs(targetHead:GetChildren()) do
					if not child:IsA("BillboardGui") and not child:IsA("Folder") and child.Name ~= "HumanoidDisplay" then
						child:Destroy()
					end
				end
				
				for _, child in pairs(dummyHead:GetChildren()) do
					child:Clone().Parent = targetHead
				end
				
				targetHead.Color = dummyHead.Color
				targetHead.Material = dummyHead.Material
				
				if dummyHead:IsA("MeshPart") and targetHead:IsA("MeshPart") then
					targetHead.MeshId = dummyHead.MeshId
					targetHead.TextureID = dummyHead.TextureID
					targetHead.Size = dummyHead.Size
				end
			end
			
			-- 4. نسخ وإعادة تثبيت الإكسسوارات
			for _, item in pairs(dummyModel:GetChildren()) do
				if item:IsA("Accessory") then
					local cloneAcc = item:Clone()
					local handle = cloneAcc:FindFirstChild("Handle")
					if handle then
						for _, w in pairs(handle:GetChildren()) do
							if w:IsA("JointInstance") then w:Destroy() end
						end
						cloneAcc.Parent = char
						
						local accAtt = handle:FindFirstChildOfClass("Attachment")
						local targetAttPart = targetHead
						local targetAtt = targetHead and targetHead:FindFirstChild("HatAttachment")
						
						if accAtt then
							for _, part in pairs(char:GetChildren()) do
								if part:IsA("BasePart") then
									local foundAtt = part:FindFirstChild(accAtt.Name)
									if foundAtt and foundAtt:IsA("Attachment") then
										targetAttPart = part
										targetAtt = foundAtt
										break
									end
								end
							end
						end
						
						if targetAttPart and targetAtt then
							local tCFrame = targetAtt.CFrame
							local aCFrame = accAtt.CFrame
							handle.CFrame = targetAttPart.CFrame * tCFrame * aCFrame:Inverse()
							
							local weld = Instance.new("WeldConstraint")
							weld.Part0 = targetAttPart
							weld.Part1 = handle
							weld.Parent = handle
						end
					end
				end
			end
			
			dummyModel:Destroy()
			Title.Text = "تم تغيير سكن الهدف بنجاح!"
		else
			Title.Text = "فشل جلب الـ ID!"
		end
		
		task.wait(3)
		Title.Text = selectedPlayer and ("الهدف: " .. selectedPlayer.Name) or "تغيير سكن الهدف (اضغط L للإخفاء)"
	end)
end)

-- Toggle Visibility with 'L'
UserInputService.InputBegan:Connect(function(input, isTyping)
	if isTyping then return end
	if input.KeyCode == Enum.KeyCode.L then
		MainFrame.Visible = not MainFrame.Visible
	end
end)
