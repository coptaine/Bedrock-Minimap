# Coptaine's Minimap

This addon adds Minimap to pre-made worlds in your game. It's well polished and easy to implement.






FEATURES:

- Zoom function

![map_zoom](https://github.com/coptaine/Bedrock-Minimap/assets/34676595/6361dc86-2c40-4f9f-bc1a-443da53ca95a)

- Player rotation:

![map_player_rotation](https://github.com/coptaine/Bedrock-Minimap/assets/34676595/72eb7a02-a4a6-48a3-9531-fdfee6d02ed8)

- Non-Player icons are bound to the edges:

![map_bound](https://github.com/coptaine/Bedrock-Minimap/assets/34676595/6fe68520-df24-45bf-a71e-96579b61d440)

- Edge detection, player icon moves instead of the map when on the edge of map:

  Toggleable thru "variable.config_bound_to_edges = true/false;"

![map_edge3](https://github.com/coptaine/Bedrock-Minimap/assets/34676595/5d4f1ba6-5174-4727-af60-1b1cc6e94050)



# **HOWTO:**


Use Unmined software to get the texture of your world map. https://unmined.net/

Get the coordinates of the block where your texture will start by hovering your mouse.

![map_coor](https://github.com/coptaine/Bedrock-Minimap/assets/34676595/30ec26b7-8dd4-4964-8814-fdbe8df3634a)

Click Export.

![map_export](https://github.com/coptaine/Bedrock-Minimap/assets/34676595/94146c6d-3a81-402a-92f6-b953b9c25a81)

Take note of these values. X and Z ending blocks are based on your map size. The image is for reference only.

![block selection_edit](https://github.com/coptaine/Bedrock-Minimap/assets/34676595/d054a413-d437-48dd-b62e-58ac2da13a71)

Textures are inside textures/minimap. Change the textures and add more if needed.
![image](https://github.com/coptaine/Bedrock-Minimap/assets/34676595/42d90dca-f831-4e1d-8e75-62a05443e661)

The main config is in the player.entity.json. There are 10 npcs that already made, modify its coordinates and add more if needed.
## Adding npcs:
- Add the coordinates under the initialize:

```
"variable.npc1_x = 123.0;", // Your NPC X coordinate

"variable.npc1_z = 456.0;", // Your NPC Z coordinate

```
- Add the texture:
```
"minimap_npc1": "textures/minimap/npc1"
```

- Add the geometry:
```
"minimap_npc1": "geometry.minimap.npc1"
```

- Add the render controller:
```
{ "controller.render.minimap.npc1": "query.life_time >= 5.0 && !query.is_swimming && query.is_in_ui && !query.is_spectator" }
```

- Add render controller:
```
"controller.render.minimap.npc1": {
"geometry": "Geometry.minimap_npc1",
"materials": [{ "*": "Material.default" }],
"textures": [ "Texture.minimap_npc1" ],
"is_hurt_color": {},
"on_fire_color": {}
}
```

- Add model:
```
{ "description": { "identifier": "geometry.minimap.npc1", "texture_width": 2, "texture_height": 2, "visible_bounds_width": 2, "visible_bounds_height": 13, "visible_bounds_offset": [0, 5.5, 0]}, "bones": [{ "name": "minimap", "pivot": [0, 177, 0]}, { "name": "npc_1", "parent": "minimap", "pivot": [0, 176, 0], "cubes": [{ "origin": [-1, 175, -0.1], "size": [2, 2, 0], "uv": [0, 0]}]}]}
```

## Changing map background texture:
```
"minimap_bg": "textures/map/map_background"
```

## Changing map activation method: 
```
"variable.minimap = query.is_item_name_any('slot.weapon.mainhand', 'coptaine:minimap') ||  query.is_item_name_any('slot.weapon.offhand', 'coptaine:minimap');"
```

Tip: Just change the value to true to make it always show

## Resizing the map:
  (Animation file) Add "scale" value to the "minimap" bone
  
```
"minimap": {
					"relative_to": {
						"rotation": "entity"
					},
					"rotation": [ 0, "q.is_riding ? q.target_y_rotation : 0", 0 ],
					"scale": 1
				},
```

## Moving the map:
  (UI File) Play with values of "offset"
  
```
{
                "minimap": {
                  "renderer": "live_player_renderer",
                  "size": [ 100, 100 ],
                  "offset": [ -70, 950 ],
                  "type": "custom"
                }
              }
```


# **NOT WORKING:**
- While swimming
- While gliding

I have tried using different renderer and it worked but query.position is not functional there.

# **CREDITS**
For the map used for the sake of showing the minimap's functionalies:

https://mcpedl.com/skyline-city/

https://discord.com/channels/523663022053392405/1213488446807478302




