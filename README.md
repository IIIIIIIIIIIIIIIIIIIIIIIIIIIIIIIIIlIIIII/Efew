if game:GetService("RunService"):IsClient() then error("Script must be server-side in order to work; use h/ and not hl/") end
local Player,game,owner = owner,game
local RealPlayer = Player
do
    print("FE Compatibility code by Mokiros")
    local rp = RealPlayer
    script.Parent = rp.Character
   
    --RemoteEvent for communicating
    local Event = Instance.new("RemoteEvent")
    Event.Name = "UserInput_Event"
 
    --Fake event to make stuff like Mouse.KeyDown work
    local function fakeEvent()
        local t = {_fakeEvent=true,Functions={},Connect=function(self,f)table.insert(self.Functions,f) end}
        t.connect = t.Connect
        return t
    end
 
    --Creating fake input objects with fake variables
    local m = {Target=nil,Hit=CFrame.new(),KeyUp=fakeEvent(),KeyDown=fakeEvent(),Button1Up=fakeEvent(),Button1Down=fakeEvent()}
    local UIS = {InputBegan=fakeEvent(),InputEnded=fakeEvent()}
    local CAS = {Actions={},BindAction=function(self,name,fun,touch,...)
        CAS.Actions[name] = fun and {Name=name,Function=fun,Keys={...}} or nil
    end}
    --Merged 2 functions into one by checking amount of arguments
    CAS.UnbindAction = CAS.BindAction
 
    --This function will trigger the events that have been :Connect()'ed
    local function te(self,ev,...)
        local t = m[ev]
        if t and t._fakeEvent then
            for _,f in pairs(t.Functions) do
                f(...)
            end
        end
    end
    m.TrigEvent = te
    UIS.TrigEvent = te
 
    Event.OnServerEvent:Connect(function(plr,io)
        if plr~=rp then return end
        m.Target = io.Target
        m.Hit = io.Hit
        if not io.isMouse then
            local b = io.UserInputState == Enum.UserInputState.Begin
            if io.UserInputType == Enum.UserInputType.MouseButton1 then
                return m:TrigEvent(b and "Button1Down" or "Button1Up")
            end
            for _,t in pairs(CAS.Actions) do
                for _,k in pairs(t.Keys) do
                    if k==io.KeyCode then
                        t.Function(t.Name,io.UserInputState,io)
                    end
                end
            end
            m:TrigEvent(b and "KeyDown" or "KeyUp",io.KeyCode.Name:lower())
            UIS:TrigEvent(b and "InputBegan" or "InputEnded",io,false)
        end
    end)
    Event.Parent = NLS([==[
    local Player = game:GetService("Players").LocalPlayer
    local Event = script:WaitForChild("UserInput_Event")
 
    local Mouse = Player:GetMouse()
    local UIS = game:GetService("UserInputService")
    local input = function(io,a)
        if a then return end
        --Since InputObject is a client-side instance, we create and pass table instead
        Event:FireServer({KeyCode=io.KeyCode,UserInputType=io.UserInputType,UserInputState=io.UserInputState,Hit=Mouse.Hit,Target=Mouse.Target})
    end
    UIS.InputBegan:Connect(input)
    UIS.InputEnded:Connect(input)
 
    local h,t
    --Give the server mouse data 30 times every second, but only if the values changed
    --If player is not moving their mouse, client won't fire events
    while wait(1/30) do
        if h~=Mouse.Hit or t~=Mouse.Target then
            h,t=Mouse.Hit,Mouse.Target
            Event:FireServer({isMouse=true,Target=t,Hit=h})
        end
    end]==],Player.Character)
 
    ----Sandboxed game object that allows the usage of client-side methods and services
    --Real game object
    local _rg = game
 
    --Metatable for fake service
    local fsmt = {
        __index = function(self,k)
            local s = rawget(self,"_RealService")
            if s then return s[k] end
        end,
        __newindex = function(self,k,v)
            local s = rawget(self,"_RealService")
            if s then s[k]=v end
        end,
        __call = function(self,...)
            local s = rawget(self,"_RealService")
            if s then return s(...) end
        end
    }
    local function FakeService(t,RealService)
        t._RealService = typeof(RealService)=="string" and _rg:GetService(RealService) or RealService
        return setmetatable(t,fsmt)
    end
 
    --Fake game object
    local g = {
        GetService = function(self,s)
            return self[s]
        end,
        Players = FakeService({
            LocalPlayer = FakeService({GetMouse=function(self)return m end},Player)
        },"Players"),
        UserInputService = FakeService(UIS,"UserInputService"),
        ContextActionService = FakeService(CAS,"ContextActionService"),
    }
    rawset(g.Players,"localPlayer",g.Players.LocalPlayer)
    g.service = g.GetService
   
    g.RunService = FakeService({
        RenderStepped = _rg:GetService("RunService").Heartbeat,
        BindToRenderStep = function(self,name,_,fun)
            self._btrs[name] = self.Heartbeat:Connect(fun)
        end,
        UnbindFromRenderStep = function(self,name)
            self._btrs[name]:Disconnect()
        end,
    },"RunService")
 
    setmetatable(g,{
        __index=function(self,s)
            return _rg:GetService(s) or typeof(_rg[s])=="function"
            and function(_,...)return _rg[s](_rg,...)end or _rg[s]
        end,
        __newindex = fsmt.__newindex,
        __call = fsmt.__call
    })
    --Changing owner to fake player object to support owner:GetMouse()
    game,owner = g,g.Players.LocalPlayer
end

local RunService = game:GetService("RunService")
local Player = owner
  local Character = Player.Character
    local Root = Character:WaitForChild("Torso")
    local Model = Instance.new("Model", Character)
  local Mouse = Player:GetMouse()
local Parts = {}
local Parts2 = {}
local Parts3 = {}
local Parts4 = {}
local RadX, RadY = 0, 0

local function Lerp(Part, CFrame, Time)
	local NewCFrame = Part.CFrame:Lerp(CFrame, Time)
	Part.CFrame = NewCFrame
	return NewCFrame
end

local function Load(Table, XOffset, YOffset)
	local Last
	for _, Part in pairs(Table) do
		if Last then
			Lerp(Part, Last.CFrame * CFrame.Angles(RadX, RadY, 0) * CFrame.new(0, 0, 2), 0.5)
		else
			Lerp(Part, Root.CFrame * CFrame.Angles(RadX + math.rad(XOffset), RadY + math.rad(YOffset), 0) * CFrame.new(0, -0.5, 3), 0.5)
		end
		Last = Part
	end
end

local function CreateParts(Table, Amount)
	for i = 1, Amount do
		local Part = Instance.new("Part", Model)
		Part.Size = Vector3.new(1, 1, 5)
		Part.Anchored = true
		Part.CanCollide = false
		table.insert(Table, Part)
	end
end

CreateParts(Parts, 12)
CreateParts(Parts2, 24)
CreateParts(Parts3, 6)
CreateParts(Parts4, 6)

local SineX = 0
local SineY = 0
local function Step()
	SineX = SineX + 0.1
	SineY = SineY + 0.1 / 2
	local SinX = math.sin(SineX) * 2
	local SinY = math.sin(SineY) * 2
	
	Load(Parts, 5 + SinX, 0 + SinY)
	Load(Parts2, -5 + SinX, 0 + SinY)
	Load(Parts3, 0 + SinX, 15 + SinY)
	Load(Parts4, 0 + SinX, -15 + SinY)
end
RunService.RenderStepped:Connect(Step)

Mouse.Move:Connect(function()
	local X = Mouse.X - Mouse.ViewSizeX/2
	local Y = Mouse.Y - Mouse.ViewSizeY/2
	RadY = (X / Mouse.ViewSizeX)*2
	RadX = (Y / Mouse.ViewSizeY)*2
end)

Model.Name = "gay"
