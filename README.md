# fwqf1wr1
wqfqwf
로컬 유창한 자 = loadstring(game:HttpGet("https://github.com/dawid-scripts/Fluent/releases/latest/download/main.lua"))() 
local SaveManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/SaveManager.lua"))()
local InterfaceManager = loadstring(game:HttpGet("https://raw.githubusercontent.com/dawid-scripts/Fluent/master/Addons/InterfaceManager.lua"))()
 
로컬 창 = 유창한 : CreateWindow ({ 
 제목 = "유창한".. 유창한 버전, 
    SubTitle = "by dawid",
 탭 너비 = 160, 
 크기 = UDim2.fromOffset(580, 460), 
 Acrylic = true, -- 블러를 감지할 수 있으며, 이를 false로 설정하면 블러가 완전히 비활성화됩니다. 
 테마 = "어둡게", 
 MinimizeKey = Enum.KeyCode.LeftControl -- MinimizeKeybind가 없을 때 사용 
})
 
로컬 탭 = { 
 AutoFarm = window:AddTab({ title = "AutoFarm", icon = "" }), 
 도구 = window:AddTab({ title = "tool", icon = "" }), 
 EXP = Window:AddTab({title = "EXP", 아이콘 = "dollar-sign"}), 
 설정 = window:AddTab({ title = "설정", icon = "설정" }), 
}
 
로컬 옵션 = Fluent.Options 
 
--바르 
로컬 플레이어 = 게임. 플레이어.로컬 플레이어 
로컬 캐릭터 = Player.Character 
로컬 휴머노이드 = Character.Humanoid 
로컬 HumanoidRootPart = Character.HumanoidRootPart 
 
--함수 
로컬 함수 fireproximityprompt(ProximityPrompt, Amount, Skip) 
 assert(ProximityPrompt, "인수 #1 누락 또는 없음") 
 assert(typeof(ProximityPrompt) == "Instance" 및 ProximityPrompt:IsA("ProximityPrompt"), "ProximityPrompt가 아닌 값을 실행하려고 시도했습니다.") 
 
 로컬 HoldDuration = ProximityPrompt.HoldDuration 
 
 건너뛰면 
        ProximityPrompt.HoldDuration = 0
 끝 
 
 for i = 1, 금액 또는 1 do 
        ProximityPrompt:InputHoldBegin()
 그렇지 않은 경우 건너 뜁니다. 
 로컬 RunService = game:GetService("RunService") 
 로컬 시작 = 시간() 
 반복하다 
 RunService.Heartbeat : 대기 (0.1) 
 until time() - HoldDuration> 시작 
 끝 
        ProximityPrompt:InputHoldEnd()
 끝 
 
 건너뛰면 
 ProximityPrompt.HoldDuration = 보류 기간 
 끝 
끝 
 
local 도구 
현지 금액 = 1 
 
로컬 ToolDropDown = Tabs.Tool:AddDropdown("ToolDropDown", { 
    Title = "복사툴 선택",
    Values = {" 백 덤블링", "540도 발차기", "내려차기", "둘개차기", "앞굽이 자세 이동", "앞돌려차기", "앞차기", "옆차기", "주춤서 몸통막기", "주춤서 아래막기", "주춤서 정권 지르기", "주춤서기 자세 이동"},
 다중 = 거짓, 
 기본값 = 1, 
})
 
ToolDropDown:OnChanged(함수(값) 
 도구 = 값 
끝) 
 
로컬 ToolNumberInput = Tabs.Tool:AddInput("ToolNumberInput", { 
    Title = "개수",
 기본값 = "1", 
    Placeholder = "개수를 입력하세요.",
 numeric = true, -- 숫자만 허용 
 Finished = false, -- Enter 키를 누를 때만 콜백을 호출합니다. 
 콜백 = function(Value) 
 금액 = 값 
 끝 
})
 
Tabs.Tool:AddButton({
    Title = "확인",
    Description = "툴 복사 진행",
 콜백 = function() 
 창:대화 상자({ 
            Title = "경고",
 내용 = "정말로 진행 하시겠습니까? (되돌리지 못합니다.)", 
 버튼 = { 
                {
                    Title = "확인",
 콜백 = function() 
 Tool and Amount인 경우 
 for i=1, 금액, 1 do 
                                local Tool = game:GetService("Lighting"):WaitForChild(Tool)
 
 도구인 경우 
 로컬 ClonedTool = 도구:Clone() 
 ClonedTool.Parent = 게임. Players.LocalPlayer.Backpack (영문) 
 끝 
 끝 
 끝 
 끝 
                },
                {
                    Title = "취소",
 콜백 = function() 
 print("대화 상자를 취소했습니다.") 
 끝 
                }
            }
        })
 끝 
})
 
로컬 BoxGivePrompt 
로컬 BoxSellPrompt 
 
for i,v in ipairs(workspace:GetDescendants()) 수행 
 v:IsA("ProximityPrompt") 및 v.ActionText == "상자 받기"이면 
        BoxGivePrompt = v
 끝 
끝 
 
for i,v in ipairs(workspace:GetDescendants()) 수행 
 v:IsA("ProximityPrompt") 및 v.ActionText == "상자 주기"이면 
        BoxSellPrompt = v
 끝 
끝 
 
로컬 BoxMacroToggle = Tabs.AutoFarm:AddToggle("BoxToggle", {Title = "박스 매크로", Default = false }) 
 
BoxMacroToggle:OnChanged(함수() 
 Options.BoxToggle.Value 및 BoxGivePrompt인 경우 
 Options.BoxToggle.Value 는 
            task.wait(.2)
            HumanoidRootPart.CFrame = BoxGivePrompt.Parent.CFrame
            task.wait(.2)
 fireproximityprompt (BoxGivePrompt, 1, true) 
            task.wait(.2)
 휴머노이드RootPart.CFrame = BoxSellPrompt.Parent.CFrame 
            task.wait(.2)
 fireproximityprompt (BoxSellPrompt, 1, true) 
 끝 
 끝 
끝) 
 
local EXPMacro = Tabs.AutoFarm:AddToggle("EXPToggle", {Title = "경험치 매크로 (오토 클릭 필요)", Default = false })
 
EXPMacro:OnChanged(함수() 
 Options.EXPToggle.Value이면 
 
 로컬 백팩 = 게임. Players.LocalPlayer.Backpack:GetChildren() 
 
 Options.EXPToggle.Value 는 
 for i,v in ipairs(백팩) do 
 v:IsA("도구")이면 
 태스크.대기(.001) 
 v.Parent = 게임. Players.LocalPlayer.캐릭터 
 태스크.대기(.001) 
 v.Parent = 게임. Players.LocalPlayer.Backpack (영문) 
 끝 
 끝 
 끝 
 
 끝 
끝) 
 
 
 
 
--특급 
현지 금액 
 
로컬 EXPInput = Tabs.EXP:AddInput("EXPInput", { 
 Title = "금액 (음수 가능)", 
 기본값 = "", 
 플레이스홀더 = "금액", 
 numeric = true, -- 숫자만 허용 
 Finished = false, -- Enter 키를 누를 때만 콜백을 호출합니다. 
 콜백 = function(Value) 
 Amount = tostring(값) 
 끝 
})
 
Tabs.EXP:AddButton({
 Title = "기부", 
    Description = "원하는 양의 EXP를 받을수 있습니다.",
 콜백 = function() 
 창:대화 상자({ 
 Title = "경고", 
            Content = "정말 진행 하시곘아요?",
 버튼 = { 
                {
 Title = "확인", 
 콜백 = function() 
 게임. ReplicatedStorage.Cilcker:FireServer(금액) 
 끝 
                },
                {
 Title = "취소", 
 콜백 = function() 
 끝 
                }
            }
        })
 끝 
})
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
-- 애드온: 
-SaveManager (구성 시스템을 가질 수 있음) 
-- InterfaceManager (인터페이스 관리 시스템을 가질 수 있음) 
 
-- 도서관을 우리 매니저에게 넘겨주세요. 
SaveManager : SetLibrary (유창한) 
InterfaceManager : SetLibrary (유창한) 
 
-- ThemeManager에서 사용하는 키를 무시합니다. 
-- (우리는 구성이 테마를 저장하는 것을 원하지 않습니다, 그렇죠?) 
SaveManager:IgnoreThemeSettings()를 호출합니다. 
 
-- 저장 관리자가 무시해야 하는 요소의 인덱스를 추가할 수 있습니다. 
SaveManager:SetIgnoreIndexes({})
 
-이런 식으로하는 사용 사례 : 
-- 스크립트 허브는 전역 폴더에 테마가 있을 수 있습니다. 
-- 게임별로 별도의 폴더에 있는 게임 구성 
InterfaceManager:SetFolder("FluentScriptHub")
SaveManager:SetFolder("FluentScriptHub/특정 게임") 
 
InterfaceManager : BuildInterfaceSection (Tabs.Settings) 
SaveManager : BuildConfigSection (Tabs.Settings) 
 
 
창:SelectTab(1) 
 
유창한:알림({ 
 제목 = "유창한", 
 Content = "스크립트가 로드되었습니다.", 
 기간 = 8 
})
 
-- SaveManager:LoadAutoloadConfig()를 사용하여 구성을 로드할 수 있습니다. 
-- 자동으로로드되는 것으로 표시되었습니다! 
SaveManager : LoadAutoloadConfig()
