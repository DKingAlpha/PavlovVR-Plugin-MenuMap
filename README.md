# Menu Map

A map where players can vote for next playing maps.

## Setup

1. Edit Game.ini, make this map (UGC3189342) the only map in your server's map rotation list.
2. Create `menu_config.json` as `~/pavlovserver/Pavlov/Saved/Config/ModSave/menu_config.json` in your pavlov server, with the following content:

```json
{
    // RCON http relay endpoint
    "endpoint": "http://<relay_server>:<relay_port>/rcon",
    // RCON server info
    "server": "<rcon_ip_or_domain>",
    "port": 12345,
    "password": "<rcon_password>",
    // vote time config
    "vote_round_time": 300, // time in seconds to end vote
    // map config
    "maps": [
        ["Map Display Name 1", "UGCXXXXXXX", "TDM", "http://xxx-16:9-image-to-display.png"],
        ["Map Display Name 2", "UGCYYYYYYY", "CUSTOM", "http://yyy-16:9-image-to-display.png"],
        // ...
    ]
}
```

To run a RCON http relay endpoint ,run [Resources/rcon.py](Resources/rcon.py)


## Make your own menu map

Copy `UGC3189342` folder to your `Plugins/` folder of PavlovVR-ModKit

*See `Plugins/UGC3189342/Content/Levels/MiniMenu.umap`*

Menu Map is essentially composed of:

1. An unique BP_MapVoteController to control the vote process
2. An unique BP_Billboard to display countdown
3. Multiple BP_MapView to display map list.
4. A config file described above

Make sure these BPs are in your level.

### 1. Migrate `Plugins/UGC3189342/Content/Blueprints` into your plugin folder


### 2. Drag BP_MapView objects to desired location near a surface

The image of map specified in config will be displayed on the surface as decal, also names and voters will display near it.

### 3. Edit parameters of BP_MapVoteController object

Add all BP_MapView objects to `Map Pool`. The order you add is the order that displays in the level, unused BP_MapView will be hidden & deactivated in game.

Set `Bill Board` to the BP_Billboard object in your level. You can customize this blueprint.

### 4. Run RCON relay, Create config on your pavlov server. Done!
