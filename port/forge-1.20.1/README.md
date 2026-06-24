# Forge 1.20.1 port of the Enchanter scroll quests

These are **1.20.1 / Forge** copies of the 5 Enchanter scroll quests that live in this repo at
`src/main/resources/data/minecolonies/colony/quests/general/` (NeoForge 1.21.1 format).

## Why a separate copy?

The MineColonies quest JSON schema diverged between 1.20.1 (Forge) and 1.21.1 (NeoForge). A single
file cannot parse on both — the `item` field is a bare string in 1.20.1 but a CODEC object in 1.21.1,
and the 1.20.1 parser additionally requires a separate `qty` int (its absence is the
`DeliveryObjectiveTemplateTemplate` NPE on launch). Differences applied here:

| Element | 1.21.1 (other folder) | 1.20.1 (these files) |
|---|---|---|
| quest folder | `data/minecolonies/colony/quests/` | `data/minecolonies/quests/` |
| delivery / item-reward `item` | object `{id,count}` | string id + separate `"qty"` int |
| potion data | `components` | NBT string `"{Potion:\"minecraft:luck\"}"` |

Triggers, dialogue, `return`/`cancel`/`advanceobjective` results, and happiness rewards are identical
and unchanged.

## How to use

Drop the `data/` tree here into the 1.20.1 build's resources (or a datapack) so the files land at:

```
data/minecolonies/quests/general/{bumpinthenight,apromisetokeep,adayinthefield,wheresthebuilder,ancientmagic}.json
```

Note the path is `quests/`, **not** `colony/quests/` — that folder name also changed between versions.
