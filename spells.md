# Spells

One of four things a book can grant (see Books in [game-overview.md](game-overview.md), alongside
Tarot Cards, Knowledge, and Potion Recipes). This doc covers the spell system on its own — inventory,
use, and what spells are actually good for.

---

## Discovery & Private Stock

A found spell goes into the player's private stock. The Grimoire's Spells page doubles as both a
discovery log and a live inventory: each spell type shows an icon with the currently-owned quantity
underneath.

---

## Use vs. Take

Hovering a spell in the Grimoire pops up its effect description with two actions (verb names TBD):

- **Use** — triggers the effect, destroys 1 copy.
- **Take** — removes 1 copy from private stock into the player's hands, to carry and place on a
  dedicated spell shelf for customers to buy individually.

Individual spell sales exist alongside sealed spell books so a spell the player doesn't personally want
still has value instead of being a dead end.

Once stocking automation is unlocked, **Take** can instead auto-place the spell on the correct shelf
directly — manual carry-and-place early game, automatic once the relevant Helper exists.

---

## Display

Spells are displayed as scrolls (rolled) on a dedicated scroll display furniture piece — exact style
TBD. See Furniture & Display System in [game-overview.md](game-overview.md).

---

## What Spells Are For

Beyond selling, spells prove useful well past the early game:

- Speeding up ingredient plant growth — ties to Foraging respawn timers, see [foraging.md](foraging.md).
- Customizing the shop.
- Changing the local climate.
- Actively creating the conditions certain customers need to show up — ties to the species-attraction
  condition system, see [creatures.md](creatures.md).
- Increasing the odds of finding rare items when opening books.
- Cleaning up potion-crafting accidents — see [potions.md](potions.md).
- Repelling goblins for a limited number of uses/duration — see [goblins.md](goblins.md).

---

## Invocation Spells → Helpers

A specific spell category, "Invocation," summons Helper assistants once the relevant station exists
(mid-late game): Potion Maker, Shelf Restocker, Cashier, a Divination Table operator (name TBD), others
TBD. Design intent: remove grind from tasks the player has already mastered, not remove player agency —
the game should still be about what the player chooses to focus on, not watching it play itself.

---

## Spell Categories & List

Four categories, each covering a distinct kind of effect. Spells have no unlock condition of their
own — a spell becomes available purely by which book crate tier it's found in. Pricier, more
advanced crates yield more advanced book contents (see Books in [game-overview.md](game-overview.md)),
so a Mid-tagged spell simply won't turn up in an early-tier crate's books. The Stage tags below are
shorthand for that crate-tier gating, not a level gate or any other kind of unlock check.

No weather system, plant-growth system, player health/stamina system, or goblin/thief-ward system
exists in the codebase yet. The Employee AI pattern (`Cashier.cs`, `Stocker.cs`, `Sorter.cs`,
`Janitor.cs`, `Security.cs`) is a strong head start for Invocation's Helper spells. The base
template's Cleaning pipeline (`Cleaner.cs` / `Cleanable.cs` / `CleaningTool.cs`) exists but isn't
reusable for the Cleaning spell — see Household below for why.

### Nature

Discovery order: **Show magical scents → Rain → Storm → Grow.**

| Spell | Effect | Stage | Code Effort |
|---|---|---|---|
| Show magical scents | Activates a particle effect on every forageable item currently in the world, making them easy to spot at a glance | Early | Low-Moderate — no target-selection or pathing needed, just toggling a VFX on the existing set of forageable spawns once that spawn system exists |
| Rain | Changes weather to rain; speeds growth for certain plants and can make some plants appear that otherwise wouldn't (see Weather & Time Sensitivity in [foraging.md](foraging.md)), raises spawn odds for certain creatures (e.g. mushroom folk) | Early | Moderate — the weather simulation itself comes from a purchased Unity Asset Store package, not built from scratch; the coding work is wiring growth-rate, plant-appearance, and spawn-chance hooks off that asset's weather state |
| Storm | Changes weather to storm; raises spawn odds for certain creatures | Early-Mid | Moderate — shares the purchased weather asset Rain needs; name/effect still flagged as unsettled in the source material |
| Grow | Instantly completes the respawn timer for foraged spots in range | Mid | Low-Moderate — the same clock as Foraging's existing respawn timer (see [foraging.md](foraging.md)), not a separate growth-stage system; Foraging itself is simple, so this is a small addition once that timer exists in code |

Show magical scents moved to first now that its effort dropped from High to Low-Moderate (see
Resolved note below) — it's the cheapest spell in the category and the one with the fewest
dependencies (no weather asset, no target-selection system), so it makes sense as the very first
Nature spell a player finds rather than the last. Rain/Storm/Grow keep their original relative
stages, unaffected by the reorder — Show magical scents sits alongside Rain at Early rather than
displacing it.

Resolved: earlier drafts considered a directional trail toward a single "best" ingredient, which
needed a target-selection system (nearest uncollected item, current recipe needs, or player choice)
before any pathing work could start. Simplified instead to a flat reveal — every forageable in the
world gets the particle effect at once, no target selection required. That simplification is what
made moving it to first, above, possible — the old High-effort version wasn't a realistic first spell.

### Household

| Spell | Effect | Stage | Code Effort |
|---|---|---|---|
| Goblin Repellant | Repels goblins for a limited number of uses/duration | Mid | Low-Moderate, but blocked on Goblins existing at all (see [goblins.md](goblins.md)) — reuses Thief/Guard with an added ward check |
| Cleaning I | Clears a potion-crafting-accident mess (see Crafting Accidents in [potions.md](potions.md)) | Early | Moderate — a new mess system scoped specifically to potion accidents; the base template's general Cleanable/Cleaner/CleaningTool pipeline isn't reusable here |
| Cleaning II | Same as Cleaning I; longer-lasting/more thorough | Mid-Late | Low incremental, once Cleaning I's mess system exists |
| Touch of luck (I/II/III) | Better odds of rare results from books/potions | Mid | Moderate — needs a luck-multiplier hook into book-opening RNG once that system exists |
| Wall Material spells | Not a single "Change the Walls" spell — a separate spell per material/texture (moss, brick, tapestry, etc). Specific material list and spell names not decided yet. | Early (one of the very first spells found) | Moderate for the first one (needs a wall-material-swap system to exist at all); Low incremental for each material after that (just a new texture reference once the swap system exists) |

**Cut:** Self-stirring spoon — appeared in early brainstorming as both a spell and an artifact idea,
but there's no cauldron/potion-crafting system to hook it into yet. Dropped rather than parked;
revisit if it comes up again once Potions exists.

### Invocation

Summons Helper assistants once the relevant station exists (see Invocation Spells → Helpers,
above). Like Wall Material spells, **Invoke Creature isn't a single spell** — there's a separate
invoke spell per creature (Invoke Cat, Invoke Goblin, Invoke Kobold, etc.), matching the "different
spells will invoke different creatures" note in the source material.

**Open Question:** whether Invoke Minor Demon follows the same one-spell-per-demon pattern (imp,
demon, succubus) isn't confirmed — assumed here by analogy to Invoke Creature.

| Spell | Effect | Stage | Code Effort |
|---|---|---|---|
| Invoke Creature spells (one per creature) | Summons a specific Helper (cat/goblin/kobold/etc) to run a station (till, stock, tarot readings) | Mid-Late | Moderate for the first one — `Employee.cs`/`Cashier.cs`/`Stocker.cs`/etc. are a working pattern to extend; Low incremental for each additional creature once that Helper-summon system exists |
| Invoke Minor Demon spells (one per demon, inferred) | Same pattern, reskinned (imp/demon/succubus); may instead grant a large request | Late | Low incremental, once Invoke Creature's system exists |
| Invoke artifact | Grants a choice of 1 artifact from a pool that grows with spell level (level 1 = pick from 2, level 2 = pick from 5, level 3 = pick from 8 — numbers not finalized) | Late | Moderate — needs a "choose 1 of N" reward UI, doesn't exist yet but is self-contained |

### Physical / Healing — Parked

Both spells in this category are parked for now, not scheduled to any stage.

| Spell | Effect | Code Effort |
|---|---|---|
| Healing | Minor player heal | Blocked — no player health/stamina system exists, and whether one ever gets built is an open game-design question, not a code one. An idea was floated tying this to a "witch must sleep after X hours" mechanic that also isn't decided. |
| Glamour (I/II/III) | Changes player appearance | Unknown — depends on whether the player avatar supports outfit/appearance layers at all; an art question before it's a code question |

---

## Editability

Resolved: spells are **not** in scope for player editability, unlike tarot decks, books, potion
recipes, and creature definitions. Those are pure data; every spell effect above needs actual code
to implement (a weather hook, a growth-stage hook, a new mess system, a Helper-summon system,
etc.) — there's no data file a player could edit to get a new working spell out of it. Worth
revisiting game-overview.md's Design Principles → Player Editability section so it reflects this —
spells currently aren't mentioned in either its "in scope" or "not editable" list.
