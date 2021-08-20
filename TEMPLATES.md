# These are Templates for all the functions in qb-target

## AddCircleZone

### Function format

```lua
-- This is the function from how you would use it inside qb-target/client/main.lua
Functions:AddCircleZone(name: string, center: vector3, radius: float, options: table, targetoptions: table)

options = {
  name: string (UNIQUE),
  debugPoly: boolean,
}

targetoptions = {
  {
    type: string,
    event: string,
    icon: string,
    label: string,
    targeticon: string,
    item: string,
    action: function,
    canInteract: function,
    job: string
  }
},
distance: float
```

### Config option, this will go into the Config.CircleZones table

```lua
  ["index"] = { -- This can be a string or a number
    name = "name", -- This is the name of the zone recognized by PolyZone, this has to be unique so it doesn't mess up with other zones
    coords = vector3(x, y, z), -- These are the coords for the zone, this has to be a vector3 and the coords have to be a float value, fill in x, y and z with the coords
    radius = 1.5, -- The radius of the circlezone calculated from the center of the zone, this has to be a float value
    debugPoly = false, -- This is for enabling/disabling the drawing of the box, it accepts only a boolean value (true or false), when true it will draw the polyzone in green
    options = { -- This is your options table, in this table all the options will be specified for the target to accept
      { -- This is the first table with options, you can make as many options inside the options table as you want
        type = "client", -- This specifies the type of event the target has to trigger on click, this can be "client", "server", "command" or "qbcommand", this is OPTIONAL and will only work if the event is also specified
        event = "Test:Event", -- This is the event it will trigger on click, this can be a client event, server event, command or qbcore registered command, NOTICE: Normal command can't have arguments passed through, QBCore registered ones can have arguments passed through
        icon = 'fas fa-example', -- This is the icon that will display next to this trigger option, all the icons can be found on fontawesome.com
        label = 'Test' -- This is the label of this option which you would be able to click on to trigger everything, this has to be a string
        targeticon = 'fas fa-example' -- This is the icon of the target itself, the icon changes to this when it turns blue on this specific option, this is OPTIONAL
        item = 'handcuffs', -- This is the item it has to check for, this option will only show up if the player has this item, this is OPTIONAL
        action = function(entity) -- This is the action it has to perform, this REPLACES the event and this is OPTIONAL
          if IsPedAPlayer(entity) then return false end -- This will return false if the entity interacted with is a player and otherwise returns true
          TriggerEvent('testing:event', 'test')
          return true
        end,
        canInteract = function(entity) -- This will check if you can interact with it, this won't show up if it returns false, this is OPTIONAL
          if IsPedAPlayer(entity) then return false end -- This will return false if the entity interacted with is a player and otherwise returns true
          return true
        end,
        job = 'police', -- This is the job, this option won't show up if the player doesn't have this job, this can also be done with multiple jobs and grades, if you want multiple jobs you always need a grade with it: job = {["police"] = 0, ["ambulance"] = 2}
      }
    },
    distance = 2.5, -- This is the distance for you to be at for the target to turn blue, this is in GTA units and has to be a float value
  },
```

### Export option, this will go into any client side resource file aside from qb-target's one

```lua
exports['qb-target']:AddCircleZone("name", vector3(x, y, z), 1.5, { -- The name has to be unique, the coords a vector3 as shown and the 1.5 is the radius which has to be a float value
  name = "name", -- This is the name of the zone recognized by PolyZone, this has to be unique so it doesn't mess up with other zones
  debugPoly = false, -- This is for enabling/disabling the drawing of the box, it accepts only a boolean value (true or false), when true it will draw the polyzone in green
}, {
  options = { -- This is your options table, in this table all the options will be specified for the target to accept
    { -- This is the first table with options, you can make as many options inside the options table as you want
      type = "client", -- This specifies the type of event the target has to trigger on click, this can be "client", "server", "command" or "qbcommand", this is OPTIONAL and will only work if the event is also specified
      event = "Test:Event", -- This is the event it will trigger on click, this can be a client event, server event, command or qbcore registered command, NOTICE: Normal command can't have arguments passed through, QBCore registered ones can have arguments passed through
      icon = 'fas fa-example', -- This is the icon that will display next to this trigger option, all the icons can be found on fontawesome.com
      label = 'Test' -- This is the label of this option which you would be able to click on to trigger everything, this has to be a string
      targeticon = 'fas fa-example' -- This is the icon of the target itself, the icon changes to this when it turns blue on this specific option, this is OPTIONAL
      item = 'handcuffs', -- This is the item it has to check for, this option will only show up if the player has this item, this is OPTIONAL
      action = function(entity) -- This is the action it has to perform, this REPLACES the event and this is OPTIONAL
        if IsPedAPlayer(entity) then return false end -- This will return false if the entity interacted with is a player and otherwise returns true
        TriggerEvent('testing:event', 'test')
        return true
      end,
      canInteract = function(entity) -- This will check if you can interact with it, this won't show up if it returns false, this is OPTIONAL
        if IsPedAPlayer(entity) then return false end -- This will return false if the entity interacted with is a player and otherwise returns true
        return true
      end,
      job = 'police', -- This is the job, this option won't show up if the player doesn't have this job, this can also be done with multiple jobs and grades, if you want multiple jobs you always need a grade with it: job = {["police"] = 0, ["ambulance"] = 2}
    }
  },
  distance = 2.5, -- This is the distance for you to be at for the target to turn blue, this is in GTA units and has to be a float value
})
```

## AddBoxZone

### Function format

```lua
-- This is the function from how you would use it inside qb-target/client/main.lua
Functions:AddBoxZone(name: string, center: vector3, length: float, width: float, options: table, targetoptions: table)

options = {
  name: string (UNIQUE),
  heading: float,
  debugPoly: boolean,
  minZ: float,
  maxZ: float,
}

targetoptions = {
  {
    type: string,
    event: string,
    icon: string,
    label: string,
    targeticon: string,
    item: string,
    action: function,
    canInteract: function,
    job: string
  }
},
distance: float
```

### Config option, this will go into the Config.BoxZones table

```lua
  ["index"] = { -- This can be a string or a number
    name = "name", -- This is the name of the zone recognized by PolyZone, this has to be unique so it doesn't mess up with other zones
    coords = vector3(x, y, z), -- These are the coords for the zone, this has to be a vector3 and the coords have to be a float value, fill in x, y and z with the coords
    length = 1.5, -- The length of the boxzone calculated from the center of the zone, this has to be a float value
    width = 1.6, -- The width of the boxzone calculated from the center of the zone, this has to be a float value
    heading = 12.0, -- The heading of the boxzone, this has to be a float value
    debugPoly = false, -- This is for enabling/disabling the drawing of the box, it accepts only a boolean value (true or false), when true it will draw the polyzone in green
    minZ = 36.7, -- This is the bottom of the boxzone, this can be different from the Z value in the coords, this has to be a float value
    maxZ = 38.9, -- This is the top of the boxzone, this can be different from the Z value in the coords, this has to be a float value
    options = { -- This is your options table, in this table all the options will be specified for the target to accept
      { -- This is the first table with options, you can make as many options inside the options table as you want
        type = "client", -- This specifies the type of event the target has to trigger on click, this can be "client", "server", "command" or "qbcommand", this is OPTIONAL and will only work if the event is also specified
        event = "Test:Event", -- This is the event it will trigger on click, this can be a client event, server event, command or qbcore registered command, NOTICE: Normal command can't have arguments passed through, QBCore registered ones can have arguments passed through
        icon = 'fas fa-example', -- This is the icon that will display next to this trigger option, all the icons can be found on fontawesome.com
        label = 'Test' -- This is the label of this option which you would be able to click on to trigger everything, this has to be a string
        targeticon = 'fas fa-example' -- This is the icon of the target itself, the icon changes to this when it turns blue on this specific option, this is OPTIONAL
        item = 'handcuffs', -- This is the item it has to check for, this option will only show up if the player has this item, this is OPTIONAL
        action = function(entity) -- This is the action it has to perform, this REPLACES the event and this is OPTIONAL
          if IsPedAPlayer(entity) then return false end -- This will return false if the entity interacted with is a player and otherwise returns true
          TriggerEvent('testing:event', 'test')
          return true
        end,
        canInteract = function(entity) -- This will check if you can interact with it, this won't show up if it returns false, this is OPTIONAL
          if IsPedAPlayer(entity) then return false end -- This will return false if the entity interacted with is a player and otherwise returns true
          return true
        end,
        job = 'police', -- This is the job, this option won't show up if the player doesn't have this job, this can also be done with multiple jobs and grades, if you want multiple jobs you always need a grade with it: job = {["police"] = 0, ["ambulance"] = 2}
      }
    },
    distance = 2.5, -- This is the distance for you to be at for the target to turn blue, this is in GTA units and has to be a float value
  },
```

### Export option, this will go into any client side resource file aside from qb-target's one

```lua
exports['qb-target']:AddBoxZone("name", vector3(x, y, z), 1.5, 1.6, { -- The name has to be unique, the coords a vector3 as shown, the 1.5 is the length of the boxzone and the 1.6 is the width of the boxzone, the length and width have to be float values
  name = "name", -- This is the name of the zone recognized by PolyZone, this has to be unique so it doesn't mess up with other zones
  heading = 12.0, -- The heading of the boxzone, this has to be a float value
  debugPoly = false, -- This is for enabling/disabling the drawing of the box, it accepts only a boolean value (true or false), when true it will draw the polyzone in green
  minZ = 36.7, -- This is the bottom of the boxzone, this can be different from the Z value in the coords, this has to be a float value
  maxZ = 38.9, -- This is the top of the boxzone, this can be different from the Z value in the coords, this has to be a float value
}, {
  options = { -- This is your options table, in this table all the options will be specified for the target to accept
    { -- This is the first table with options, you can make as many options inside the options table as you want
      type = "client", -- This specifies the type of event the target has to trigger on click, this can be "client", "server", "command" or "qbcommand", this is OPTIONAL and will only work if the event is also specified
      event = "Test:Event", -- This is the event it will trigger on click, this can be a client event, server event, command or qbcore registered command, NOTICE: Normal command can't have arguments passed through, QBCore registered ones can have arguments passed through
      icon = 'fas fa-example', -- This is the icon that will display next to this trigger option, all the icons can be found on fontawesome.com
      label = 'Test' -- This is the label of this option which you would be able to click on to trigger everything, this has to be a string
      targeticon = 'fas fa-example' -- This is the icon of the target itself, the icon changes to this when it turns blue on this specific option, this is OPTIONAL
      item = 'handcuffs', -- This is the item it has to check for, this option will only show up if the player has this item, this is OPTIONAL
      action = function(entity) -- This is the action it has to perform, this REPLACES the event and this is OPTIONAL
        if IsPedAPlayer(entity) then return false end -- This will return false if the entity interacted with is a player and otherwise returns true
        TriggerEvent('testing:event', 'test')
        return true
      end,
      canInteract = function(entity) -- This will check if you can interact with it, this won't show up if it returns false, this is OPTIONAL
        if IsPedAPlayer(entity) then return false end -- This will return false if the entity interacted with is a player and otherwise returns true
        return true
      end,
      job = 'police', -- This is the job, this option won't show up if the player doesn't have this job, this can also be done with multiple jobs and grades, if you want multiple jobs you always need a grade with it: job = {["police"] = 0, ["ambulance"] = 2}
    }
  },
  distance = 2.5, -- This is the distance for you to be at for the target to turn blue, this is in GTA units and has to be a float value
})
```