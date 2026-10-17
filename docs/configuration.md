# Configuration

`plugins/BedrockAssist/config.yml`. Apply changes with `/ba reload`. New keys are added automatically to existing
files when you update the plugin.

## General

| Key | Default | Description |
|---|---|---|
| `language` | `en` | Language used for players whose game language has no text file, and for the server log: `en`, `fr`, or a language you added |

## Links

| Key | Default | Description |
|---|---|---|
| `links.enabled` | `true` | Remember the links received by Bedrock players (last 10, for 10 minutes) and offer `/ba links` |
| `links.domains` | `[]` | Only remember links to these domains and their subdomains, e.g. `[discord.gg, example.com]`. Empty = every link |

Players get a short hint in chat ("Link received: /ba links") at most once every 30 seconds. Links from plugin
messages need PacketEvents; without it, only player chat is read.

## Commands

| Key | Default | Description |
|---|---|---|
| `commands.enabled` | `true` | Offer `/ba commands` |
| `commands.show-all` | `true` | Add an "All commands" button: every command the player may use, alphabetical, with a text field for the arguments |
| `commands.list` | spawn, home, tpa, msg | Commands shown first (see below) |

Each entry of `commands.list` has a `name` (button text), a `command` (without `/`) and optional `args`. Every
`{name}` in the command is filled from the argument of the same name:

```yaml
commands:
  list:
    - name: "Private message"
      command: "msg {player} {message}"
      args:
        player: {type: player, label: "Player"}     # list of online players
        message: {type: text, label: "Message"}     # free text
    - name: "Game mode"
      command: "gamemode {mode}"
      args:
        mode: {type: choice, label: "Mode", options: [survival, creative, adventure]}
    - name: "Pay"
      command: "pay {player} {amount}"
      args:
        player: {type: player, label: "Player"}
        amount: {type: number, label: "Amount"}    # must be a number
```

An entry is hidden when its command doesn't exist on the server, so the default entries only appear if you have a
plugin that provides them. Commands run with the player's own permissions.

## Enchantments

| Key | Default | Description |
|---|---|---|
| `enchant.enabled` | `true` | Offer `/ba enchant` |

## Anvil and smithing table

| Key | Default | Description |
|---|---|---|
| `anvil.mode` | `ask` | `ask`: when a Bedrock player opens an anvil or smithing table, ask "Normal screen" or "Combine (custom recipes)". `always`: open the Combine menu directly (a switch in it still leads to the normal screen, for renaming). `off`: disabled |

The result and its cost are computed by the server, so plugins that change anvil results (custom enchantments) are
taken into account. Anvil wear and level cost are vanilla; creative players pay nothing.

## Villagers

| Key | Default | Description |
|---|---|---|
| `villager.mode` | `mobile` | `mobile`: trade menu for Android and iOS players only (the platforms affected by the Geyser bug). `all`: every Bedrock player. `off`: disabled |

The menu is not shown when the player is sneaking, holds a name tag or a spawn egg, or when the villager is
sleeping: these keep their vanilla behaviour. A villager already trading with someone else is refused.

## Languages

Texts are in `plugins/BedrockAssist/lang/<code>.yml`. `en.yml` and `fr.yml` are created at the first start.

- Each player gets the file matching the language of their game: `pt_br.yml` for Brazilian Portuguese, otherwise
  `pt.yml`, otherwise the `language` of the config
- To change a text, edit it and run `/ba reload`
- To add a language, copy `en.yml` to `de.yml` (for example) and translate it. Keep the `%s` and `%d` placeholders
  in the same order
- A text missing from a file, or with a placeholder error, falls back to the built-in text (English for a language
  you added)

Item names in the menus stay in English: Bedrock doesn't translate the text of forms.
