# Current Tasks

## Sprint Goal (2 weeks)
Get Book Product working end-to-end — create it as a product, open it, and receive its rewards (tarot cards, spells, etc.).

1. ✅ Done — Rewire the prompt system to support the upcoming "open book" prompt.
2. 🔵 WIP — Grimoire UI — the central hub replacing the PC. Covers:
   - Shop (ordering functionality migrated from PC)
   - Tarot page — display + underlying Tarot Card/source-deck data structure
   - Spells page — display + underlying Spell data structure
   - Potion Recipes page — display + underlying Potion Recipe data structure
3. ⬜ Book Product — book as a purchasable product (model, data definition).
4. ⬜ Book-opening logic — grants rewards into the player's collection when a book is opened.
5. ⬜ Book Setup System — editable odds/percentages for what a book can grant (tarot, spells, etc.); needs the underlying tarot/spell infrastructure to exist first.
6. ⬜ Book Opening Experience — the full process of opening a book: animation, UI, and a skip option.

## Ongoing Decision
- PC's shop functionality is migrating into the Grimoire (item 2); the PC gets removed once that migration is complete.

## Backlog (low priority, not blocking)
- Redo navmesh — customers currently walk through walls, and should also be blocked from zones the player can still access.
- Grimoire: Knowledge page and Bestiary page — both deliberately left out of this sprint's Grimoire work. Knowledge in particular is expected to be a hard one; revisit later.
- Delivery Box — will need changing to support book delivery, but not this sprint's focus.
