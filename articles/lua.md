### Lua
Lua is a lightweight multi-paradigm programming language designed primarily for embedded systems and clients. Lua files are stocked and loaded
from .res files with functions: [luaL_loadbuffer](http://pgl.yoyo.org/luai/i/luaL_loadbuffer), [luaL_loadfile](http://pgl.yoyo.org/luai/i/luaL_loadfile), [lua_call](http://pgl.yoyo.org/luai/i/lua_call), [lua_pcall](http://pgl.yoyo.org/luai/i/lua_pcall). 

We can easily find these functions in the StreetGear executable file and load our own lua file. 

All we gotta do is read the lua file and stock it into a buffer and then load it into the current lua state with luaL_loadbuffer.

The lua state pointer is located at two different addresses
```
BaseAddress + 0x00599BBC 
```
```
BaseAddress + 0x00599BD4
```
### Scripting

[StreetGears use its own lua functions, here is a raw dump](https://raw.githubusercontent.com/OpenStreetGears/docs/master/raw/func_dump.md), feel free to contribute to add arguments next to functions.

Let's start the basics, most of player functions use a player index, here is how you get it for local player

```
local selfIdx = GetPlayerIdx() -- Player index
local selfActor = GetPlayerActor(GetPlayerIdx()) -- Self actor id
```

Here is how you get and set position of your player
```
local pos = GetPlayerPos(selfIdx)
SetPos(pos.x, pos.y, pos.z + 200) -- This will teleport us high in the sky
```
Here is some functions I made 
```
function playEffect(actor, fx, animation, time)
    actor:PlayEffect(fx)
    if actor:IsViewPlayer() == true then
    	actor:Play_ForceEffect( "hit" )
    end
	AddSystemText(string.format("L'effet %s a ete lance !", fx))
end
```
```
function playAnimation(actor, animation, time)
	actor:PlayAnimation(animation, 0, time)
	actor:PlayAnimation(animation, 0, time, "hair")
    if actor:IsViewPlayer() == true then
    	actor:Play_ForceEffect( "hit" )
    end
	AddSystemText(string.format("L'animation %s a ete joue !", animation))
end
```
```
function spawnEffect(effect)
	local pos = GetPlayerPos(GetLocalIdx())
	mis_AddEffectWithPosAndView( effect, pos.x, pos.y + 25, pos.z, 0, 1, 0 )
end
```
A list of different effects and animations:
### Player effect
```
item_fx_use_lightning_hitting
```
### Player animation
```
attack_lightning
```
### Spawnable effect
```
intro_item_fx_gp_x50_get
sgfx_quest_fire02_fx
```
