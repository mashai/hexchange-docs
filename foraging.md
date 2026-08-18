# Foraging & Ingredients

Gathering raw ingredients from the environment, in the shop, or around it. Feeds two other systems
directly: sold on their own, or used in Potions. First system in the build order (see
[scope.md](scope.md)) — cheap relative to Tarot and Potions, and it's what makes both of those
actually mean what they're supposed to mean.

---

## Ingredients

- Foraged in the environment (e.g. the forest) — flowers are the flagship example, but not the only
  kind. Foraging spots also exist near or inside the shop itself, not just out in the world (see
  Potted Plants below).
- Sold directly, or used as potion ingredients (see [potions.md](potions.md)).
- Some are more potent at night — learned through the Grimoire, not told to the player upfront.
- Each foraging spot respawns on its own timer after being picked, tunable per item (mushrooms and
  flowers won't necessarily share a respawn rate). This is the same clock the Grow spell completes
  instantly (see [spells.md](spells.md)) — not a separate growth-stage system. Foraging itself is
  simple, so this should be fast to build.

---

## Weather & Time Sensitivity

Once the weather system exists (see Nature spells in [spells.md](spells.md)), plants respond to it
beyond the night-potency note above: rain speeds up growth for certain plants, and in some cases
weather conditions gate whether a plant appears at all rather than just how fast it grows — the same
applies to sunlight, nighttime, and other conditions. Mirrors the weather/time-sensitivity pattern
already used for customers — see Weather & Time Sensitivity in [creatures.md](creatures.md).

Which specific plants respond to which conditions isn't mapped out yet — needs a per-ingredient pass
once ingredients are actually defined. Blocked on the weather system existing, same as Rain/Storm in
spells.md.

---

## Potted Plants

The store sells potted plants as purchasable stock, separate from foraging out in the world. A potted
plant can serve either or both purposes:

- **Decorative** — just shop dressing, no gameplay function.
- **Forage source** — placed in/around the shop as a standing ingredient source, picked (and
  respawning) the same as any other foraging spot.

This gives the player a way to bring foraging in-house instead of relying entirely on trips outside —
buy the convenience with Soul Shards, or forage it for free out in the world. Ties into the "Plant
containers" furniture type (bags, chests, barrels) in the Furniture & Display System — see
[game-overview.md](game-overview.md).

**Open question:** does a purchased potted plant yield the same ingredient(s) every time, or is that
randomized/selectable per plant type? Not decided yet.

---

## Collection — The Bag

Foraging doesn't use a one-at-a-time carry. There's a "bag" — a general, always-available implicit
inventory. Functionally an invisible box that can't be thrown or opened and takes no carry-slot space.

- If the player is physically holding a real box, shelf interaction uses that box as normal (bag ignored).
- If hands are empty and the focused shelf accepts something the bag is carrying, the player can place
  from the bag instead.

---

## Where This Connects

- **Potions** — foraged ingredients feed the cauldron; some recipes need no purchased ingredients at
  all, making them pure profit. See [potions.md](potions.md).
- **Spells** — Grow completes a spot's respawn timer instantly; Rain/Storm affect plant growth rate
  and appearance once the weather system exists — see Weather & Time Sensitivity above and Nature
  spells in [spells.md](spells.md).
- **Forest Portal** — one of the ways the player can learn the portal exists is foraging for mushrooms
  and overhearing/discovering something in the process. See [creatures.md](creatures.md).
- **Grimoire** — night-potency and other foraging knowledge lives there once learned.

---

## Ingredient Definitions

Ingredients are not player-editable content — they exist as assets in the project (name, forage
location, respawn timer, day/night potency, weather-growth modifiers, weather-gated appearance, sell
value, whether it's usable in potions), the same way products do in the base template. Plants can't be
added or removed through mods; see Design Principles in [game-overview.md](game-overview.md).
