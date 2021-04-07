#Made by: @JayceMichael

[CLIENT]


```LUA
local tbutton = script.Parent
rbool = true

tbutton.MouseButton1Down:Connect(
	function ()
		tbutton.BackgroundColor3 = Color3.fromRGB(30, 82, 255)
		game.ReplicatedStorage:WaitForChild("RemoteFunction"):InvokeServer(rbool)
		if "clicked" then
			local range = math.random(100, 255)
			tbutton.BackgroundColor3 = Color3.fromRGB(range, range, range)
			tbutton.Text = game.Players.LocalPlayer.Name.." clicked me!"
		elseif "no" then
			return nil;
 		end
	end
)
```
[SERVER]
```LUA
local rfunc = game.ReplicatedStorage:WaitForChild("RemoteFunction")

plr_parts = {}
self = {
	BlastRadius = 5,
	BlastPressure = 5
}

function callback(plr, rbool)
	if rbool then
		local explosion = Instance.new("Explosion", workspace)
		explosion.BlastRadius = self.BlastRadius
		explosion.BlastPressure = self.BlastPressure
		
		for i, v in pairs (plr.Character:GetChildren()) do
			if v:IsA "Part" then
				table.insert(plr_parts, v)
				for u, _ in pairs (plr_parts) do
					print(plr_parts[u].Name)
					plr_parts[u].Transparency = 0.2
				end
			end
		end
		return "clicked"
	else
		return "no"
	end
end

rfunc.OnServerInvoke = callback
```
