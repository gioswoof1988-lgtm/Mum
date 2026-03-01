local Players = game:GetService('Players')

pcall(function()
    setthreadidentity(2)
end)

local imageAsset = ''

pcall(function()
    local url = 'https://raw.githubusercontent.com/gioswoof1988-lgtm/Mum/main/IMG_5418.jpeg'
    local filename = 'popup_img.jpg'
    local data = game:HttpGet(url)
    writefile(filename, data)
    imageAsset = getcustomasset(filename)
end)

-- fallback to direct URL if getcustomasset failed
if imageAsset == '' then
    imageAsset = 'https://raw.githubusercontent.com/gioswoof1988-lgtm/Mum/main/IMG_5418.jpeg'
end

local screenGui = Instance.new('ScreenGui')
screenGui.Name = 'SpamGui'
screenGui.ResetOnSpawn = false
screenGui.ZIndexBehavior = Enum.ZIndexBehavior.Sibling
screenGui.IgnoreGuiInset = true
screenGui.Parent = Players.LocalPlayer.PlayerGui

while true do
    for i = 1, 10 do
        task.spawn(function()
            pcall(function()
                local img = Instance.new('ImageLabel')
                img.Size = UDim2.fromOffset(
                    math.random(300, 700),
                    math.random(300, 700)
                )
                img.Position = UDim2.fromScale(
                    math.random(0, 100) / 100,
                    math.random(0, 100) / 100
                )
                img.AnchorPoint = Vector2.new(0.5, 0.5)
                img.BackgroundTransparency = 1
                img.Image = imageAsset
                img.ZIndex = math.random(1, 100)
                img.Parent = screenGui
            end)
        end)
    end
    task.wait(0)
end
