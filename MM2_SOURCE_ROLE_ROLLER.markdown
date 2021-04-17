**this code was fully written by me, the formula's written in the script are of my creation. (nothing is stolen).**
##### pretty freaking long script, sorry.

```LUA
local RoleLabel = script.Parent.DisplayRoleChoice.RoleLabel
local Roles = game.ReplicatedStorage.Roles
local StopRoll = game.ReplicatedStorage:WaitForChild("StopRoll")

local MurdTool = game.ReplicatedStorage.RemoteEvents:WaitForChild("MurdTool")
local plrs = game.Players:GetChildren()

print(#plrs)
x = #plrs*25

local chances = math.random(1, #plrs + 50 / #plrs * math.rad(x)) -->> the amount i allow
print(chances)

local rTable = {}
local chancesShuffled = {}

local bool_cancelReqForRole = game.ReplicatedStorage.GameValues:WaitForChild("cancelReq")

Available_Roles = {
	Innocent = 5; -->> innocent
	Sheriff = 1; -->> sheriff
	Murderer = 1; -->> murderer
	ROLE = {
		self.Available_Roles.Innocent.Name == "yo momma"
	}
}

local function timing()
	for i = 1, #workspace.waiter:GetChildren(), 1 do
		wait(i)
		if i == 6 then
			StopRoll.Value = true
		end
	end
end

timing(print "Counted" )

local stopfunc = Instance.new("BoolValue", game.ReplicatedStorage.GameValues)

function ifMurderer()
	if not bool_cancelReqForRole.Value then
		if RoleLabel.Text == Available_Roles.Murderer then
			RoleLabel.TextColor3 = Color3.fromRGB(255, 0, 0)
			MurdTool:FireServer()
		end
	else
		return;
	end
end

function ifSheriff()
	if RoleLabel.Text == Available_Roles.Sheriff then
		RoleLabel.TextColor3 = Color3.fromRGB(0, 0, 255)
	end
end

function ifInnocent()
	if RoleLabel.Text == Available_Roles.Innocent then
		RoleLabel.TextColor3 = Color3.fromRGB(0, 255, 0)
	end
end

-->> so kurzgesagt this takes a roll of 1 to players in the game and then / 2 then puts val into table and randomizes from 1 to the shuffled chances.
function Roll()
	if RoleLabel ~= nil then
		-->> if that exists then
		for i, v in pairs (Roles:GetChildren()) do
			table.insert(rTable, v.Name)
			table.insert(chancesShuffled, chances)
			
			for key, _ in pairs (chancesShuffled) do
				local sChances = math.random(chancesShuffled[1], chancesShuffled[key])
				
				print(rTable[i])
				
				repeat wait(0.5)
					RoleLabel.Text = rTable[i]
				until RoleLabel.Text == rTable[i] and StopRoll.Value
				-->> 1 = 100 / 2 = 50
				if #plrs == 2 then
					if sChances == Available_Roles.Innocent and RoleLabel.Text == "Innocent" then
					Roles.Innocent.Value = true
					if Roles.Innocent.Value then
						ifInnocent()
					else
						return
						end
					else
						if sChances == Available_Roles.Sheriff and RoleLabel.Text == "Sheriff" then
							Roles.Sheriff.Value = true
							if Roles.Sheriff.Value then
								ifSheriff()
							else
								return
							end
						else
							return
						end
					end
					-->> for now this is always 1 (not anymore)
				elseif sChances == Available_Roles.Murderer and RoleLabel.Text == "Murderer" then
					Roles.Murderer.Value = true
					if Roles.Murderer.Value then
						ifMurderer()
					else
						return
					end
				elseif sChances ~= Available_Roles.Innocent + Available_Roles.Sheriff then
					print(Available_Roles.Innocent + Available_Roles.Sheriff) -- what the heck is this?
					ifInnocent()
				else
					return
				end
				StopRoll.Value = true
			end
		end
	end
end

Roll(print "rolled")

-- to cancel all req to prevent duplicated roles
if stopfunc.Value then
	wait(1)
	RoleLabel.TextColor3 = Color3.fromRGB(255, 255, 0)
	for i = 10, 1, -1 do
		wait(1)
		RoleLabel.Text = i
	end
end
```
