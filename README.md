# HTML5 Template SOLAR2D

- Build from Solar2D V3709
  - Fixed:
    * Fixed blurry in-game images.
    * Fixed low fps.
    * Fixed crash when running the game with the browser zoomed in.
  - Some differences:
    * Override default screen size with full browser size.
    * Full-screen display with mobile devices.

## BOX2D V3
### Changes compared to box2d v2:
#### Post collision replace by hit collision
```lua
local function hitCollisionEvent( self, event )
	if e.approachSpeed > 10 then
		-- do something
	else
		-- ..
	end
end

local ball = display.newCircle( display.contentCenterX, display.contentCenterY-40, 15 )
physics.addBody( ball, "dynamic", { bounce=0.0, radius=20 } )

ball.hitCollision = hitCollisionEvent
body:setHitEventsEnabled(true)
ball:addEventListener( "hitCollision", ball )
```
#### PreCollision need to enable
```lua
local platform = display.newRect( 0, 0, 280, 30 )
platform.x, platform.y = display.contentCenterX, display.contentCenterY+80
platform.collType = "passthru"
physics.addBody( platform, "static", { bounce=0.0, friction=0.3 } )
 
local function preCollisionEvent( self, event )
   local collideObject = event.other
   if ( collideObject.collType == "passthru" ) then
      -- event.contact.isEnabled = false -- box2d v2
      return false -- box2d v3
   end
   return true
end
 
local ball = display.newCircle( display.contentCenterX, display.contentCenterY-40, 15 )
physics.addBody( ball, "dynamic", { bounce=0.0, radius=20 } )
 
ball.preCollision = preCollisionEvent
body:setPreSolveEventsEnabled(true)
ball:addEventListener( "preCollision", ball )
```
#### More bodies
```lua
-- Circle with x, y
physics.addBody(object, "dynamic", {circle = {x = 0, y = 0, radius = 32})

-- capsule
physics.addBody(object, "dynamic", {capsule = {x1 = 0, y1 = -16, x2 = 0, y2 = 16, radius = 8}) -- -> 2 circle top and bottom
-- more detail
--https://box2d.org/documentation/group__geometry.html#structb2_capsule 
```

Build from:

https://github.com/labolado/corona/releases

## Usage:

Replace webtemplate file in resources folder of Solar2D.

## Sponsor this project
- Gift me a coffee cup: [Kofi](https://www.ko-fi.com/kandev)
