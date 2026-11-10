# Current Tasks

## Sprint Goal (2 weeks)
Get Book Product working end-to-end — create it as a product, open it, and receive its rewards (tarot cards, spells, etc.).

1. ✅ Done — Rewire the prompt system to support the upcoming "open book" prompt.
2. 🔵 WIP — Grimoire UI — the central hub replacing the PC. Covers:
   - Shop (ordering functionality migrated from PC). Current build buys immediately with no cart; the design is now a catalog grid (left) and a signed parchment checkout with a cart (right) — see Grimoire in game-overview.md
   - Tarot page — display + underlying Tarot Card/source-deck data structure
   - Spells page — display + underlying Spell data structure
   - Potion Recipes — display + underlying Potion Recipe data structure; lives in a separate Potion Grimoire that reuses the Grimoire's assets
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
- Weather Maker performance profiles — currently pinned to a single manual profile (`WeatherMakerPerformanceProfile_Default`) with `Auto Set Performance Profile` off, because the project only has one Unity Quality Settings tier ("Standard"). Weather Maker's auto-detection expects 3-6 tiers to map profiles against. Once real Low/Medium/High quality tiers + a graphics settings menu exist (a release-polish concern, not now), build matching URP Render Pipeline Assets per tier and re-enable auto-detection, or wire the profile selection to the settings menu manually.
