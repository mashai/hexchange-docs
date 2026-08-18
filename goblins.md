# Goblins (Thieves)

> **Not designed yet.** This is a scaffold, not a finished spec — game-overview.md lists goblins among
> the systems this game's arc touches that aren't designed. Deliberately barebones; fill in as we go.
> Scope: "Want" tier (see [scope.md](scope.md)) — adds tension, cheap-ish since it reuses an existing
> system, but not required for a complete shop-sim loop.

---

## What We Have

- Goblins steal items from the shop instead of buying them.
- The base CheckoutFrenzy template already ships a **reactive** theft mechanic: `Thief.cs` + a `Guard`
  component under `Assets/CheckoutFrenzy/Scripts/Gameplay/Theft/` — you catch them after the fact via a
  Guard.
- The intended goblin countermeasures are **preventative**, not just reactive:
  - A spell repels goblins for a limited number of uses/duration — Goblin Repellant, already
    designed, see Household in [spells.md](spells.md).
  - An artifact repels them permanently while displayed (see Artifacts in
    [game-overview.md](game-overview.md)) — not designed yet, deferred to the full content pass (see
    Minimum below).

---

## Open Question — Relationship to the Existing Thief/Guard System

Whether the spell/artifact wards **replace**, **reduce**, or **layer on top of** the existing reactive
Thief/Guard system isn't decided. Read `Thief.cs`/`Guard` before assuming either way — don't design
goblins in a vacuum from what's already in the template.

---

## Minimum to Get Goblins Working At All

- Reuse the existing Thief prefab/behaviour (steal item, flee) rather than building a new creature type.
- One repel mechanism for the first pass — the Goblin Repellant spell (already in spells.md). The
  artifact version is real to the vision but deferred until core mechanics are proven out; add it back
  in during the full content pass.
- Goblins are now listed as a Forest Creature customer species in [creatures.md](creatures.md), but
  their rarity/preference data there is still an unfilled placeholder — for this minimum pass, treat
  them purely as a hazard; a real Bestiary entry can wait until that placeholder data gets a proper
  design pass.

---

## Perfect World / Cool Ideas (not committed)

- Goblins scale with shop value or stock on hand — more to steal, more incentive to visit.
- Different goblin "tiers" (a sneaky one vs. a bold one that fights the Guard).
- A Guard upgrade path funded by shop profit.
- Goblins drop something when caught or repelled — petty loot, or a piece of Bestiary knowledge about
  them.
- A real goblin Bestiary entry once the placeholder species data in [creatures.md](creatures.md) gets
  a proper design pass, so "what attracts goblins" becomes part of the same system as legitimate
  customers instead of a special case.

---

## Open Questions

- Do goblins spawn like customers (walk in, browse, then steal) or behave differently from the start?
- Does catching a goblin via Guard return the stolen item, or is it lost either way?
- Is there a cost to being a repeated goblin target (reputation, rent pressure), or is it purely a
  stock-loss nuisance?
- Are goblins ever a story beat, or purely a mechanical hazard?
