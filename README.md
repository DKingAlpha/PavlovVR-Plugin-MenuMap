# Menu Map

A map where players can vote for next playing maps.

![Demo](UGC3189342/Resources/menu_map_20230729062427.png)

## Requirements

1. A dedicated server with file system access (You can manually create config file for server)
2. Python 3.11, with package `async-pavlov`. (`pip3 install async-pavlov`)

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

## Make your own menu map

**See `Plugins/UGC3189342/Content/Levels/MiniMenu.umap` for example**

Menu Map is essentially composed of:

1. An unique Actor inheriting BP_VoteControllerBase to control the vote process on server side.
2. Anything to display countdown
3. Multiple Actors inheriting BP_VoteProxyBase to display maps as an option to client side.
4. A json config file described above

### 1. Copy `UGC3189342` folder to your `Plugins/` folder of PavlovVR-ModKit

### 2. Migrate `Plugins/UGC3189342/Content/Blueprints` into your plugin folder

Make sure these BPs are in your level.

### 3. Drag BP_VoteControllerMap into your level

Edit properties if needed.

### 4. Run RCON relay, Create config on your pavlov server. Done! Start PavlovServer now.

