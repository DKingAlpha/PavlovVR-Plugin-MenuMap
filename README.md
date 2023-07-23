# Menu Map

A map where players can vote for next playing maps.

## Setup

1. Edit Game.ini, make this map (UGC3189342) the only map in your server's map rotation list.
2. Run a RCON http relay endpoint with [UGC3189342/Resources/rcon.py](UGC3189342/Resources/rcon.py)
3. Create `menu_config.json` as `~/pavlovserver/Pavlov/Saved/Config/ModSave/menu_config.json` in your pavlov server, with the following content:

```json
{
    // RCON http relay endpoint
    "endpoint": "http://<relay_server>:<relay_port>/rcon",
    // RCON server info
    "server": "<rcon_ip_or_domain>",
    "port": 12345,
    "password": "<rcon_password>",
    // time in seconds to end vote
    "vote_round_time": 300,
    // map config
    "maps": [
        ["Map Display Name 1", "UGCXXXXXXX", "TDM", "http://xxx-16:9-image-to-display.png"],
        ["Map Display Name 2", "UGCYYYYYYY", "CUSTOM", "http://yyy-16:9-image-to-display.png"]
    ]
}
```

**REMOVE `//` comments before use.**

Demo MiniMenu.umap Level supports up to 6 maps. Want more? See below.


## Make your own menu map


Menu Map is essentially composed of:

1. An unique BP_MapVoteController to control the vote process
2. An unique BP_Billboard to display countdown
3. Multiple BP_MapView to display map list.
4. A config file described above

### 1. Copy `UGC3189342` folder to your `Plugins/` folder of PavlovVR-ModKit

*See `Plugins/UGC3189342/Content/Levels/MiniMenu.umap`*

### 2. Migrate `Plugins/UGC3189342/Content/Blueprints` into your plugin folder

Make sure these BPs are in your level.

### 3. Drag BP_MapView objects to desired location near a surface

The image of map specified in config will be displayed on the surface as decal, also names and voters will display near it.

### 4. Edit parameters of BP_MapVoteController object

Add all BP_MapView objects to `Map Pool`. The order you add is the order that displays in the level, unused BP_MapView will be hidden & deactivated in game.

Set `Bill Board` to the BP_Billboard object in your level. You can customize this blueprint.

### 5. Run RCON relay, Create config on your pavlov server. Done!
