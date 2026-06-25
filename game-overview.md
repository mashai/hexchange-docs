# Game Overview

## Concept

A cozy-dark shop management game where you play as a witch running a magic shop after making a mysterious bargain with an entity known as the Traveler (also called Old Nick, the Gentleman, Papa Legba, the Horned One, the Collector). The price of the bargain is never revealed.

## Opening Narrative

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
- A cauldron (empty, non-functional until the player receives their first Potion Recipe — shortly after which the self-stirring spell becomes available)

## Currency

- **Soul Shards** — used to purchase stock from the Traveler's UI (players are left to guess the source)

## Core Loop

1. Purchase boxes of books using Soul Shards
2. Boxes appear in a burst of flames in the summoning circle
3. Open boxes and place books on shelves
4. Customers come in and buy books
5. Use profit to buy better stock and expand the shop
6. Pay monthly rent to stay afloat

## Content Systems

### Books
- Opened to discover and collect their contents
- Basic Spell Books available at the start; better books unlock with progression
- Book quality affects the rarity and value of what's inside

### What Books Contain
- **Spells** — activatable with various effects; can also be sold
- **Tarot Cards** — collectible; can be sold individually, as a pack, or kept for a full deck
- **Knowledge** — added to the Grimoire; never sold
- **Potion Recipes** — unlocked from Potion Books; used to craft potions

### Flowers
- Picked up from outside the shop
- Sold directly or used as potion ingredients
- Some are more potent at night (learned through the Grimoire)

### Potions
- Crafted using Potion Recipes + flowers
- Sold in the shop

### Tarot
- Cards collected from books
- Build toward a full deck
- **Tarot Table** (purchasable): use cards to read fortunes, attract more customers
- A complete deck unlocks additional customer-draw bonuses

### Grimoire
Collects everything the player has learned:
- **Knowledge** — passive lore and gameplay hints (e.g. flowers more potent at night, vampires more likely on cloudy days, sell X potions to trigger Y)
- **Spells** — all discovered spells
- **Potion Recipes** — all discovered recipes
- **Tarot Deck** — card collection progress
- **Bestiary** — log of all customer types encountered

### Helpers (via Spells)
Certain spells summon assistants:
- Potion Maker
- Shelf Restocker
- Cashier
- (others TBD)

## Customer System
- Various customer types with different behaviours and preferences
- Some are weather/time sensitive (e.g. vampires on cloudy days)
- Tracked in the Bestiary

## Economy
- Monthly rent creates ongoing financial pressure
- Progression tied to profit — better books, more mechanics, more customer types

## Design Principles

### Player Editability
The game should be easy for players to mod and customise. Game content — not core engine logic — should live in external, human-readable data files so players can edit them without touching code.

**In scope for editability:**
- Tarot card decks (card names, imagery, effects)
- Book definitions (stats, rarity, what contents they can yield and in what quantities/probabilities)
- Potion recipes (ingredients, quantities, output effects)
- Creature/customer definitions (spawn conditions, preferences, behaviours)

**Not editable (core engine logic):**
- Shop mechanics and economy rules
- UI and scene structure
- Save/load system
- Spell activation logic

**Approach:** Two tiers, decided case by case:
- **ScriptableObjects** — developer-facing content, edited in the Unity Inspector, not exposed to players
- **JSON files** — player-facing content, editable in any text editor without Unity installed

These choices may change as the project progresses. Decide per system when we get to it.

---

## Furniture & Display System

### Furniture Types

| Furniture | Accepts | Notes |
|---|---|---|
| Bookcase / Shelf | Books, Potions, Artifacts, Scrolls, Tarot | General display surface |
| Table | Books, Potions, Artifacts, Scrolls, Tarot | Books pile differently than on shelves |
| Chair | Books (piled) | Freeform, player-placed |
| Plant containers (bags, chests, barrels) | Plants/Flowers only | Cannot hold books, potions, spells, etc. |
| Tarot Display Stand | Tarot Cards only | Cards fanned or propped — TBD exact style |
| Magical Stasis furniture | Special artifacts / potions | **Out of scope for now** |

### Display Style by Item Type
- **Books** — stacked/piled; style varies by furniture (neat rows in a bookcase, loose pile on a table or chair)
- **Spells** — displayed as scrolls (rolled)
- **Potions** — bottles/vials
- **Plants/Flowers** — loose, in containers
- **Tarot Cards** — dedicated display stand only (for now)

### Slot System
Display is managed at the **slot level**, not the shelf level. Each slot on a piece of furniture defines:

- **Allowed / excluded item types** — set per slot on the furniture definition
- **Lock behaviour** — once an item is placed in a slot, only more items of the same type can be added; reverts to open state when the slot is emptied
- **Stacking rules** — defined per slot:
  - Orientation: vertical or horizontal
  - Random rotation: on or off (applied per item added)

This means a single shelf can have slots with different rules — e.g. one slot stacks books horizontally with no rotation, another stacks potions vertically with slight random rotation.

### Key Design Note
This is a meaningful departure from the base template, which assigns one product type to the whole shelf. Here control is at the slot level, giving the player much more layout freedom. Will need a custom display/placement system when we build it.

---

## Base Template
Built on top of the **CheckoutFrenzy** Unity asset as a starting point, heavily modified to fit this concept.

---

## Future Ideas (Out of Scope for Now)

Captured for later consideration — do not design or build toward these until explicitly scoped in.

- **Village pub** — leave the shop and interact with NPCs in the wider world
