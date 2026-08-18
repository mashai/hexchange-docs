# Tarot

Second system in the build order (see [scope.md](scope.md)) — the payoff for one of the two starting
short-term goals in Progression, alongside the cauldron (see [potions.md](potions.md)).

---

## Cards

- Collected from books, never sold individually — see Books in [game-overview.md](game-overview.md).
- Every card belongs to a **source deck** — real historical tarot deck editions (Rider-Waite, Marseille,
  Thoth, etc.), not invented in-universe ones. Art comes from sourcing/adapting existing decks rather
  than designing new ones from scratch. Double-check public-domain/rights status per deck before
  committing art — Rider-Waite-Smith (1909) is confirmed PD.
- Collecting a full matching-source set can take a while, so a functional deck can be assembled from
  mixed sources, but a deck built entirely from one source sells for more.

---

## The Divination Table

Collecting a full set (composition TBD — likely one of each archetype) unlocks the ability to purchase
the **Divination Table** (previously called the "Tarot Table" — standardizing on Divination Table going
forward).

Works like the PC or till — its own dedicated menu. There, the player can:

- Assemble a deck from owned cards, and do **readings** — for customers (earns money for the shop) or
  for themselves (effect TBD).

An invocation spell (see [spells.md](spells.md)) can summon a helper who performs customer readings
autonomously, same earning effect as the player doing it directly.

---

## Deck Lifecycle

- **Assembling** a deck removes the used cards from the loose collection.
- **Disassembling** returns them (reversible, while unsold).
- **Selling** removes the deck and permanently forfeits those specific cards — they can never be
  returned once sold.

---

## Deck Visuals & Pricing

Every deck shares the same box shape/mesh, with the cover texture and price determined by composition:

- A deck built entirely from one source deck resolves to that source's own price and box art (a
  collector's premium).
- A mixed-source deck resolves to a single generic "Custom Deck" price and texture.

Same shared-mesh-plus-swapped-texture mechanism as book cover variation — just deterministic here
instead of random.

---

## Display

Tarot Decks use a dedicated **Tarot Display Stand** — exact style TBD. See Furniture & Display System
in [game-overview.md](game-overview.md).

---

## Grimoire

The Tarot Deck page of the Grimoire tracks collection progress.

---

## Future Idea (Not Designed Now)

Trading individual tarot cards — with customers, either at the pub or in the shop. (Not with Forest
Spirits — that's a separate barter marketplace, see [creatures.md](creatures.md).)
