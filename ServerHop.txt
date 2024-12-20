local HttpService = game:GetService("HttpService")

local function teleportToRandomServer(placeId)
    local gameData = game:HttpGet('https://games.roblox.com/v1/games/' .. tostring(placeId) .. '/servers/Public?sortOrder=Asc&limit=100')
    if gameData then
        local servers = HttpService:JSONDecode(gameData).data
        if servers then
            local server = servers[Random.new():NextInteger(1, #servers)]
            if server and server.id then
                game:GetService("TeleportService"):TeleportToPlaceInstance(placeId, server.id, Player)
                return true
            end
        end
    end
    return false
end

task.wait(1)

teleportToRandomServer(game.PlaceId)
