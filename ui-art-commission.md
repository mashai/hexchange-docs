# UI Art Commission — Grimoire, Ledger & Parchment

The first UI art commission for Hexchange. Covers the three book/paper UI families only: the
Grimoire (and the Potion Grimoire, which reuses its assets), the Ledger, and parchment. Purpose:
Steam page screenshots, in-game feel, and a UI test.

Two artist-facing documents are produced from this one:
- **Intro scope** — short, sent on first contact.
- **In-depth scope** — sent to interested artists; covers every mechanism the UI has to work with.

See [game-overview.md](game-overview.md) for the Grimoire, Potion Grimoire, Ledger and The Contract,
and [demo.md](demo.md) for the demo states.

---

## In Scope / Out of Scope

**In scope**
- Grimoire — inside covers, pages, section layouts
- Potion Grimoire — inside covers; everything else reuses the Grimoire's assets
- Ledger — inside covers, pages, layout
- Parchment — see Parchment below

**Out of scope**
- Main HUD and icons. Both stay on placeholder assets (current icon pack and self-made frames) for
  now and will be replaced later. The new assets have to sit alongside them in the meantime. A
  later HUD/icon pass may be offered as follow-up work.
- 3D models, environments, characters, tarot card illustrations.
- Sigils (player and customer) — handled in-house.

---

## Shared Requirements

Apply to the Grimoire, Ledger and parchment alike.

- **Production-ready for Unity** — sliced, implementation-ready assets, not mockups.
- **One visual family** — same style and visual direction across all three.
- **Fonts** — current fonts are cleared for commercial use and stay. The artist may swap in another
  free, commercial-use font.
- **Live text** — no text baked into artwork. The game has a language selector, so layouts leave
  room for longer translations.
- **States** — collected / not yet collected, locked (demo, "Full Game"), hover / selected, empty.
- **Readability** — legible at 1080p in dim scenes; ornament and wear never compete with content.
- **Page flipping and effects** — worked out together with the artist. Effects in this commission:
  blood-drop signing and parchment burning away.
- **AI use** — AI tools may be used during the process. Final delivered assets must be human-made;
  AI-generated images, including AI-generated images with edits or paintovers, are not accepted.

---

## Reference Material

- **Pinterest board** — overall vibe and aesthetic. Link: TBD.
- **Shared references** — one set covering all three families, since they share a style. Each
  reference is laid out the same way:

  | Reference | What works | What doesn't | What to take from it |
  |---|---|---|---|
  | (image) | | | |

- **Temporary assets** — current AI-generated placeholder pages, shown as layout and intent only.
  Labelled clearly as placeholders, not the style to match.
- **Game screenshots** — in the forest, in the village, inside the shop. For look and vibe.
- **Environment and character asset packs** in use:
  - Forest — [FANTASTIC - Ancient Forest](https://assetstore.unity.com/packages/3d/environments/fantastic-ancient-forest-281914)
  - Village — [Pure Village](https://assetstore.unity.com/packages/3d/environments/pure-village-269090)
  - Villagers — [Stylized Modular Human Male](https://assetstore.unity.com/packages/3d/characters/stylized-modular-human-male-178646)
- **Icon pack** — [The Creative Icon Pack III](https://www.artstation.com/marketplace/p/DG1r/the-creative-icon-pack-iii), used for current icons.
- **Current fonts** — all cleared for commercial use (files in `Assets/TextMesh Pro/Fonts/`):

  | Font | Used for |
  |---|---|
  | Deutsche Uncialis | Page headers — The Grimoire, Store, Profile, Spells, Tarot, Knowledge, Potion Recipes |
  | Caveat (Regular, Bold) | Handwritten text — the Grimoire's first-page text, Today's Summary / Ledger labels and values, Profile stats and progress labels, day/time and currency |
  | Ostrich Sans Rounded (Medium) | Grimoire top-bar menu, filter prompts, pause menu, action prompts |
  | TeX Gyre Adventor | Small functional labels — toggles, level, Continue button, messages |

  Liberation Sans (Unity's default) still appears on some Grimoire elements — dropdowns, mission text,
  page arrows — as leftovers, not a chosen font.

---

## Books

### Common to all books

- Books are only ever shown open, never closed.
- **Inside covers** — the first and last spreads show the inside cover alongside a distinct first
  page and a distinct last page.
- **Inside pages** — several variants that look slightly different from each other, so the book
  doesn't read as one repeated sheet.
- **Interchangeable** — any page variant works in any section.
- **Spine position** — the open book in three states, so the page stack reflects where the player
  is: spine close to one side (near the start), centered (middle), close to the other side (near the
  end).
- **Wear** — some pages carry stains, blood stains, potion stains, burnt edges or torn edges. Subtle,
  with good variety across the set. Wear is kept on separate layers so it can be mixed and matched
  across page variants.
- **Layouts and section assets** — the artist designs each section listed below, following these
  guidelines, and produces whatever assets and UI elements each section needs.
- **Buttons and icons** — the current temporary buttons and icons may be reused (e.g. Ledger inventory
  icons); replaced in a later pass.

### Grimoire

The central hub; replaces the PC. Sections and the information each one shows:

- **Store** — products and furniture to order, across both pages:
  - **Left page — catalog:** all store items in a grid, searchable and filterable by category.
  - **Right page — checkout:** sheets of parchment stacked on top of one another. The top sheet is the
    cart, listing every item added and the total. To buy, the player signs it with their sigil; it
    burns away, leaving the next parchment underneath ready for a new order.
  - States: normal; demo version with locked crate tiers (greyed, lock, "Full Game" tag);
    unavailable items. Locked items have to read as intentional, not broken.
  - Current temporary Store reference doesn't reflect this layout; a new one is needed.
- **Tarot Deck** — collection progress grouped by source deck; collected and not-yet-collected
  cards (e.g. a deck shown at 1/78). See [tarot.md](tarot.md).
- **Spells** — all discovered spells; doubles as the live spell inventory. Spells are shown as
  scrolls, with binding varying by category (e.g. vines for Nature) plus an icon. See
  [spells.md](spells.md).
- **Profile** — current mission with a collect-reward button; today's customers, earnings and
  spending. See [missions.md](missions.md).
- **Knowledge, Bestiary** — later sections. Not designed in this commission, but the style has to
  extend to them.

### Potion Grimoire

A separate book for potion recipes. Reuses the Grimoire's pages, layouts and spine states; needs
its own inside covers. Recipes show ingredients, quantities and output. See [potions.md](potions.md).

### Ledger

The end-of-day report as a multi-page book, smaller than the Grimoire, one spread per day. Opens on
the latest day; the player can page back to any previous day. Same layout every day, only the data
changes. Has its own inside covers and two spine states: close to the start, and centered.

- **Left page — summary:** total customers, previous balance, total revenue, total spending,
  current balance.
- **Right page — detail:** icons of the items sold that day (for inventory), plus sections for
  tarot, potions and other content types.

---

## Parchment

Same family as the books. Used in three places:

- **The intro (The Contract)** — the opening deal with the Traveler, floating in front of the player
  before the shop appears. Name entry field, Next; a choice of sigils (premade set until
  name-to-sigil generation is built, plus a default X); signed with the sigil in blood; the
  parchment then burns away. See The Contract in [game-overview.md](game-overview.md).
- **Store checkout** — the stacked cart parchment on the Grimoire's Store page. Signed with the
  player's sigil on purchase, it burns away, leaving a fresh, empty sheet for the next order (see
  Grimoire above).
- **Customer buying** — payment at the till: a parchment appears, the amount is added, the customer
  signs, and it burns away. Customers sign in their own way: witches with a sigil, people with their
  name or an X when they pay without Soul Shards, forest creatures with an X or a splatter of blood
  or goo.

The player's sigil is their signature from then on, wherever they sign.

---

## Deliverables Summary

| Item | Quantity |
|---|---|
| Grimoire inside covers (front, back) | 2 |
| Potion Grimoire inside covers (front, back) | 2 |
| Ledger inside covers (front, back) | 2 |
| First page, last page (Grimoire family) | 2 |
| First page, last page (Ledger) | 2 |
| Spine states — near start, centered, near end (Grimoire family) | 3 |
| Spine states — near start, centered (Ledger) | 2 |
| Inside-page variants (Grimoire family) | 4 |
| Inside-page variants (Ledger) | 2 |
| Wear overlays (stains, blood, potion, burnt edges, torn edges) | 8–10 |
| Section layouts — Store, Tarot Deck, Spells, Profile, Potion Grimoire | 5 |
| Ledger spread layout | 1 |
| Parchment sheets — Contract, Store checkout (stack + fresh sheet), Customer buying | TBC |
| Section UI elements as needed (e.g. tabs/bookmarks, slots, frames, search field, filters, locked overlay) — temp buttons and icons may be reused | TBC |

---

## Terms

- Commercial use in Hexchange, its demo, trailers, store page and marketing; right to modify.
- Source files: layered PSDs with every element on its own, clearly named layer, easy to edit on our
  end.
- AI use as stated in Shared Requirements, confirmed in writing.
- Budget and timeline: not set; open to the artist's quote and availability.
- Paid test piece: one Grimoire spread — the Store page, with a checkout parchment sheet and a couple
  of wear overlays.
- Milestones and revision rounds: TBD.

---

## Open Questions

- **Open Question:** Milestones and revision rounds.
