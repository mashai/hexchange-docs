# Potions

Third system in the build order (see [scope.md](scope.md)) — its value depends on Foraging already
existing, which is why it's last of the three, but it's still core to the game's arc, not an add-on.

---

## The Cauldron

The shop starts with a **broken cauldron** — pure set dressing, non-functional and cannot be repaired.
A working cauldron must be purchased before potion-making is possible at all. It's one of two parallel
short-term goals early on (the other being a full tarot set — see [tarot.md](tarot.md)), and the
nearer-term of the two.

Once bought, potion-making is a genuine trade-off, not a strict upgrade: it's a great way to get extra
money when needed, but it's time-consuming — finding ingredients and brewing both take real effort,
unlike passively reselling crates.

The cauldron has its own dedicated menu (like the PC or till) for mixing ingredients into a potion.

---

## Crafting

- Ingredients are either purchased or foraged (see [foraging.md](foraging.md)); some recipes need no
  purchased ingredients at all, making them pure profit compared to the base buy-and-resell loop.
- Recipes come from Potion Recipes, unlocked by opening Potion Books and kept in the Potion
  Grimoire (a separate book that reuses the Grimoire's assets) — see Books in
  [game-overview.md](game-overview.md). Same book-crate tier gating as spells (see the Spell
  Categories & List intro in [spells.md](spells.md)): a recipe's availability is just a function of
  which crate tier its Potion Book came from, no separate unlock condition.
- Once crafted, the potion goes straight into the player's hands to carry and place on a shelf —
  no private-stock step first (unlike Spells).
- **Sell-only** — potions don't affect any player mechanic directly, and players have no personal
  use for one once made. Their real function is drawing in customers who want specific potions (see
  the Species-Attraction Condition System in [creatures.md](creatures.md)), not something the
  player benefits from beyond the sale itself.

---

## Private Ingredient Storage

Potion-crafting ingredient stock needs its own area customers can't access or buy from — enforced
both physically (a collider/navmesh obstruction) and logically (a flag customers check before ever
considering a shelf for purchase). **Neither system exists yet; both need to be built.** Small in
scope, but the ingredient sourcing above depends on it existing — it's a "Need," not a "Want" (see
[scope.md](scope.md)).

---

## Crafting Interaction

**Minimum version:** open the cauldron menu, pick a known recipe, and if the ingredients are in
stock, the potion crafts instantly.

**Stretch goal — timed crafting:** not required for the core loop. Ingredients need to be added at
the right timing during the brew; getting it wrong risks the potion exploding — see Crafting
Accidents below. This is what actually gives Crafting Accidents something to happen from — under
the minimum version there's no timing to get wrong, so no accidents either.

---

## Crafting Accidents

Crafting accidents create a mess that only a spell can clean (Cleaning I — see
[spells.md](spells.md)). **Polish/stretch goal — build if time allows**, and depends on the timed
crafting stretch goal above existing in the first place. Doesn't block potion-making; unresolved
messes just keep accumulating and may deter customers. Not a progression trap: Cleaning I is an
early-stage spell, easy to get from books early.

---

## Potion Maker (Helper)

An invocation spell (see [spells.md](spells.md)) can summon a Potion Maker helper. Rather than
drawing from the player's full known-recipe list, the player curates a preferred-potions list; the
Helper checks that list against currently available ingredients and brews whenever it has enough
for one of them, stocking the result itself. Mid-late game — removes grind, not agency.

The base template's Employee work-loop pattern (see `Stocker.cs`/`Sorter.cs`: a `LocateTargets()`
check followed by a retrieve → act → rest coroutine) is a reasonable base to extend — a Potion
Maker's `LocateTargets()` would check the preferred list against available ingredients instead of
"does a shelf need stock."

---

## Data-Driven Note

Potion recipes (ingredients, quantities, output effects) are explicitly in scope for player editability —
see Design Principles in [game-overview.md](game-overview.md).
