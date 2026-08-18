# Game Overview

## Concept

A cozy-dark shop management game where you play as a witch running a magic shop after making a mysterious bargain with an entity known as the Traveler (also called Old Nick, the Gentleman, Papa Legba, the Horned One, the Collector). The price of the bargain is never revealed.

## Opening Narrative (TBD)

> He goes by many names. Old Nick, the Gentleman, Papa Legba, the Horned One, the Collector…
>
> I knew him as the Traveler. And like so many others before me, I made a bargain.
>
> A shop of my own, and all the knowledge I could ever want.
>
> Was the price worth it?
>
> Maybe, maybe not.
>
> Only time will tell. But at last… the shop was mine.

## Starting State

The player begins with an empty shop containing:
- A till
- Empty shelves
- A summoning circle (used for deliveries)
- A broken cauldron — pure set dressing. Non-functional and cannot be repaired; a working cauldron must be purchased before potion-making is possible at all (see Potions below).

## Currency

- **Soul Shards** — used to purchase stock from the Traveler's UI (players are left to guess the source)

## Core Loop

1. Purchase boxes of books using Soul Shards, and forage ingredients (herbs/flowers) — out in the world, or from potted plants in/around the shop (see [foraging.md](foraging.md))
2. Boxes appear in a burst of flames in the summoning circle
3. Open boxes and place books (and foraged ingredients) on shelves
4. Customers come in and buy books and ingredients
5. Use profit to buy better stock and expand the shop
6. Pay monthly rent to stay afloat

This is the loop the player starts with — no cauldron, no Divination Table. See Progression below for how it evolves.

## Progression

The overall arc, roughly in order. No explicit win condition, but the implicit story goal is attracting/discovering every customer species (tracked via the Bestiary).

1. **Start:** just the Core Loop above — buy and open books, forage and sell ingredients.
2. The player discovers opening books grants knowledge/tarot cards/spells/potion recipes, not just resale value — opening a book becomes a real strategic choice (sell it sealed vs. open it) rather than "just resell everything."
3. Two parallel short-term goals emerge: save up enough money to purchase a working cauldron (nearer-term), and collect enough tarot cards for a full set to unlock purchasing the Divination Table (longer-term, takes a while). Money is also an ongoing lever here, not just a one-time gate: better book crates cost more but yield better books, and crucially can be **specialized** — nature-themed, spell-themed, potion-themed, etc. — letting the player skew their odds toward the kind of content they're currently chasing instead of pulling from flat, uniform odds.
4. Once the cauldron is bought, potion-making is a genuine trade-off, not a strict upgrade: it's a great way to get extra money when needed, but it's time-consuming — finding ingredients and brewing both take real effort, unlike passively reselling crates.
5. Spells prove useful well beyond just selling them: speeding up ingredient plant growth, customizing the shop, changing the local climate, actively creating the conditions certain customers need to show up, and increasing the odds of finding rare items when opening books.
6. Economic snowball: more money → better crates/better books → better spells, tarot, and knowledge.
7. Mid-game narrative pivot: through pub conversation or exploration (e.g. foraging for mushrooms), the player learns about a portal in the forest that brings customers from around the world — widening the pool of customer species available. See Forest Portal below for the mechanic.
8. New-customer-variety loop: books grant Bestiary knowledge about creatures — what potions or conditions attract a given species. Gameplay becomes figuring out what each species needs and providing it, directly serving the "attract every species" story goal.
9. Mid-late game: Helpers unlock (activated by spells found in certain book types) and start automating stations the player has built up — potions, till, Divination Table, shelf restocking.

**Systems this arc touches that aren't designed yet** (confirmed as part of the plan, not "out of scope" — just no detail worked out):
- The condition-matching system for what attracts a given customer species (spells can now manufacture some of these conditions directly — see Progression #5 — but which species need which conditions isn't mapped out) — see [creatures.md](creatures.md)
- Forest Spirits — a second, barter-capable marketplace — see [creatures.md](creatures.md)
- Goblins — a theft threat and its countermeasures — see [goblins.md](goblins.md)
- **The pub/village social layer is the exception — it's already fully designed, just not built.** See [the-village.md](the-village.md) for the cast and tone, and [npc-dialogue-and-relationships.md](npc-dialogue-and-relationships.md) for the dialogue/relationship engine spec. Both are marked "Not started, planned for later phase" — this game-loop pivot is what motivates building it.

## Content Systems

### Books
- Opened to discover and collect their contents
- Basic Spell Books available at the start; better books unlock with progression
- Book quality affects the rarity and value of what's inside
- Lifecycle: only two fates, nothing else — sold to a customer sealed (normal purchase), or opened by the player (grants contents, then removed from stock). Never just sits there indefinitely.
- Crate variety: a crate contains multiple copies of the same book (same stats/contents odds), but each physical copy should look different — different size and cover art, randomized at spawn from a shared texture pool. A book rare/important enough to be sold and read individually (not just rolled from a crate) simply has a pool of exactly one texture — same randomization code path either way, no special-casing needed.

### What Books Contain
- **Spells** — found spells go into the player's private stock, sellable individually or usable directly. See [spells.md](spells.md) for the full discovery/inventory/use spec.
- **Tarot Cards** — collectible only, never sold or interacted with individually. Every card belongs to a "source deck" — real historical tarot deck editions (Rider-Waite, Marseille, Thoth, etc.), not invented in-universe ones, so art comes from sourcing/adapting existing decks rather than designing new ones from scratch (double-check public-domain/rights status per deck before committing art — Rider-Waite-Smith, 1909, is confirmed PD). Collecting a full matching-source set can take a while, so a functional deck can be assembled from mixed sources, but a deck built entirely from one source sells for more. See Tarot below for the full lifecycle.
- **Knowledge** — added to the Grimoire; never sold
- **Potion Recipes** — unlocked from Potion Books; used to craft potions

### Ingredients
Foraged outside the shop, sold directly or used in potions, on a per-item respawn timer. See [foraging.md](foraging.md) for the full spec.

### Forest Portal & Forest Spirits
A stone circle that expands the customer roster once ritually activated, and a second barter-capable supply marketplace encountered in the forest. See [creatures.md](creatures.md) for both.

### Potions
Requires a purchased, working cauldron (see Starting State above). See [potions.md](potions.md) for crafting, the Potion Maker helper, and the accident/mess stretch goal.

### Tarot
Cards collected from books, never sold individually (see What Books Contain above). Collecting a full set unlocks the Divination Table. See [tarot.md](tarot.md) for the full deck lifecycle, pricing, and readings.

### Grimoire
Collects everything the player has learned:
- **Knowledge** — passive lore and gameplay hints (e.g. flowers more potent at night, vampires more likely on cloudy days, sell X potions to trigger Y)
- **Spells** — all discovered spells; doubles as the player's live spell inventory (see What Books Contain above)
- **Potion Recipes** — all discovered recipes
- **Tarot Deck** — card collection progress
- **Bestiary** — log of all customer types encountered; also the knowledge source for what conditions attract a given species (see Progression above)

### Artifacts
- Purchased as store supply, sellable to customers like any other product
- Also grant an ongoing **passive effect** while displayed — attracting certain customers, granting shop-wide stats, or permanently repelling goblins (see Customer System below). This is a third product-behavior pattern distinct from both plain commodities (potions, ingredients) and one-time-triggered-and-consumed items (books, spells, tarot decks).
- The passive effect is active purely because a physical instance exists somewhere in the shop — independent of whether that location is reachable by customers. An artifact stashed in a customer-inaccessible area (see Private Ingredient Storage in [potions.md](potions.md)) still grants its effect, it just can't be sold from there. The effect stops the moment a customer buys/removes it.

### Helpers (via Spells)
"Invocation" spells summon assistants, unlocked mid-late game once the relevant stations exist. Design intent: these exist to remove grind from tasks the player has already mastered, not to remove player agency — the game should still be about what the player chooses to focus on, not watching it play itself.
- Potion Maker
- Shelf Restocker
- Cashier
- A Divination Table operator (name TBD)
- (others TBD)

## Customer System
Various customer types with different behaviours, preferences, and weather/time sensitivity, tracked in the Bestiary. See [creatures.md](creatures.md) for customer types, species groups, the Bestiary, and the (undesigned) per-species condition details.

**Goblins** steal items from the shop instead of buying them, as a preventable-not-just-reactive threat layered on the base template's existing `Thief`/`Guard` system. Not designed yet — see [goblins.md](goblins.md).

## Economy
- Monthly rent creates ongoing financial pressure
- Progression tied to profit — better books, more mechanics, more customer types

## Design Principles

### Player Editability
The game should be easy for players to mod and customise. Game content — not core engine logic — should live in external, human-readable data files so players can edit them without touching code.

**In scope for editability:**
- Tarot card decks (card names, imagery, effects, source decks)
- Book definitions (stats, rarity, what contents they can yield and in what quantities/probabilities)
- Potion recipes (ingredients, quantities, output effects)
- Creature/customer definitions (spawn conditions, preferences, behaviours)

**Not editable (core engine logic):**
- Shop mechanics and economy rules
- UI and scene structure
- Save/load system
- Spells — every spell effect needs actual code (a weather hook, a growth hook, a new mess system, a
  Helper-summon system, etc.); there's no data file that produces a working spell on its own. See
  Editability in [spells.md](spells.md).
- Ingredient/plant definitions — exist as in-project assets, the same way products do in the base
  template, not external data. Plants can't be added or removed through mods. See
  [foraging.md](foraging.md).

**Approach:** Two tiers, decided case by case:
- **ScriptableObjects** — developer-facing content, edited in the Unity Inspector, not exposed to players
- **JSON files** — player-facing content, editable in any text editor without Unity installed

These choices may change as the project progresses. Decide per system when we get to it.

---

## Furniture & Display System

### Furniture Types

| Furniture | Accepts | Notes |
|---|---|---|
| Bookcase / Shelf | Books, Potions, Artifacts | General display surface |
| Table | Books, Potions, Artifacts | Books pile differently than on shelves |
| Chair | Books (piled) | Freeform, player-placed |
| Plant containers (bags, chests, barrels) | Plants/Ingredients only | Cannot hold books, potions, spells, etc. |
| Scroll display | Spells only | Scrolls, fanned or propped — TBD exact style |
| Tarot Display Stand | Tarot Decks only | Dedicated stand — TBD exact style |
| Magical Stasis furniture | Special artifacts / potions | **Out of scope for now** |

### Display Style by Item Type
- **Books** — stacked/piled; style varies by furniture (neat rows in a bookcase, loose pile on a table or chair)
- **Spells** — displayed as scrolls (rolled), dedicated scroll display only
- **Potions** — bottles/vials
- **Ingredients** — loose, in containers
- **Tarot Decks** — dedicated display stand only

### Slot System — future target, not current implementation
Documented intent: display managed at the **slot level**, not the shelf level, with each slot defining allowed/excluded item types, lock behaviour (once an item is placed, only more of the same type can join, until emptied), and stacking rules (orientation, random rotation).

**Current state: simplified to one product type per shelf**, matching what's actually implemented (`Shelf.cs`, a single `AssignedProduct` per shelf) and everything designed in the product-interaction architecture pass. A future pass will revisit shelving and stocking specifically to create a feeling of chaotic, organic organization — being able to place different products side by side — though not necessarily identical to the exact per-slot mechanics described above; that's a direction, not a locked spec.

### Key Design Note
This is a meaningful departure from the base template, which assigns one product type to the whole shelf — though for now we've kept that base-template behavior deliberately, revisiting it later per the note above.

---

## Base Template
Built on top of the **CheckoutFrenzy** Unity asset as a starting point, heavily modified to fit this concept.

---

## Future Ideas (Out of Scope for Now)

Captured for later consideration — do not design or build toward these until explicitly scoped in.

- (Nothing currently parked here — the village/pub social layer used to be listed as a vague future idea, but it's actually fully designed already; see [the-village.md](the-village.md) and [npc-dialogue-and-relationships.md](npc-dialogue-and-relationships.md), status "Not started, planned for later phase.")
