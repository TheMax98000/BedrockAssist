# Commands and permissions

`/ba` is an alias of `/bedrockassist`. The menus are for Bedrock (Floodgate) players; Java players get a short
message instead.

| Command | Description |
|---|---|
| `/ba` | Main menu: links, commands, enchantments (enabled modules only) |
| `/ba links` (`/ba liens`) | Links received in the last 10 minutes, ready to copy |
| `/ba commands` (`/ba commandes`) | Command list, then every command the player may use |
| `/ba enchant` | Enchantments and levels of the item in hand |
| `/ba reload` | Reload `config.yml` and the language files |

The anvil, smithing table and villager menus open by themselves when a Bedrock player uses the block or villager.

| Permission | Default | Description |
|---|---|---|
| `bedrockassist.use` | everyone | Use `/ba` |
| `bedrockassist.admin` | op | Use `/ba reload` |
