# File_Explorer Nums of folder children indicator
```LUA
local feFrame = script.Parent

local FindNumsOfFolderChildren = feFrame:WaitForChild("FindNumsOfFolderChildren")
FindNumsOfFolderChildren.TextScaled = true

local NumsOfItemsSelected = feFrame:WaitForChild("NumsOfItemsSelected")
NumsOfItemsSelected.TextScaled = true

located = {}

--// make this automated with collectionservice l8r and dual selection by getting the values of 1 & 2 and +(adding) them together with formula i+i
feFrame:WaitForChild("TestFolder").MouseButton1Down:Connect(
	function ()
		table.insert(located, feFrame:WaitForChild("TestFolder"))
		for i, v in pairs (located) do
			for _, children in pairs (located[i]:GetChildren()) do
				lcle = children:GetChildren()
				for nums = 1, #lcle, 1 do
					g_nums = nums;
					FindNumsOfFolderChildren.Text = "["..nums.."]".."items indexed." --// in display it should be shown like "[1] items indexed."
					print(i+nums)
				end
			end
		end
		if FindNumsOfFolderChildren.Text ~= "" then
			table.remove(located, g_nums)
			print(g_nums)
			return;
		end
	end
)
```

# example
![after_click](https://i.gyazo.com/af81f0ba6969caa8ab84f5ec82b4b29b.png)
![item tree](https://i.gyazo.com/8ad8d798c265e646e404c5f008551b89.png)
