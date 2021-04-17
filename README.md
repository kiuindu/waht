local NilUiLib = {}


function MTError(...)
local Args = ...
local TempConn = nil
TempConn = game:GetService("RunService").RenderStepped:Connect(function()
TempConn:Disconnect()
error(Args)
end)
end


function GRName()
local StringData = ""
for Attempt=1,math.random(100,1000) do
local UTF8Char = utf8.char(math.random(0,math.random(1000,1049599)))
local NormalInt = ""
if math.random(0,1) == 1 then
NormalInt = math.random(0,9)
end
StringData = StringData .. tostring(NormalInt) .. tostring(UTF8Char)
end
return StringData
end

function RoundGui(GuiObj,Size)
local UiCorner = Instance.new("UICorner",GuiObj)
UiCorner.CornerRadius = Size
UiCorner.Name = GRName()
return UiCorner
end
function ReverseNum(Num)
return Num*-1
end

function CalculateMidPoint(...)
local Total = 0
for _,i in ipairs({...}) do
Total = Total + 1
end
return(Total/2)
end
function Lerp(Min,Max,InterpolationVal)
return Min + (Max-Min) * InterpolationVal
end
--[[
local function GetCenter(Model)
	local Sum = Vector3.new(0, 0, 0)
	local Divisor = 0
	
	for _, Descendant in pairs(Model:GetDescendants()) do
		if Descendant:IsA("BasePart") then
			Sum = Sum + Descendant.Position
			Divisor = Divisor + 1
		end
	end
	
	return Divisor ~= 0 and Sum / Divisor or false
end
--]]
function ReverseUDim2(Udim2)
local XScale,YScale,XOffset,YOffset = ReverseNum(Udim2.X.Scale), ReverseNum(Udim2.Y.Scale), ReverseNum(Udim2.X.Offset), ReverseNum(Udim2.Y.Offset)
return UDim2.new(XScale,XOffset,YScale,YOffset)
end
function CenterGuiItem(Gui)
local S = Gui.Size
Gui.Position = UDim2.new(0.5,(S.X.Offset*-1)/2,0.5,(S.Y.Offset*-1)/2)
end
local MainParent = game:GetService("CoreGui")
local Tween = game:GetService("TweenService")
local UIS = game:GetService("UserInputService")
local Mouse = game:GetService("Players").LocalPlayer:GetMouse()

local DATA_GUI_COLORS = 
{
Background = Color3.fromRGB(30,30,30),
--Borders = Color3.fromRGB(20,20,20),
--Text = Color3.fromRGB(255,255,255),
BubbleColor = Color3.fromRGB(255,255,255),
ScrollingFrameImage = Color3.fromRGB(100,100,100),
ScrollingFrameBorder = Color3.fromRGB(255,255,255),
ToggleGuiButton_OPEN = Color3.fromRGB(255,255,255),
ToggleGuiButton_CLOSED = Color3.fromRGB(20,20,20),
ToggleGuiButtonText_OPEN = Color3.fromRGB(20,20,20),
ToggleGuiButtonText_CLOSED = Color3.fromRGB(255,255,255),
TabsSelectorButton = Color3.fromRGB(255,255,255),
TabsSelectorButtonText = Color3.fromRGB(20,20,20),
TabsScrollingFrameBGColor = Color3.fromRGB(50,50,50),
TabsScrollingFrameBorderColor = Color3.fromRGB(255,255,255),
TabsScrollingFrameScrollColor = Color3.fromRGB(100,100,100),
TabSelectorButtonBGColor = Color3.fromRGB(50,50,50),
TabSelectorButtonTextColor = Color3.fromRGB(255,255,255),


ITEM_LabelTextColor = Color3.fromRGB(255,255,255),
ITEM_LabelBGColor = Color3.fromRGB(20,20,20),

-- BUTTON
ITEM_ButtonTextColor = Color3.fromRGB(255,255,255),
ITEM_ButtonBGColor = Color3.fromRGB(50,50,50),

-- TOGGLE
ITEM_MainToggleFrameBGColor = Color3.fromRGB(50,50,50),
ITEM_MainToggleTextColor = Color3.fromRGB(255,255,255),
ITEM_ToggleColorStyleOn = Color3.fromRGB(255,255,255),
ITEM_ToggleColorStyleOff = Color3.fromRGB(20,20,20),

-- VIEWPORTFRAME
ITEM_ViewportFrameFrameColor = Color3.fromRGB(50,50,50),
ITEM_ViewportFrameZoomLabelColor = Color3.fromRGB(255,255,255),

ITEM_ViewportFrameZoomButtonAddBGColor = Color3.fromRGB(30,30,30),
ITEM_ViewportFrameZoomButtonAddTextColor = Color3.fromRGB(255,255,255),

ITEM_ViewportFrameZoomButtonSubBGColor = Color3.fromRGB(30,30,30),
ITEM_ViewportFrameZoomButtonSubTextColor = Color3.fromRGB(255,255,255),

ITEM_ViewportFrameZMoveSubButtonBGColor = Color3.fromRGB(30,30,30),
ITEM_ViewportFrameZMoveSubButtonTextColor = Color3.fromRGB(255,255,255),
ITEM_ViewportFrameZMoveAddButtonBGColor = Color3.fromRGB(30,30,30),
ITEM_ViewportFrameZMoveAddButtonTextColor = Color3.fromRGB(255,255,255), 

ITEM_ViewportFrameYMoveSubButtonBGColor = Color3.fromRGB(30,30,30),
ITEM_ViewportFrameYMoveSubButtonTextColor = Color3.fromRGB(255,255,255),
ITEM_ViewportFrameYMoveAddButtonBGColor = Color3.fromRGB(30,30,30),
ITEM_ViewportFrameYMoveAddButtonTextColor = Color3.fromRGB(255,255,255), 


-- DROPDOWN
ITEM_DropdownFrameColor = Color3.fromRGB(50,50,50),
ITEM_DropdownTextColor = Color3.fromRGB(255,255,255),
ITEM_DropdownButtonBGColorDeactivated = Color3.fromRGB(30,30,30),
ITEM_DropdownButtonIconColorDeactivated = Color3.fromRGB(255,255,255),

ITEM_DropdownButtonBGColorActivated = Color3.fromRGB(255,255,255),
ITEM_DropdownButtonIconColorActivated = Color3.fromRGB(30,30,30),
ITEM_DropdownScrollingFrameColor = Color3.fromRGB(50,50,50),
ITEM_DropdownItemBackgroundColor = Color3.fromRGB(30,30,30),
ITEM_DropdownItemTextColor = Color3.fromRGB(255,255,255),

-- SLIDER
ITEM_SliderMainFrameBGColor = Color3.fromRGB(50,50,50),
ITEM_SliderInnerFrameColor = Color3.fromRGB(20,20,20),
ITEM_SliderSelectorStartColor = Color3.fromRGB(0,0,0),
ITEM_SliderSelectorEndColor = Color3.fromRGB(255,255,255),
ITEM_SliderSelectorTextBGColor = Color3.fromRGB(30,30,30),
ITEM_SliderSelectorTextColor = Color3.fromRGB(255,255,255),
ITEM_SliderMainTextColor = Color3.fromRGB(255,255,255),

-- TEXTBOX
ITEM_SliderTextBoxBGColor = Color3.fromRGB(50,50,50),
ITEM_SliderTextBoxTextColor = Color3.fromRGB(255,255,255),
ITEM_SliderTextBoxPlaceHolderColor = Color3.fromRGB(100,100,100),

}


function NilUiLib.Window(Info)

local TabSelectorOffset = 50
local MAIN_SLIDER_RUNNING = false
local WindowFunctions = {} 
local Tabs = {}
local ConnectionsTable = {}

local MainScreen = Instance.new("ScreenGui",MainParent)
MainScreen.Name = GRName()


local MainFrame = Instance.new("Frame",MainScreen)

RoundGui(MainFrame,UDim.new(0,Info.RoundSize))

MainFrame.Position = UDim2.new(0.5,(Info.SizeX/2)*-1,0.5,(Info.SizeY/2)*-1)
MainFrame.Name = GRName()
MainFrame.ClipsDescendants = true

MainFrame.BackgroundColor3 = DATA_GUI_COLORS.Background
local TabsButton = Instance.new("TextButton",MainFrame)
RoundGui(TabsButton,UDim.new(0,Info.RoundSize))
TabsButton.Name = GRName()
TabsButton.BackgroundColor3 = DATA_GUI_COLORS.TabsSelectorButton
TabsButton.Size = UDim2.new(0,30,0,30)
TabsButton.ZIndex = 10

    local TBI1 = Instance.new("Frame",TabsButton)
    TBI1.Size = UDim2.new(UDim.new(0,4),TabsButton.Size.Y-UDim.new(0,4))
    TBI1.ZIndex = 11
    TBI1.BackgroundColor3 = DATA_GUI_COLORS.TabsSelectorButtonText
    TBI1.Name = GRName()
    RoundGui(TBI1,UDim.new(0,Info.RoundSize))
    CenterGuiItem(TBI1)
    local TBI2 = Instance.new("Frame",TabsButton)
    TBI2.Size = UDim2.new(UDim.new(0,4),TabsButton.Size.Y-UDim.new(0,4))
    TBI2.ZIndex = 11
    TBI2.BackgroundColor3 = DATA_GUI_COLORS.TabsSelectorButtonText
    TBI2.Name = GRName()
    RoundGui(TBI2,UDim.new(0,Info.RoundSize))
    CenterGuiItem(TBI2)
    TBI2.Position = TBI2.Position + UDim2.new(0,8,0,0)
    local TBI3 = Instance.new("Frame",TabsButton)
    TBI3.Size = UDim2.new(UDim.new(0,4),TabsButton.Size.Y-UDim.new(0,4))
    TBI3.ZIndex = 11
    TBI3.BackgroundColor3 = DATA_GUI_COLORS.TabsSelectorButtonText
    TBI3.Name = GRName()
    RoundGui(TBI3,UDim.new(0,Info.RoundSize))
    CenterGuiItem(TBI3)
    TBI3.Position = TBI3.Position + UDim2.new(0,-8,0,0)
TabsButton.Position = UDim2.new(0,8,0,5)

local TabsSelectorSF = Instance.new("ScrollingFrame",MainFrame)
TabsSelectorSF.Size = UDim2.new(UDim.new(0,Info.SizeX/2),UDim.new(0,Info.SizeY-TabSelectorOffset))
TabsSelectorSF.BackgroundTransparency = 1
TabsSelectorSF.BorderColor3 = DATA_GUI_COLORS.TabsScrollingFrameBorderColor
TabsSelectorSF.ScrollBarImageColor3 = DATA_GUI_COLORS.TabsScrollingFrameScrollColor
TabsSelectorSF.ZIndex = 9
TabsSelectorSF.CanvasSize = UDim2.new(0,0,0,0)
TabsSelectorSF.AutomaticCanvasSize = Enum.AutomaticSize.Y
TabsSelectorSF.Name = GRName()
TabsSelectorSF.Visible = false
TabsSelectorSF.Position = UDim2.new(-2,0,0,0)
RoundGui(TabsSelectorSF,UDim.new(0,Info.RoundSize))
local UiListLayout = Instance.new("UIListLayout",TabsSelectorSF)
UiListLayout.Name = GRName()
UiListLayout.Padding = UDim.new(0,5)
UiListLayout.FillDirection = 1
UiListLayout.SortOrder = 2
UiListLayout.HorizontalAlignment = 0

local LastTab = nil
local Toggled = false
local IsRunning = false
table.insert(ConnectionsTable,TabsButton.MouseButton1Click:Connect(function()
    if IsRunning == false then
        IsRunning = true
        if Toggled == false then
                Toggled = true
                Tween:Create(TabsButton,TweenInfo.new(0.3,5,2),{Rotation = 90}):Play()
                for _,i in ipairs(Tabs) do
                    if i.TabSF.Visible == true then
                    LastTab = i
                    end
                    coroutine.resume(coroutine.create(function()
                    Tween:Create(i.TabSF,TweenInfo.new(0.3,5,2),{Position = UDim2.new(2,0,0,0)}):Play()
                    wait(1)
                    if i ~= LastTab then
                    i.TabSF.Visible = false
                    end
                    end))
                    
                end
                TabsSelectorSF.Visible = true
                Tween:Create(TabsSelectorSF,TweenInfo.new(0.3,5,2),{Position = UDim2.new(0,0,0,TabSelectorOffset)}):Play()
        elseif Toggled == true then
            Toggled = false
            Tween:Create(TabsButton,TweenInfo.new(0.3,5,2),{Rotation = 0}):Play()
            coroutine.resume(coroutine.create(function()
            Tween:Create(TabsSelectorSF,TweenInfo.new(0.3,5,2),{Position = UDim2.new(-1.5,0,0,0)}):Play()
            wait(1)
            TabsSelectorSF.Visible = false
            end))
            wait(0.3)
            pcall(function()
            LastTab.TabSF.Position = UDim2.new(1.5,0,0,0)
            Tween:Create(LastTab.TabSF,TweenInfo.new(0.3,5,2),{Position = UDim2.new(0,0,0,LastTab.SFOffset)}):Play()
            LastTab.TabSF.Visible = true 
            end)
            
            wait(1)
        end
        IsRunning = false
    end
end))



if Info.SizeTween == true then
    MainFrame:TweenSize(
    UDim2.new(0,Info.SizeX,0,Info.SizeY),
    Info.SizeTweenEasingDirection,
    Info.SizeTweenEasingStyle,
    Info.SizeTweenTime
    )
else
    MainFrame.Size = UDim2.new(0,Info.SizeX,0,Info.SizeY)
end


if Info.CanToggleGui == true then
local Button = Instance.new("TextButton",MainFrame)
Button.Name = GRName()
Button.Visible = false
RoundGui(Button,UDim.new(0,1000000))
Button.Size = UDim2.new(0,30,0,30)
Button.Text = ""
Button.Font = Enum.Font.SciFi
Button.TextSize = 50
Button.TextColor3 = DATA_GUI_COLORS.ToggleGuiButtonText_OPEN
Button.TextWrapped = false
Button.Visible = true
Button.Position = Button.Position + UDim2.new(0.92,0,0.01,0)
Button.BackgroundColor3 = DATA_GUI_COLORS.ToggleGuiButton_OPEN
Button.ZIndex = 10
local Stick1 = Instance.new("Frame",Button)
Stick1.Size = UDim2.new(Button.Size.X-UDim.new(0,4),UDim.new(0,4))
Stick1.ZIndex = 11
Stick1.BorderSizePixel = 0
Stick1.Rotation = 0
Stick1.Name = GRName()
RoundGui(Stick1,UDim.new(0,Info.RoundSize))
CenterGuiItem(Stick1)
local Stick2 = Instance.new("Frame",Button)
Stick2.Size = UDim2.new(Button.Size.X-UDim.new(0,4),UDim.new(0,4))
Stick2.ZIndex = 11
Stick2.BorderSizePixel = 0
Stick2.Rotation = 90
Stick2.Name = GRName()
RoundGui(Stick2,UDim.new(0,Info.RoundSize))
CenterGuiItem(Stick2)

    local function SetButtonOpen()
    Tween:Create(Button,TweenInfo.new(1,7,2),{Rotation = 45}):Play()
    local BTweenGoal = {}
    BTweenGoal.BackgroundColor3 = DATA_GUI_COLORS.ToggleGuiButton_OPEN
    BTweenGoal.Position = UDim2.new(0.92,0,0.01,0)
    local TInfo = TweenInfo.new(2.5,5,2)
    Tween:Create(Button,TInfo,BTweenGoal):Play()
    
    Tween:Create(Stick1,TweenInfo.new(2.5,5,2),{BackgroundColor3 = DATA_GUI_COLORS.ToggleGuiButtonText_OPEN}):Play()
    Tween:Create(Stick2,TweenInfo.new(2.5,5,2),{BackgroundColor3 = DATA_GUI_COLORS.ToggleGuiButtonText_OPEN}):Play()

    local TweenGoal = {}
    TweenGoal.Size = UDim2.new(0,Info.SizeX,0,Info.SizeY)
    local TInfo = TweenInfo.new(2.5,5,2)
    Tween:Create(MainFrame,TInfo,TweenGoal):Play()
    end
    SetButtonOpen()


    local function SetButtonClosed()
    Tween:Create(Button,TweenInfo.new(1,7,2),{ Rotation = 180}):Play()
    local BTweenGoal = {}
    BTweenGoal.BackgroundColor3 = DATA_GUI_COLORS.ToggleGuiButton_CLOSED
    BTweenGoal.Position = UDim2.new(0.92,0,0.07,0)
    local TInfo = TweenInfo.new(2.5,5,2)
    Tween:Create(Button,TInfo,BTweenGoal):Play()

    Tween:Create(Stick1,TweenInfo.new(2.5,5,2),{BackgroundColor3 = DATA_GUI_COLORS.ToggleGuiButtonText_CLOSED}):Play()
    Tween:Create(Stick2,TweenInfo.new(2.5,5,2),{BackgroundColor3 = DATA_GUI_COLORS.ToggleGuiButtonText_CLOSED}):Play()

    
    local TweenGoal = {}
    TweenGoal.Size = UDim2.new(0,Info.SizeX,0,40)
    local TInfo = TweenInfo.new(2.5,5,2)
    Tween:Create(MainFrame,TInfo,TweenGoal):Play()

    end


local Connection = nil
local Toggled = true
Connection = Button.MouseButton1Click:Connect(function()
if Toggled == false then
Toggled = true
SetButtonOpen()
elseif Toggled == true then
Toggled = false
SetButtonClosed()
end
end)
table.insert(ConnectionsTable,Connection)
function WindowFunctions.ToggleShowGuiButton(Bool)
if Bool == true then
        Button.Visible = true
        local Transparency = 100
        for _=1,100 do
        Transparency = Transparency - 1 
        Button.Transparency = Transparency/100
        Stick1.Transparency = Transparency/100
        Stick2.Transparency = Transparency/100
        game:GetService("RunService").RenderStepped:Wait()
        end
elseif Bool == false then
        for _=1,100 do
        Button.Transparency = _/100
        Stick1.Transparency = _/100
        Stick2.Transparency = _/100
        game:GetService("RunService").RenderStepped:Wait()
        end
        Button.Visible = false
end
end



end



local DraggingEnabled = false

if Info.CanDrag == true then
DraggingEnabled = true
end
    function WindowFunctions.SetCanDrag(Bool)
    DraggingEnabled = Bool
    end
    


local Drag = MainFrame
local UserInputService = game:GetService("UserInputService")
	local dragging = nil
	local dragInput = nil
	local dragStart = nil
	local startPos = nil
    local TempConn = nil
	local function update(input)
		local delta = input.Position - dragStart
		local dragTime = 0.04
		local SmoothDrag = {}
		SmoothDrag.Position = UDim2.new(startPos.X.Scale, startPos.X.Offset + delta.X, startPos.Y.Scale, startPos.Y.Offset + delta.Y)
		local dragSmoothFunction = Tween:Create(Drag, TweenInfo.new(dragTime, Enum.EasingStyle.Sine, Enum.EasingDirection.InOut), SmoothDrag)
		dragSmoothFunction:Play()
	end
	table.insert(ConnectionsTable,Drag.InputBegan:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseButton1 or input.UserInputType == Enum.UserInputType.Touch and MAIN_SLIDER_RUNNING == false and DraggingEnabled == true then
			dragging = true
			dragStart = input.Position
			startPos = Drag.Position
			TempConn = input.Changed:Connect(function()
				if input.UserInputState == Enum.UserInputState.End then
					dragging = false
                    TempConn:Disconnect()
				end
			end)
		end
	end))
	table.insert(ConnectionsTable,Drag.InputChanged:Connect(function(input)
		if input.UserInputType == Enum.UserInputType.MouseMovement or input.UserInputType == Enum.UserInputType.Touch then
			dragInput = input
		end
	end))
	table.insert(ConnectionsTable,UserInputService.InputChanged:Connect(function(input)
		if input == dragInput and dragging and Drag.Size then
			update(input)
		end
	end))


-- EFFECTS

if Info.Effect then
if Info.Effect.Type == "Bubbles" then

local Bubbles = {}

    local function Update()
    for _,Item in ipairs(Bubbles) do
    Item.Position = Item.Position + UDim2.new(0,math.random(-2,2),0,-1)
    if Item.AbsolutePosition.Y < MainFrame.AbsolutePosition.Y-(MainFrame.AbsoluteSize.Y/2) then
    Item:Destroy()
    table.remove(Bubbles,_)
    end
    end
    end

    local function AddBubble(StartPos)
    local BFrame = Instance.new("Frame",MainFrame);table.insert(Bubbles,BFrame)
    BFrame.Name = GRName()
    local Size = math.random(Info.Effect.MinSize,Info.Effect.MaxSize)
    BFrame.Size = UDim2.new(0,Size,0,Size)
    BFrame.Position = StartPos

    if Info.Effect.RandomColor == true then
        BFrame.BackgroundColor3 = Color3.fromRGB(math.random(0,255),math.random(0,255),math.random(0,255))
    else
        BFrame.BackgroundColor3 = DATA_GUI_COLORS.BubbleColor
    end
    coroutine.resume(coroutine.create(function()
        local Transparency = 100
        for _=1,100 do
        Transparency = Transparency - 1 
        BFrame.Transparency = Transparency/100
        game:GetService("RunService").RenderStepped:Wait()
        end
    end))

    RoundGui(BFrame,UDim.new(1000,10000))
    end

local SkipRate = Info.Effect.SpawnerSkipRate
local Skip = 0
local MouseIsInside = false
local Activated = true
    table.insert(ConnectionsTable,MainFrame.MouseEnter:Connect(function()
    MouseIsInside = true
    end))

    table.insert(ConnectionsTable,MainFrame.MouseLeave:Connect(function()
    MouseIsInside = false
    end))

table.insert(ConnectionsTable,game:GetService("RunService").RenderStepped:Connect(function()
    if Activated == true then
        local GEP = (MainFrame.AbsolutePosition.X+MainFrame.AbsoluteSize.X)
        local GSP = (MainFrame.AbsolutePosition.X-MainFrame.AbsoluteSize.X)
        local Rand = 0
        if GEP > GSP then
        Rand = math.random(GSP,GEP)
        elseif GSP > GEP then
        Rand = math.random(GEP,GSP)
        end
        Skip = Skip + 1
        if Skip >= SkipRate then

            if Info.Effect.Spawner == true then
                AddBubble(UDim2.new(UDim.new(0,Rand),MainFrame.Size.Y+(UDim.new(0,MainFrame.Size.Y.Offset/2))))
            end

            if Info.Effect.SpawnOnMouse == true and MouseIsInside == true then
                --local V2 = Vector2.new(Mouse.X, Mouse.Y)/Vector2.new(Mouse.ViewSizeX, Mouse.ViewSizeY)
                AddBubble(UDim2.new(0,(Mouse.X-MainFrame.AbsolutePosition.X)+math.random(-50,50),0,(Mouse.Y-MainFrame.AbsolutePosition.Y)+math.random(-50,50)))
            end
            Skip = 0

        end
        Update()
    end
end))

    function WindowFunctions.ClearBubbles()
    for _,i in ipairs(Bubbles) do
    i:Destroy()
    end
    Bubbles = {}
    end

    function WindowFunctions.SetBubbles(Bool)
    Activated = Bool
    WindowFunctions.ClearBubbles()
    end

    function WindowFunctions.SetBubblesOptions(SetInfo)
    Info.Effect = {
        RandomColor = SetInfo.RandomColor,
        SpawnOnMouse = SetInfo.SpawnOnMouse,
        Spawner = SetInfo.Spawner,
        SpawnerSkipRate = SetInfo.SpawnerSkipRate,
        MinSize = SetInfo.MinSize,
        MaxSize = SetInfo.MaxSize
        }
    end


end
end


function WindowFunctions.NewTab(TabInfo)
local Offset = 50
local TabFunctions = {}
local MainScrollingFrame = Instance.new("ScrollingFrame",MainFrame)

local TabIndent = Instance.new("TextButton")
TabIndent.Name = GRName()
TabIndent.Size = UDim2.new(0,TabsSelectorSF.AbsoluteSize.X-50,0,20)
RoundGui(TabIndent,UDim.new(0,Info.RoundSize))
TabIndent.BackgroundColor3 = DATA_GUI_COLORS.TabSelectorButtonBGColor
TabIndent.Parent = TabsSelectorSF
TabIndent.TextWrapped = true
TabIndent.Text = TabInfo.Name
TabIndent.TextColor3 = DATA_GUI_COLORS.TabSelectorButtonTextColor
TabIndent.ZIndex = 11

table.insert(ConnectionsTable,TabIndent.MouseButton1Click:Connect(function()
for _,i in ipairs(Tabs) do
i.TabSF.Visible = false
end
MainScrollingFrame.Visible = true
LastTab = {TabName = TabInfo.TabName,TabSF = MainScrollingFrame,SFOffset = Offset}
end))


local UiListLayout = Instance.new("UIListLayout",MainScrollingFrame)

MainScrollingFrame.Name = GRName()
UiListLayout.Name = GRName()

RoundGui(MainScrollingFrame,UDim.new(0,Info.RoundSize))

MainScrollingFrame.BackgroundTransparency = 1
MainScrollingFrame.AutomaticCanvasSize = Enum.AutomaticSize.Y
MainScrollingFrame.Position = UDim2.new(0,0,0,Offset)
MainScrollingFrame.ZIndex = 15
MainScrollingFrame.ScrollBarImageColor3 = DATA_GUI_COLORS.ScrollingFrameImage
MainScrollingFrame.BorderColor3 = DATA_GUI_COLORS.ScrollingFrameBorder
MainScrollingFrame.CanvasSize = UDim2.new(0,0,0,0)

UiListLayout.Padding = UDim.new(0,5)
UiListLayout.FillDirection = 1
UiListLayout.SortOrder = 2
UiListLayout.HorizontalAlignment = 0


if Info.SizeTween == true then
    MainScrollingFrame:TweenSize(
    UDim2.new(0,Info.SizeX,0,Info.SizeY-Offset),
    Info.SizeTweenEasingDirection,
    Info.SizeTweenEasingStyle,
    Info.SizeTweenTime
    )
else
    MainScrollingFrame.Size = UDim2.new(0,Info.SizeX,0,Info.SizeY-Offset)
end


table.insert(Tabs,{
TabName = TabInfo.TabName,
TabSF = MainScrollingFrame,
SFOffset = Offset
})

function TabFunctions.Label(LabelInfo)
local LabelFuncs = {}
local Label = Instance.new("TextLabel",MainScrollingFrame)
Label.Name = GRName()
Label.Size = UDim2.new(0,Info.SizeX-50,0,20)
Label.Text = LabelInfo.Text
Label.TextWrapped = true
RoundGui(Label,UDim.new(0,Info.RoundSize))
Label.TextColor3 = DATA_GUI_COLORS.ITEM_LabelTextColor
Label.BackgroundColor3 = DATA_GUI_COLORS.ITEM_LabelBGColor
Label.ZIndex = 11

function LabelFuncs:UpdateText(Text)
    Label.Text = Text
end

function LabelFuncs:GetText()
    return Label.Text
end


function LabelFuncs:Toggle(Bool)
    if Bool == true then
        Label.Visible = true
    elseif Bool == false then
        Label.Visible = false
    end
end

    return LabelFuncs
end

function TabFunctions.Button(ButtonInfo)
    local ButtonFuncs = {}
    local Button = Instance.new("TextButton",MainScrollingFrame)
    Button.Name = GRName()
    Button.Size = UDim2.new(0,Info.SizeX-50,0,30)
    Button.Text = ButtonInfo.Text
    RoundGui(Button,UDim.new(0,Info.RoundSize))
    Button.TextColor3 = DATA_GUI_COLORS.ITEM_ButtonTextColor
    Button.BackgroundColor3 = DATA_GUI_COLORS.ITEM_ButtonBGColor
    Button.ZIndex = 11
    local CurrentConnection = nil
    if ButtonInfo.Callback then
        CurrentConnection = Button.MouseButton1Click:Connect(ButtonInfo.Callback)
        table.insert(ConnectionsTable,CurrentConnection)
    end


    function ButtonFuncs:UpdateText(Text)
    Button.Text = Text
    end
    function ButtonFuncs:ForceFire()
    if ButtonInfo.Callback then
    ButtonInfo.Callback()
    end
    end

    function ButtonFuncs:Disconnect()
    if CurrentConnection then
    CurrentConnection:Disconnect()
    CurrentConnection = nil
    end
    end

    function ButtonFuncs:Reconnect(func)
        if not CurrentConnection then
            if func then
                CurrentConnection = Button.MouseButton1Click:Connect(func)
                table.insert(ConnectionsTable,CurrentConnection)
            end
        end
    end

    function ButtonFuncs:GetText()
    return Button.Text
    end

    function ButtonFuncs:Toggle(Bool)
        if Bool == true then
            Button.Visible = true
        elseif Bool == false then
            Button.Visible = false
        end
    end

    return ButtonFuncs
end


function TabFunctions.Toggle(ToggleInfo)
    local ToggleFuncs = {}
    local CurrentStatus = false

    local ToggleMainFrame = Instance.new("Frame",MainScrollingFrame)
    ToggleMainFrame.Name = GRName()
    ToggleMainFrame.Size = UDim2.new(0,Info.SizeX-50,0,30)
    RoundGui(ToggleMainFrame,UDim.new(0,Info.RoundSize))
    ToggleMainFrame.BackgroundColor3 = DATA_GUI_COLORS.ITEM_MainToggleFrameBGColor
    ToggleMainFrame.ZIndex = 11
    local ToggleMainTextFrame = Instance.new("TextLabel",ToggleMainFrame)
    ToggleMainTextFrame.Name = GRName()
    ToggleMainTextFrame.Size = UDim2.new(0,Info.SizeX-80,0,30)
    RoundGui(ToggleMainTextFrame,UDim.new(0,Info.RoundSize))
    ToggleMainTextFrame.BackgroundTransparency = 1
    ToggleMainTextFrame.ZIndex = 11
    ToggleMainTextFrame.Text = ToggleInfo.Text
    ToggleMainTextFrame.TextColor3 = DATA_GUI_COLORS.ITEM_MainToggleTextColor
    local TFTB = Instance.new("TextButton",ToggleMainFrame)
    TFTB.Name = GRName()
    TFTB.Size = UDim2.new(0,25,0,25)
    RoundGui(TFTB,UDim.new(0,100000))
    TFTB.BackgroundColor3 = DATA_GUI_COLORS.ITEM_ToggleColorStyleOff
    TFTB.ZIndex = 11
    TFTB.Position = UDim2.new(0,(ToggleMainTextFrame.AbsoluteSize.X),0.5,math.round((TFTB.AbsoluteSize.Y/2)*-1))
    TFTB.AutoButtonColor = false
    local CBFunc = nil
    if ToggleInfo.Callback then
    CBFunc = ToggleInfo.Callback
    end
    local Locked = false
    table.insert(ConnectionsTable,TFTB.MouseButton1Click:Connect(function()
    if CurrentStatus == true and Locked == false then
    CurrentStatus = false
    Tween:Create(TFTB,TweenInfo.new(0.5,Enum.EasingStyle.Quint,Enum.EasingDirection.InOut),{BackgroundColor3 = DATA_GUI_COLORS.ITEM_ToggleColorStyleOff}):Play()
    elseif CurrentStatus == false and Locked == false then
    CurrentStatus = true
    Tween:Create(TFTB,TweenInfo.new(0.5,Enum.EasingStyle.Quint,Enum.EasingDirection.InOut),{BackgroundColor3 = DATA_GUI_COLORS.ITEM_ToggleColorStyleOn}):Play()
    end
    if CBFunc ~= nil then
    CBFunc(CurrentStatus)
    end
    end))
    
    function ToggleFuncs:SetState(Bool)
    if Bool == true then
    CurrentStatus = false
    Tween:Create(TFTB,TweenInfo.new(0.5,Enum.EasingStyle.Quint,Enum.EasingDirection.InOut),{BackgroundColor3 = DATA_GUI_COLORS.ITEM_ToggleColorStyleOff}):Play()
    elseif Bool == false then
    CurrentStatus = true
    Tween:Create(TFTB,TweenInfo.new(0.5,Enum.EasingStyle.Quint,Enum.EasingDirection.InOut),{BackgroundColor3 = DATA_GUI_COLORS.ITEM_ToggleColorStyleOn}):Play()
    end
    if CBFunc ~= nil then
    CBFunc(CurrentStatus)
    end
    end
    function ToggleFuncs:Toggle(Bool)
        if Bool == true then
            ToggleMainFrame.Visible = true
        elseif Bool == false then
            ToggleMainFrame.Visible = false
        end
    end
    function ToggleFuncs:LockToggle(Bool)
    Locked = Bool
    end

    return ToggleFuncs
end

function TabFunctions.ViewportFrame(ViewInfo)
    local ViewPortFuncs = {}
    local VPMainFrame = Instance.new("Frame",MainScrollingFrame)
    VPMainFrame.Name = GRName()
    VPMainFrame.Size = UDim2.new(0,Info.SizeX-50,0,ViewInfo.SizeY)
    RoundGui(VPMainFrame,UDim.new(0,Info.RoundSize))
    VPMainFrame.BackgroundColor3 = DATA_GUI_COLORS.ITEM_ViewportFrameFrameColor
    VPMainFrame.ZIndex = 11
    local VPF = Instance.new("ViewportFrame",VPMainFrame)
    VPF.Name = GRName()
    if ViewInfo.UserAbsoluteControl == true then
    VPF.Size = UDim2.new(0,Info.SizeX-50,0,ViewInfo.SizeY-70)
    else
    VPF.Size = UDim2.new(0,Info.SizeX-50,0,ViewInfo.SizeY-30)
    end
    RoundGui(VPF,UDim.new(0,Info.RoundSize))
    VPF.BackgroundTransparency = 1
    VPF.ZIndex = 11
    local CurrentZoomLabel = Instance.new("TextLabel",VPMainFrame)
    CurrentZoomLabel.BackgroundTransparency = 1
    CurrentZoomLabel.Size = UDim2.new(0,20,0,10)
    CurrentZoomLabel.TextColor3 = DATA_GUI_COLORS.ITEM_ViewportFrameZoomLabelColor
    CurrentZoomLabel.Position = UDim2.new(0,CurrentZoomLabel.AbsoluteSize.X,0,(VPF.AbsoluteSize.Y*1)+CurrentZoomLabel.AbsoluteSize.Y)
    CurrentZoomLabel.ZIndex = 11
    CurrentZoomLabel.Name = GRName()
    local ZoomPlusButton = nil
    local ZoomSubButton = nil
    local RotZPlusButton = nil
    local RotZSubButton = nil
    local RotYPlusButton = nil
    local RotYSubButton = nil

    if ViewInfo.UserAbsoluteControl == true then
        ZoomPlusButton = Instance.new("TextButton",VPMainFrame)
        ZoomPlusButton.Size = UDim2.new(0,30,0,30)
        ZoomPlusButton.Position = UDim2.new(0,(CurrentZoomLabel.AbsoluteSize.Y)/2,0,(VPF.AbsoluteSize.Y*1)+(ZoomPlusButton.AbsoluteSize.Y+(CurrentZoomLabel.AbsoluteSize.Y)/2))
        ZoomPlusButton.ZIndex = 11
        ZoomPlusButton.BackgroundColor3 = DATA_GUI_COLORS.ITEM_ViewportFrameZoomButtonAddBGColor
        ZoomPlusButton.TextColor3 = DATA_GUI_COLORS.ITEM_ViewportFrameZoomButtonAddTextColor
        ZoomPlusButton.Name = GRName()
        ZoomPlusButton.Text = "+"
        ZoomPlusButton.TextSize = 19
        ZoomPlusButton.TextWrapped = false
        RoundGui(ZoomPlusButton,UDim.new(0,Info.RoundSize))
        ZoomSubButton = Instance.new("TextButton",VPMainFrame)
        ZoomSubButton.Size = UDim2.new(0,30,0,30)
        ZoomSubButton.Position = UDim2.new(0,((CurrentZoomLabel.AbsoluteSize.Y)/2)+ZoomPlusButton.AbsoluteSize.X+3,0,(VPF.AbsoluteSize.Y*1)+(ZoomPlusButton.AbsoluteSize.Y+(CurrentZoomLabel.AbsoluteSize.Y)/2))
        ZoomSubButton.ZIndex = 11
        ZoomSubButton.BackgroundColor3 = DATA_GUI_COLORS.ITEM_ViewportFrameZoomButtonSubBGColor
        ZoomSubButton.TextColor3 = DATA_GUI_COLORS.ITEM_ViewportFrameZoomButtonSubTextColor
        ZoomSubButton.Name = GRName()
        ZoomSubButton.Text = "-"
        ZoomSubButton.TextSize = 19
        ZoomSubButton.TextWrapped = false
        RoundGui(ZoomSubButton,UDim.new(0,Info.RoundSize))

        RotZPlusButton = Instance.new("TextButton",VPMainFrame)
        RotZPlusButton.Size = UDim2.new(0,30,0,30)
        RotZPlusButton.Position = UDim2.new(0.21,0,0,(VPF.AbsoluteSize.Y*1)+(ZoomPlusButton.AbsoluteSize.Y+(CurrentZoomLabel.AbsoluteSize.Y)/2))
        RotZPlusButton.ZIndex = 11
        RotZPlusButton.BackgroundColor3 = DATA_GUI_COLORS.ITEM_ViewportFrameZMoveAddButtonBGColor
        RotZPlusButton.TextColor3 = DATA_GUI_COLORS.ITEM_ViewportFrameZMoveAddButtonTextColor
        RotZPlusButton.Name = GRName()
        RotZPlusButton.Text = "<"
        RotZPlusButton.TextSize = 19
        RotZPlusButton.TextWrapped = false
        RoundGui(RotZPlusButton,UDim.new(0,Info.RoundSize))
        RotZSubButton = Instance.new("TextButton",VPMainFrame)
        RotZSubButton.Size = UDim2.new(0,30,0,30)
        RotZSubButton.Position = UDim2.new(0.21,RotZSubButton.AbsoluteSize.X+3,0,(VPF.AbsoluteSize.Y*1)+(ZoomPlusButton.AbsoluteSize.Y+(CurrentZoomLabel.AbsoluteSize.Y)/2))
        RotZSubButton.ZIndex = 11
        RotZSubButton.BackgroundColor3 = DATA_GUI_COLORS.ITEM_ViewportFrameZMoveSubButtonBGColor
        RotZSubButton.TextColor3 = DATA_GUI_COLORS.ITEM_ViewportFrameZMoveSubButtonTextColor
        RotZSubButton.Name = GRName()
        RotZSubButton.Text = ">"
        RotZSubButton.TextSize = 19
        RotZSubButton.TextWrapped = false
        RoundGui(RotZSubButton,UDim.new(0,Info.RoundSize))

        RotYPlusButton = Instance.new("TextButton",VPMainFrame)
        RotYPlusButton.Size = UDim2.new(0,30,0,30)
        RotYPlusButton.Position = UDim2.new(0.41,0,0,(VPF.AbsoluteSize.Y*1)+(ZoomPlusButton.AbsoluteSize.Y+(CurrentZoomLabel.AbsoluteSize.Y)/2))
        RotYPlusButton.ZIndex = 11
        RotYPlusButton.BackgroundColor3 = DATA_GUI_COLORS.ITEM_ViewportFrameYMoveAddButtonBGColor
        RotYPlusButton.TextColor3 = DATA_GUI_COLORS.ITEM_ViewportFrameYMoveAddButtonTextColor
        RotYPlusButton.Name = GRName()
        RotYPlusButton.Text = "<"
        RotYPlusButton.Rotation = 90
        RotYPlusButton.TextSize = 19
        RotYPlusButton.TextWrapped = false
        RoundGui(RotYPlusButton,UDim.new(0,Info.RoundSize))
        RotYSubButton = Instance.new("TextButton",VPMainFrame)
        RotYSubButton.Size = UDim2.new(0,30,0,30)
        RotYSubButton.Position = UDim2.new(0.41,RotYSubButton.AbsoluteSize.X+3,0,(VPF.AbsoluteSize.Y*1)+(ZoomPlusButton.AbsoluteSize.Y+(CurrentZoomLabel.AbsoluteSize.Y)/2))
        RotYSubButton.ZIndex = 11
        RotYSubButton.BackgroundColor3 = DATA_GUI_COLORS.ITEM_ViewportFrameYMoveSubButtonBGColor
        RotYSubButton.TextColor3 = DATA_GUI_COLORS.ITEM_ViewportFrameYMoveSubButtonTextColor
        RotYSubButton.Name = GRName()
        RotYSubButton.Text = ">"
        RotYSubButton.Rotation = 90
        RotYSubButton.TextSize = 19
        RotYSubButton.TextWrapped = false
        RoundGui(RotYSubButton,UDim.new(0,Info.RoundSize))
    end

    local Idle = true
    local IsMouseInside = false
    local ZoomSubtraction = 0
    local CameraUpdatingConnections = {}
    local InstancesTable = {}
    local InstanceUpdateConnTable = {}
    local A1UPDTR = 0
    local CamYRot = -35
    local Change = 5
    local VPFCam = Instance.new("Camera",VPF)
    VPFCam.Name = GRName()
    VPF.CurrentCamera = VPFCam
    local MainModel = Instance.new("Model",VPF)
    MainModel.Name = GRName()
    for _,i in pairs(ViewInfo.Items) do
    pcall(function()
    local Cloned = i:Clone()
    Cloned.Name = GRName()
    Cloned.Parent = MainModel
    end)
    end
    local CamZoomPlusUpdater = nil
    local CamZoomSubUpdater = nil
    local CamZSubUpdater = nil
    local CamZPlusUpdater = nil
    local CamYSubUpdater = nil
    local CamYPlusUpdater = nil
    local MouseIdleEnter = nil
    local MouseIdleLeave = nil
    if ViewInfo.UserAbsoluteControl == true then

        CamYSubUpdater = RotYSubButton.MouseButton1Click:Connect(function()
        CamYRot = CamYRot + Change
        end)
        table.insert(ConnectionsTable,CamYSubUpdater)
        table.insert(CameraUpdatingConnections,CamYSubUpdater)

        CamYPlusUpdater = RotYPlusButton.MouseButton1Click:Connect(function()
        CamYRot = CamYRot - Change
        end)
        table.insert(ConnectionsTable,CamYPlusUpdater)
        table.insert(CameraUpdatingConnections,CamYPlusUpdater)

        CamZSubUpdater = RotZSubButton.MouseButton1Click:Connect(function()
        A1UPDTR = A1UPDTR + Change
        end)
        table.insert(ConnectionsTable,CamZSubUpdater)
        table.insert(CameraUpdatingConnections,CamZSubUpdater)

        CamZPlusUpdater = RotZPlusButton.MouseButton1Click:Connect(function()
        A1UPDTR = A1UPDTR - Change
        end)
        table.insert(ConnectionsTable,CamZPlusUpdater)
        table.insert(CameraUpdatingConnections,CamZPlusUpdater)



        CamZoomPlusUpdater = ZoomPlusButton.MouseButton1Click:Connect(function()
        ZoomSubtraction = ZoomSubtraction - Change
        end)
        table.insert(ConnectionsTable,CamZoomPlusUpdater)
        table.insert(CameraUpdatingConnections,CamZoomPlusUpdater)

        CamZoomSubUpdater = ZoomSubButton.MouseButton1Click:Connect(function()
        ZoomSubtraction = ZoomSubtraction + Change
        end)
        table.insert(ConnectionsTable,CamZoomSubUpdater)
        table.insert(CameraUpdatingConnections,CamZoomSubUpdater)

        MouseIdleEnter = VPMainFrame.MouseEnter:Connect(function()
        Idle = false
        end)
        table.insert(ConnectionsTable,MouseIdleEnter)
        table.insert(CameraUpdatingConnections,MouseIdleEnter)

        MouseIdleLeave = VPMainFrame.MouseLeave:Connect(function()
        Idle = true
        end)
        table.insert(ConnectionsTable,MouseIdleLeave)
        table.insert(CameraUpdatingConnections,MouseIdleLeave)

    end


    local CamMovementUpdater = nil
    CamMovementUpdater = game:GetService("RunService").RenderStepped:Connect(function()

    local MCF, MS = MainModel:GetBoundingBox()

        
    local RotInv = (MCF - MCF.Position):Inverse()
    MCF = MCF * RotInv
    MS = RotInv * MS
    MS = Vector3.new(math.abs(MS.X), math.abs(MS.Y), math.abs(MS.Z))
        
    local Diagonal = 0
    local MaxExtent = math.max(MS.x, MS.y, MS.z)
    local Tan = math.tan(math.rad(VPFCam.FieldOfView/2))
        
    if (MaxExtent == MS.x) then
        Diagonal = math.sqrt(MS.Y*MS.Y + MS.Z*MS.Z)/2
    elseif (MaxExtent == MS.y) then
        Diagonal = math.sqrt(MS.X*MS.X + MS.Z*MS.Z)/2
    else
        Diagonal = math.sqrt(MS.X*MS.X + MS.Y*MS.Y)/2
    end
        
    local MinDist = (MaxExtent/2)/Tan + Diagonal

    CurrentZoomLabel.Position = UDim2.new(0,CurrentZoomLabel.TextBounds.X/2,0,(VPF.AbsoluteSize.Y*1)+CurrentZoomLabel.AbsoluteSize.Y)

    local Zoom = math.round((MinDist + 3)+ZoomSubtraction)
    if ViewInfo.ShowZoomLabel == true then
    CurrentZoomLabel.Text = "Current Zoom: " .. tostring(Zoom)
    else
    CurrentZoomLabel.Text = ""
    end
    if ViewInfo.RotateCameraWhenIdle == true and Idle == true then
    A1UPDTR = A1UPDTR + 0.1
    VPFCam.CFrame = MCF * CFrame.fromEulerAnglesYXZ(math.rad(CamYRot), math.rad(A1UPDTR), 0) * CFrame.new(0, 0, Zoom)
    else
    VPFCam.CFrame = MCF * CFrame.fromEulerAnglesYXZ(math.rad(CamYRot), math.rad(A1UPDTR), 0) * CFrame.new(0, 0, Zoom)
    end
    if A1UPDTR >= 360 then
    A1UPDTR = 0
    end
    if CamYRot >= 360 then
    CamYRot = 0
    end



    end)

    table.insert(ConnectionsTable,CamMovementUpdater)
    table.insert(CameraUpdatingConnections,CamMovementUpdater)

    function ViewPortFuncs:Toggle(Bool)
            if Bool == true then
                VPMainFrame.Visible = true
            elseif Bool == false then
                VPMainFrame.Visible = false
            end
    end
    function ViewPortFuncs:ClearModel()
    for _,i in ipairs(MainModel:GetChildren()) do
    pcall(function()
    i:Destroy()
    end)
    end
    end
    function ViewPortFuncs:SetItems(Items)
    ViewPortFuncs:ClearModel()
    for _,i in pairs(Items) do
    pcall(function()
    local Cloned = i:Clone()
    Cloned.Name = GRName()
    Cloned.Parent = MainModel
    end)
    end

    end

    function ViewPortFuncs:SetSensibility(S)
    Change = S
    end
    function ViewPortFuncs:GetSensibility()
    return Change
    end
    function ViewPortFuncs:GetZoom()
    return Zoom
    end
    function ViewPortFuncs:SetZoom(Val)
    Zoom = Val
    end


    return ViewPortFuncs
end

function TabFunctions.Dropdown(DropDownInfo)
local DropDownFuncs = {}
local MainFrame = Instance.new("Frame",MainScrollingFrame)
MainFrame.Size = UDim2.new(0,Info.SizeX-50,0,30)
MainFrame.BackgroundColor3 = DATA_GUI_COLORS.ITEM_DropdownFrameColor
RoundGui(MainFrame,UDim.new(0,Info.RoundSize))
MainFrame.ZIndex = 11
MainFrame.Name = GRName()
local Label = Instance.new("TextLabel",MainFrame)
local Button = Instance.new("TextButton",MainFrame)
Button.Size = UDim2.new(0,25,0,25)
Button.BackgroundColor3 = DATA_GUI_COLORS.ITEM_DropdownButtonBGColorDeactivated
Button.Position = UDim2.new(0,(MainFrame.AbsoluteSize.X)-Button.AbsoluteSize.X-5,0.5,(Button.AbsoluteSize.Y/2)*-1)
RoundGui(Button,UDim.new(0,Info.RoundSize))
Button.ZIndex = 13
Button.Name = GRName()
Label.Size = MainFrame.Size - UDim2.new(Button.Size.X,UDim.new(0,0))
Label.ZIndex = 13
Label.Text = DropDownInfo.PlaceHolderText
Label.BackgroundTransparency = 1
Label.TextColor3 = DATA_GUI_COLORS.ITEM_DropdownTextColor
Label.Name = GRName()
RoundGui(Label,UDim.new(0,Info.RoundSize))

local S1 = Instance.new("Frame",Button)
S1.Size = UDim2.new(0,4,0,Button.AbsoluteSize.Y-5)
RoundGui(S1,UDim.new(0,Info.RoundSize))
CenterGuiItem(S1)
S1.Rotation = 90
S1.ZIndex = 13
S1.BackgroundColor3 = DATA_GUI_COLORS.ITEM_DropdownButtonIconColorDeactivated
S1.Name = GRName()
local S2 = Instance.new("Frame",Button)
S2.Size = UDim2.new(0,4,0,Button.AbsoluteSize.X-5)
RoundGui(S2,UDim.new(0,Info.RoundSize))
CenterGuiItem(S2)
S2.Rotation = 0
S2.ZIndex = 13
S2.BackgroundColor3 = DATA_GUI_COLORS.ITEM_DropdownButtonIconColorDeactivated
S2.Name = GRName()
local ListFrame = Instance.new("Frame",MainFrame)
ListFrame.ZIndex = 12
ListFrame.Size = UDim2.new(0,0,0,0)--UDim2.new(0,Info.SizeX-50,0,Info.SizeY-30)
ListFrame.Position = UDim2.new(0,0,0,0)
ListFrame.Name = GRName()
ListFrame.BackgroundColor3 = DATA_GUI_COLORS.ITEM_DropdownScrollingFrameColor
ListFrame.AutomaticSize = Enum.AutomaticSize.Y
ListFrame.ClipsDescendants = true
ListFrame.Visible = false
RoundGui(ListFrame,UDim.new(0,Info.RoundSize))
local SizePlaceHolder = Instance.new("Frame",ListFrame)
SizePlaceHolder.Size = UDim2.new(MainFrame.Size.X,MainFrame.Size.Y)
SizePlaceHolder.Transparency = 1
SizePlaceHolder.Name = GRName()
local UiListLayout = Instance.new("UIListLayout",ListFrame)
UiListLayout.Padding = UDim.new(0,5)
UiListLayout.FillDirection = 1
UiListLayout.SortOrder = 2
UiListLayout.HorizontalAlignment = 0
UiListLayout.Name = GRName()



local ItemsTable = {}
local Selected = ""
function AddItem(Name)

local Button = Instance.new("TextButton",ListFrame) 
Button.BackgroundColor3 = DATA_GUI_COLORS.ITEM_DropdownItemBackgroundColor
Button.Text = Name
Button.Name = GRName()
RoundGui(Button,UDim.new(0,Info.RoundSize))
Button.Size = UDim2.new(UDim.new(MainFrame.Size.X.Scale,MainFrame.Size.X.Offset/1.1),MainFrame.Size.Y)
Button.TextColor3 = DATA_GUI_COLORS.ITEM_DropdownItemTextColor
Button.ZIndex = 14
local Conn = Button.MouseButton1Click:Connect(function()
DropDownInfo.Callback(Name)
Label.Text = DropDownInfo.Text .. Name
Selected = Name
end)

table.insert(ItemsTable,{Button,Name,Conn})
end

for _,i in pairs(DropDownInfo.Options) do
AddItem(i)
end

local Toggled = false
local IsOnCycle = false
local ButtonConn = Button.MouseButton1Click:Connect(function()
if IsOnCycle == false then
IsOnCycle = true
if Toggled == true then
Toggled = false
Tween:Create(S1,TweenInfo.new(1,5,2),{ Rotation = 90,BackgroundColor3 = DATA_GUI_COLORS.ITEM_DropdownButtonIconColorDeactivated}):Play()
Tween:Create(S2,TweenInfo.new(1,5,2),{ Rotation = 0,BackgroundColor3 = DATA_GUI_COLORS.ITEM_DropdownButtonIconColorDeactivated}):Play()
Tween:Create(Button,TweenInfo.new(1,5,2),{BackgroundColor3 = DATA_GUI_COLORS.ITEM_DropdownButtonBGColorDeactivated}):Play()
Tween:Create(ListFrame,TweenInfo.new(1,5,2),{Size = UDim2.new(0,0,0,0)}):Play()
wait(0.65)
ListFrame.Visible = false
elseif Toggled == false then
Toggled = true
Tween:Create(S1,TweenInfo.new(1,5,2),{ Rotation = -45,BackgroundColor3 = DATA_GUI_COLORS.ITEM_DropdownButtonIconColorActivated}):Play()
Tween:Create(S2,TweenInfo.new(1,5,2),{ Rotation = -135,BackgroundColor3 = DATA_GUI_COLORS.ITEM_DropdownButtonIconColorActivated}):Play()
Tween:Create(Button,TweenInfo.new(1,5,2),{BackgroundColor3 = DATA_GUI_COLORS.ITEM_DropdownButtonBGColorActivated}):Play()
Tween:Create(ListFrame,TweenInfo.new(1,5,2),{Size = UDim2.new(0,Info.SizeX-50,0,Info.SizeY-30)}):Play()
ListFrame.Visible = true
wait(1)

end
IsOnCycle = false
end
end)
table.insert(ConnectionsTable,ButtonConn)

function DropDownFuncs:Update(NewItems)
    for _,i in ipairs(ItemsTable) do
    local Button,Name,Connection = table.unpack(i)
    pcall(function()
    Button:Destroy()
    Connection:Disconnect()
    end)
    end
    ItemsTable = {}
    for _,i in pairs(NewItems) do
    AddItem(i)
    end

end
function DropDownFuncs:Add(NewItem)
AddItem(NewItem)
end
function DropDownFuncs:Clear()

    for _,i in ipairs(ItemsTable) do
    local Button,Name,Connection = table.unpack(i)
    pcall(function()
    Button:Destroy()
    Connection:Disconnect()
    end)
    end
    ItemsTable = {}
end
function DropDownFuncs:SetText(Text)
Label.Text = Text
end
function DropDownFuncs:GetText(Text)
return Label.Text
end

function DropDownFuncs:GetSelected()
return Selected
end

function DropDownFuncs:Toggle(Bool)
            if Bool == true then
                MainFrame.Visible = true
            elseif Bool == false then
                MainFrame.Visible = false
            end
end


return DropDownFuncs
end



function TabFunctions.Slider(SliderInfo)
local SliderFuncs = {}

local MainFrame = Instance.new("Frame",MainScrollingFrame)
MainFrame.Size = UDim2.new(0,Info.SizeX-50,0,30)
MainFrame.BackgroundColor3 = DATA_GUI_COLORS.ITEM_SliderMainFrameBGColor
RoundGui(MainFrame,UDim.new(0,Info.RoundSize))
MainFrame.ZIndex = 11
MainFrame.Name = GRName()
local SliderTextInfo = Instance.new("TextLabel",MainFrame) 
SliderTextInfo.Size = UDim2.new(0,Info.SizeX-50,0,20)
SliderTextInfo.TextColor3 = DATA_GUI_COLORS.ITEM_SliderMainTextColor
RoundGui(SliderTextInfo,UDim.new(0,Info.RoundSize))
SliderTextInfo.ZIndex = 11
SliderTextInfo.Name = GRName()
SliderTextInfo.BackgroundTransparency = 1
SliderTextInfo.Text = SliderInfo.Text
local SliderFrame = Instance.new("Frame",MainFrame)
SliderFrame.Size = UDim2.new(0,Info.SizeX-80,0,3)
SliderFrame.BackgroundColor3 = DATA_GUI_COLORS.ITEM_SliderInnerFrameColor
RoundGui(SliderFrame,UDim.new(0,Info.RoundSize))
SliderFrame.ZIndex = 11
SliderFrame.Name = GRName()
CenterGuiItem(SliderFrame)
SliderFrame.Position = SliderFrame.Position - UDim2.new(0,0,0,-5)
local SliderPoint = Instance.new("TextButton",SliderFrame)
SliderPoint.Size = UDim2.new(0,12,0,12)
SliderPoint.Position = UDim2.new(0,0,0.5,-(12/2))
SliderPoint.BackgroundColor3 = DATA_GUI_COLORS.ITEM_SliderSelectorStartColor
RoundGui(SliderPoint,UDim.new(0,Info.RoundSize))
SliderPoint.ZIndex = 11
SliderPoint.Name = GRName()
local SliderText = Instance.new("TextLabel",SliderPoint)
SliderText.Size = UDim2.new(0,80,0,25)
SliderText.Position = UDim2.new(0.5,-25,-3,0)
SliderText.BackgroundColor3 = DATA_GUI_COLORS.ITEM_SliderSelectorTextBGColor
RoundGui(SliderText,UDim.new(0,Info.RoundSize))
SliderText.ZIndex = 13
SliderText.Name = GRName()
SliderText.Text = "0|0%"
SliderText.Visible = false
SliderText.TextColor3 = DATA_GUI_COLORS.ITEM_SliderSelectorTextColor
--SliderText.AutomaticSize = Enum.AutomaticSize.XY

function ModdedRound(num)
return math.round(num*10)/10
end
local Sliding = false
local CurrentVal = SliderInfo.Min
table.insert(ConnectionsTable,Mouse.Move:Connect(function()
if Sliding == true then
local XOffset = Mouse.X-SliderFrame.AbsolutePosition.X-(SliderPoint.AbsoluteSize.X/2)
local ClampMaxVal = SliderFrame.AbsoluteSize.X-SliderPoint.AbsoluteSize.X
local Clamped = math.clamp(XOffset,0,ClampMaxVal)
SliderPoint.Position = UDim2.new(UDim.new(0,Clamped),SliderPoint.Position.Y)
local ToLerpValue = Clamped/ClampMaxVal

local CLRS = DATA_GUI_COLORS.ITEM_SliderSelectorStartColor
local SR,SG,SB = CLRS.R,CLRS.G,CLRS.B
local CLRE = DATA_GUI_COLORS.ITEM_SliderSelectorEndColor
local ER,EG,EB = CLRE.R,CLRE.G,CLRE.B
local FR,FG,FB = Lerp(SR,ER,ToLerpValue),Lerp(SG,EG,ToLerpValue),Lerp(SB,EB,ToLerpValue)
SliderPoint.BackgroundColor3 = Color3.new(FR,FG,FB)
CurrentVal = Lerp(SliderInfo.Min,SliderInfo.Max,ToLerpValue)
SliderInfo.Callback(CurrentVal)
SliderText.Text = tostring(math.round(CurrentVal)) .. "|" .. tostring(ModdedRound(ToLerpValue * 100)) .. "%"
Tween:Create(SliderText,TweenInfo.new(0.3,5,2),{Size = UDim2.new(0,SliderText.TextBounds.X+8,0,25)}):Play()
if SliderText.TextBounds.X - 15 > SliderText.AbsoluteSize.X then
SliderText.Size = UDim2.new(0,SliderText.TextBounds.X+8,0,25)
end
end
end))
table.insert(ConnectionsTable,SliderPoint.MouseButton1Down:Connect(function()
Sliding = true
MAIN_SLIDER_RUNNING = true
SliderText.Transparency = 1
SliderText.Visible = true
Tween:Create(SliderText,TweenInfo.new(0.3,5,2),{Transparency = 0}):Play()
wait(0.35)
end))
table.insert(ConnectionsTable,Mouse.Button1Up:Connect(function()
Sliding = false
MAIN_SLIDER_RUNNING = false
SliderText.Transparency = 0
Tween:Create(SliderText,TweenInfo.new(0.3,5,2),{Transparency = 1}):Play()
wait(0.35)
SliderText.Visible = false
end))
table.insert(ConnectionsTable,SliderPoint.MouseButton1Up:Connect(function()
Sliding = false
MAIN_SLIDER_RUNNING = false
SliderText.Transparency = 0
Tween:Create(SliderText,TweenInfo.new(0.3,5,2),{Transparency = 1}):Play()
wait(0.35)
SliderText.Visible = false
end))

function SliderFuncs.GetText()
return SliderTextInfo.Text
end

function SliderFuncs.SetText(NewText)
SliderTextInfo.Text = NewText
end

function SliderFuncs.GetValue()
return CurrentVal
end
--[[

ITEM_SliderSelectorTextBGColor = Color3.fromRGB(30,30,30),
ITEM_SliderSelectorTextColor = Color3.fromRGB(255,255,255),
--]]

return SliderFuncs
end

function TabFunctions.TextBox(TextBoxInfo)

local MainFrame = Instance.new("TextBox",MainScrollingFrame)
MainFrame.Size = UDim2.new(0,Info.SizeX-50,0,30)
MainFrame.BackgroundColor3 = DATA_GUI_COLORS.ITEM_SliderTextBoxBGColor
RoundGui(MainFrame,UDim.new(0,Info.RoundSize))
MainFrame.ZIndex = 11
MainFrame.Name = GRName()
MainFrame.TextColor3 = DATA_GUI_COLORS.ITEM_SliderTextBoxTextColor
MainFrame.PlaceholderColor3 = DATA_GUI_COLORS.ITEM_SliderTextBoxPlaceHolderColor
MainFrame.PlaceholderText = TextBoxInfo.PlaceholderText
MainFrame.Text = TextBoxInfo.Text
MainFrame.ClipsDescendants = true
MainFrame.TextWrapped = true
table.insert(ConnectionsTable,MainFrame.FocusLost:Connect(function(PressedEnter,Ins)
TextBoxInfo.Callback(MainFrame.Text,PressedEnter,Ins)
end))

end



return TabFunctions
end









function WindowFunctions.ToggleWindow(Bool)
if Bool == true then

if Info.SizeTween == true then
    MainScreen.Enabled = true
    MainFrame:TweenSize(
    UDim2.new(0,Info.SizeX,0,Info.SizeY),
    Info.SizeTweenEasingDirection,
    Info.SizeTweenEasingStyle,
    Info.SizeTweenTime
    )
    wait(Info.SizeTweenTime)
else
    MainScreen.Enabled = true
    MainFrame.Size = UDim2.new(0,Info.SizeX,0,Info.SizeY)
end
if WindowFunctions.ToggleShowGuiButton then
WindowFunctions.ToggleShowGuiButton(true)
end
elseif Bool == false then
if WindowFunctions.ToggleShowGuiButton then
WindowFunctions.ToggleShowGuiButton(false)
end

if Info.SizeTween == true then
    MainFrame:TweenSize(
    UDim2.new(0,0,0,0),
    Info.SizeTweenEasingDirection,
    Info.SizeTweenEasingStyle,
    Info.SizeTweenTime
    )
    wait(Info.SizeTweenTime)
    MainScreen.Enabled = false
else
    MainScreen.Enabled = false
    MainScrollingFrame.Size = UDim2.new(0,0,0,0)
end
end


end

return WindowFunctions
end
