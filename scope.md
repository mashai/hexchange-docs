# Scope

What's actually required to release Hexchange, what's a real part of the vision but survivable to cut or defer, and what's pure polish. See [game-overview.md](game-overview.md) for how each of these systems actually works — this doc is just the priority triage.

## Need (the game isn't Hexchange without these)

- **Base shop loop** — buy crates, shelve, sell, rent. Already exists (CheckoutFrenzy foundation).
- **Book-opening → rewards** — the "sell sealed vs. open it" choice is the one thing that makes this not-vanilla-CheckoutFrenzy. Can't cut this without cutting the game's premise. Includes book cover/size visual variation (crate copies looking different from each other) — part of the core book-opening fantasy, not separable polish.
- **Foraging/Ingredients** — first in the build order, cheap relative to the others, and it's what makes Spells and Potions actually mean what they're supposed to mean.
- **Tarot** (cards, Divination Table, deck build/disassemble/sell, readings) — second in the build order, and it's the payoff for one of the two starting short-term goals in Progression. Cutting it guts a stated core goal, not a side system.
- **Potions** (cauldron, crafting) — third in the build order. Its value depends on foraging existing, which is why it's last, but it's still part of the same core arc, not an add-on.
- **Customer-inaccessible area** (private potion-ingredient shelf) — small, but Potions' ingredient sourcing as designed depends on it existing.
- **Grimoire UI** — the tracking backbone for everything books grant. Already in progress per current-task.md.

## Want (real part of the vision, but the game survives without it at launch)

- **Artifact passive effects** (attract customers / stats / repel goblins) — could ship as plain sellable decor instead, no passive effects, without breaking anything else.
- **Species-attraction condition system** — already deferred (not mapped yet). Customers can still spawn via the existing weather/time system without it.
- **Forest Portal** — expands the customer roster, serves the "attract every species" story goal, but the game is a complete loop without it — just a smaller roster.
- **Forest Spirits** — a second supply source; the Traveler's UI already covers all necessary supply on its own.
- **Goblins** — adds tension, cheap-ish since it reuses the existing `Thief`/`Guard` system, but a shop-sim doesn't need an active threat to be finished.
- **Helpers** — explicitly mid-late game per game-overview.md; automates stations that work fine manually.
- **Pub/village NPC system** — already filed in its own doc as "planned for later phase after the core shop loop is complete." Not really "want, might cut" so much as already scoped post-initial-release.
- **Crop Field Mystery** — lives entirely inside the pub system, follows its fate.

## Polish (cosmetic/QoL, zero mechanical stakes)

- **Potion-accident/mess mechanic** — already flagged this way in game-overview.md.
- **Chaotic multi-product shelving** — already deferred as a future pass in game-overview.md.
- **Tarot source-deck matching-price economics** — the base loop (collect → assemble → sell or read) works fine with flat pricing; the real-deck collector layer adds depth but isn't structural.
