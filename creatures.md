# Creatures & Customers

Various customer species with different behaviours and preferences. No explicit win condition for the
game, but the implicit story goal is attracting/discovering every customer species — tracked via the
Bestiary.

---

## Customer Types

Species are defined per [npc-dialogue-and-relationships.md](npc-dialogue-and-relationships.md)'s
Character Tiers:

- **Full Characters** — named, recurring individuals with a folder of files (dialogue, personality, arc).
  Can appear in the pub, the shop, or both. See [the-village.md](the-village.md) for the cast.
- **Ambient Customers** — minimal data (a single YAML). Show up in the shop, contribute to the Bestiary,
  no pub presence or arc.

Both share a `type` field on their data (`human` / `vampire` / `fae` / `werewolf` / `witch` /
`sorcerer` / etc.) — this is the species identity the Bestiary and condition-matching (below) key off.

---

## Customer Species

Four broad groups, roughly matching the game's progression arc. Each group has its own
arrival/unlock mechanism. Within a group, individual species still need their own design pass for
exact spawn conditions and preferences — the tables below flag what's real vs. placeholder.

### Non-Magical Humans

Available from the start, no unlock condition.

| Species | Rarity | Interested In |
|---|---|---|
| Villagers | Super Common | Common knowledge books, common potions, herbs/flowers/mushrooms, tarot decks, common artifacts |
| Hunters | Common | All books, all potions, all artifacts, protection and luck spells |

### Magical Humans

Hedge Witches and Druids are locally tied and show up early, same as the non-magical humans above.
Witches & Wizards and Arcanists live elsewhere in the world and need the Forest Portal active to
teleport in (see Forest Portal below) — once it's active, Druids also start arriving in bigger
numbers from further afield, on top of the local ones already showing up.

| Species | Rarity | Arrival | Interested In |
|---|---|---|---|
| Hedge Witch | Common | Early, no portal needed | Common spell scrolls, herbs/flowers/mushrooms, common spell books, common potion books, common potions, tarot decks |
| Druids | Uncommon | Early (local); larger numbers once the portal's active | Artifacts and gemstones, common and advanced potion books, advanced potions |
| Witches & Wizards | Common | Requires the Forest Portal active | All spell scrolls, herbs/flowers/mushrooms, all spell books, all potion books, all potions, tarot decks |
| Arcanists | Uncommon | Requires the Forest Portal active | Artifacts and gemstones, advanced spell books, advanced potions, arcane tarot decks |

### Forest Creatures

Live in pockets that sit halfway between this world and the other — neither fully here nor there.
Drawn in once the shop's magical aura is strong enough, not by the Forest Portal. Exact aura
threshold per species isn't mapped out yet.

- Ents
- Mushroom Folk
- Satyr
- Kobolds
- Ogres
- Bogfolk
- Vampire
- Werewolf
- Cyclops
- Banshee
- Goblins — also a theft threat with its own countermeasures (see [goblins.md](goblins.md)); as a
  customer species they belong in this group like the rest

**Mythological grounding:** see [breton-folklore.md](breton-folklore.md) for the per-species
folklore pass — real Breton/Celtic equivalents where they exist, explicit "not native, portal-brought"
status where they don't.

**Placeholder data:** rarity and preferences for this whole group are still an unfilled block in the
source material (Common / Artifacts and gemstones, advanced spell books, advanced potions — identical
for all of them). Needs a real per-species design pass, not usable as-is.

### High Fae & Demons

Live in the other world and only cross over when summoned — end-game content. The Invoke Minor Demon
spells (see Invocation in [spells.md](spells.md)) are the summoning mechanism. The Traveler, the
entity behind the player's opening bargain (see Concept in [game-overview.md](game-overview.md)), is
also high fae/demon, though not a shop customer. Burning any Devil tarot card summons him as a
character to talk to (see Burning the Devil in [tarot.md](tarot.md)).

- Imps
- Succubus
- Demon
- Nephilim

**Placeholder data:** same unfilled block as Forest Creatures above — needs its own design pass.

---

## Bestiary

Part of the Grimoire (see [game-overview.md](game-overview.md)). Log of every customer type encountered —
also the knowledge source for what conditions attract a given species. Books grant Bestiary knowledge
(what potions or conditions attract a species, not just resale value), directly serving the
"attract every species" story goal.

---

## Weather & Time Sensitivity

Some species are weather/time sensitive — e.g. vampires more likely on cloudy days. This is the system
that already works and doesn't depend on the condition-matching design below.

---

## Forest Portal

A stone circle in the forest that expands the customer roster once activated.

- Discoverable at any time through normal exploration, or learned about first from a villager (pub
  conversation) or a Knowledge entry from a book — sometimes foraging for mushrooms is what leads to it.
- Activating requires knowing the ritual (its own Knowledge entry): place an artifact at the center of
  the circle during a full moon.
- Once activated, sets a portal-open flag. Hooks directly into the existing `presence.lua` "Type Unlock
  Conditions" system documented in
  [npc-dialogue-and-relationships.md](npc-dialogue-and-relationships.md) — including `is_full_moon()`,
  already supported there. No new engine infrastructure needed, just a new flag value.
- Whatever else is needed for a specific character or species to show up beyond the portal being open
  lives in that species' own presence script, not centrally defined.
- **Open detail:** does the artifact get consumed by the ritual, or is it retrievable afterward? Not
  decided yet.

Scope: "Want" — expands the roster and serves the "attract every species" goal, but the game is a
complete loop without it, just with a smaller roster.

---

## Forest Spirits

A second marketplace for shop supply, separate from the Traveler's Soul Shard UI — encountered in the
forest. Some items still cost Soul Shards; others specifically require a barter trade (give an item,
receive an item) instead of currency.

**Not yet designed:** which spirits, what they stock, what they want in trade, how/when they're
encountered. Scope: "Want" — the Traveler's UI already covers all necessary supply on its own.

---

## Per-Species Condition Details — Not Designed Yet

### What We Have

- Broad per-group arrival mechanisms are defined — see Customer Species above (the Forest Portal for
  some Magical Humans, shop aura for Forest Creatures, summoning for High Fae & Demons).
- Books teach the player what a given species needs, via the Bestiary.
- Spells can manufacture some of these conditions directly (speeding growth, customizing the shop,
  changing the local climate, actively creating conditions a species needs) — see
  [spells.md](spells.md).
- The existing weather/time system already works independently of this — see above.

### Open Question

Exactly which conditions gate an individual species — aura strength, weather, moon phase, specific
potions or artifacts on display — isn't mapped out at all. This needs an actual design pass, species
by species, before it can be built.

### Minimum to Get Something Working

The existing weather/time sensitivity system alone; customers can already spawn through it without any
condition-matching layer.

### Perfect World / Cool Ideas (not committed)

- A full condition-matching table per species: temperature, moon phase, potions currently on display,
  artifacts present, spells recently cast, forest-portal state.
- Conditions discoverable progressively through Bestiary entries rather than all at once.
- Some conditions player-manufacturable (via spells), others purely environmental/seasonal.
