# 30-Minute Demo

A free Steam demo whose job is threefold: earn wishlists, tell us what to actually spend
development effort on, and — once the full game ships — convert into purchases. "30-minute" is a
rough estimate of how much content is actually in the build, not a timer — see Content Walls, Not
a Time Limit below. The point is to tease and leave the player wanting more, not to cut them off.

---

## Purpose

Three goals, in order of what the demo has to do first:

1. **Wishlists** — the immediate, on-Steam ask. Everything about the demo's content walls (the
   bouncer, the locked crate tiers, the locked cauldron, the feedback prompt) should point at this
   directly, not just imply it.
2. **Where to spend effort** — read player reaction to the core loop early, before Foraging/Tarot/
   Potions are all fully built out. Not just "did they like it" but "what did they respond to most,"
   since that's what should actually steer near-term priorities. See Feedback below for how the
   in-game prompt is shaped around this, not just general sentiment.
3. **Future purchases** — the payoff comes later, at full release; the demo's job is to earn the
   wishlist now that becomes a purchase then.

The demo is deliberately narrower than the "Need" tier in [scope.md](scope.md) — it doesn't have to
prove the whole game, just enough of it to tell whether the shop loop and the book-opening hook
land, and to give a wishlisting player a reason to come back.

Being on Steam specifically also shapes what the content walls and feedback mechanisms can be — see
Content Walls and Feedback below.

---

## Content Walls, Not a Time Limit

No timer, no forced end screen. The player can keep running the shop — buying crates, opening
books, foraging, shelving, giving tarot readings — for as long as they want. What limits the demo is
content, fenced off in three different ways depending on how the player runs into it:

1. **Location-triggered** — the pub. The player can walk the road to it at any time; the door
   doesn't open, and the bouncer stops them with a real conversation (see The Pub & Bouncer below).
   This doesn't end anything — the player just leaves and keeps playing the shop like before.
2. **Systemic, inside the shop loop itself** — locked crate tiers. Ordering crates above the
   demo's scope shows them in the catalog rather than hiding them, but purchasing is blocked (see
   Locked Crate Tiers below). This is the wall a player runs into naturally, during normal play,
   without needing to go looking for it the way the pub requires a deliberate walk.
3. **In the shop, from minute one** — the cauldron. The broken cauldron is in the shop from the
   start (see Starting State in [game-overview.md](game-overview.md)); in the demo the working
   cauldron is visible in the furniture catalog but locked, same treatment as locked crate tiers.
   Inspecting the broken one gives a short line about brewing in the full game. See Potions in the
   Demo below.

All three walls exist at the same time, encountered independently and in whatever order the player
finds them. None is "the ending" — the demo doesn't have one. It just gets narrower the further
a player pushes, until everything left to reach is on the other side of a wishlist.

---

## The Opening

No text crawl before play. The game opens with the contract — the floating parchment where the
player enters their name and signs with their sigil (see The Contract in [game-overview.md](game-overview.md)).
Once it's signed, the parchment burns away and the shop **builds itself** in the forest — walls, shelves, till, the
summoning circle and the broken cauldron assembling magically in place. When it's finished, two
tarot cards float out, twirling around each other: **the Six of Wands** (victory, public recognition
— opening day) and **the Devil** (the deal that paid for it). Triumph and its price. The player takes
them, and play begins.

The Six of Wands is **the sister's card** — from her Tarot de Marseille deck, the answer to the
one-card reading she did about the player before she left (see The Sister's Deck in
[tarot.md](tarot.md)). The demo never says so; it just looks different from the cards in the books.
The Grimoire shows her deck at 1/78.

The Devil is the **lost Visconti-Sforza Devil** (see The Lost Cards in [tarot.md](tarot.md)) — a
gilded Renaissance card beside the sister's plain woodcut one. Unexplained: a wink for players who
notice and look it up, and the most shareable detail in the demo. Its art must be commissioned before the demo ships.
In the full game, any Devil card can later be burned to summon the devil (see Burning the Devil in
tarot.md) — the demo only plants the card.

- The player already knows a deal with the devil was made for the shop — not why, or what the price
  was. The pairing doesn't reveal anything; it puts those questions into the cards from minute one.
- The Devil also needs to be owned early so self-reading story questions can draw it (see
  Self-Readings in [tarot.md](tarot.md)).
- The Grimoire's Tarot page shows those two cards from minute one — a quiet invitation to collect
  the rest, and it means the page is never empty.
- Not a demo-only exception: this is the real game's opening too (see Starting State in
  [game-overview.md](game-overview.md)). Giving the cards in the intro rather than guaranteeing them
  in the first book keeps the first book opening genuinely random — the book-opening hook stays honest.
- A natural trailer shot.

---

## A Typical Session

Roughly what an average player does in ~30 minutes, guided by a chain of prompts. Books are the main
hook; tarot is one of the things books feed, not the center.

1. **The intro** — the contract and sigil, then the shop builds itself, the Six of Wands and the Devil (see The Opening above).
2. **Prompt: purchase your first crate and fill a shelf.**
3. **Prompt: pick some mushrooms/flowers and fill a shelf.** Foraging, and foraged goods as stock.
4. **Prompt: open the shop and serve your first customer.**
5. **Prompt: open books** — the main hook. Cards, spreads and spells go into the collection.
6. **Prompt: cast a spell.**
7. **Prompt: purchase the tarot table.** The catalog shows it unlocks at **10 tarot cards**, so the
   requirement is visible before it's met. The store offers both **Tarot for Beginners** books and
   **Basic Spell Books** (see Crate Specialization below), so the player can choose to work toward the
   table. By the time they get there, they've served plenty of regular customers.
8. **Prompt: do a reading** — the first reading customer (see Scripted Moment under Tarot in the Demo
   below).
9. **Prompt: head off to the village.**
10. **Prompt: speak to the bouncer** (see The Pub & Bouncer below).
11. **Free play** — shop, books, readings, foraging, decorating. Along the way the player runs into
    the locked crate tiers and the locked cauldron. See After the Prompts below.

### Prompts = the mission chain

These prompts map directly onto the inherited mission chain (see [missions.md](missions.md)) — a
single linear sequence, one goal at a time, already shown on the Grimoire's Profile page. Adding or
reordering prompts is data-only via the Mission Manager window; only new goal *categories* need code.

| Prompt | Goal category | Exists? |
|---|---|---|
| Purchase first crate | Restock | Yes |
| Fill a shelf (stock / foraged) | — | **New** — no "place on shelf" goal today |
| Pick mushrooms/flowers | — | **New** — "Forage" isn't in missions.md's planned list either |
| Serve first customer | Checkout | Yes |
| Open books | Open a book | Planned in missions.md |
| Cast a spell | Cast spells | Planned in missions.md |
| Purchase the tarot table | Furnish | Yes |
| Do a reading | Tarot reading | Planned in missions.md — now designable (untargeted "do N readings") |
| Head to the village | — | **New** — a "reach location" goal |
| Speak to the bouncer | — | **New** — a "talk to NPC" goal, could be fired from Ink |

**Prompts keep the inherited money reward** — each one pays Soul Shards on collection, to help the
player buy more stock. Rewards should be sized to fund the *next* step where it matters — e.g. the
"open books" reward covers a Tarot for Beginners crate, and the rewards leading up to the table cover
its price — so the guided part never stalls on money.

### Estimated Pacing

Rough per-step estimates, to be checked in playtesting:

| Step | Est. time |
|---|---|
| Contract + sigil | 1–2 min |
| Intro (shop builds itself, two cards) | ~1 min |
| First crate + fill a shelf (incl. delivery) | 2–3 min |
| Forage + fill a shelf (walk out and back) | 3–4 min |
| Open shop, first customer | 1–2 min |
| Open books | 2–3 min |
| Cast a spell | ~1 min |
| Reach 10 cards (starts at 2) + save up for the table | 5–10 min — the most variable step |
| First reading | 2–3 min |
| Walk to the village | ~2 min |
| Bouncer conversation | 2–3 min |
| **Guided total** | **~23–35 min** |

Then free play on top. So the guided chain alone roughly fills the 30 minutes, and free play
stretches it for players who want more. The 10-card step is the swing: it depends on how many cards
Tarot for Beginners drops and how fast money comes in, because books opened for cards aren't sold.
Main tuning levers: card drop rates, mission reward sizes, and walking distances to the forage
spots and the village.

### After the Prompts

- **The mission chain ends at the bouncer.** The tracker shows a closing line (something like "The
  rest of the story is in the full game") instead of a new goal. No more mission rewards.
- **No ramp-up.** Customers keep coming at the normal rate; nothing scales up. More customers with
  nothing new to spend on would only make the demo grindier and hit the content walls faster.
- **The game keeps running.** Shop, books, readings, foraging all keep working — the content walls
  already cap progress, so nothing needs switching off.
- **Collecting stays open.** Players who keep opening books to grow their deck, with no prompt
  telling them to, are the strongest signal the demo can give.
- **Furniture is the money sink.** A good range of pretty furniture gives free-play money somewhere
  to go and suits the cozy audience. Art cost scales with the range — Asset Store packs make a wide
  range cheap; fully custom means fewer, better pieces.
- **No save carry-over** to the full game — not possible at this point. Possible later idea only.

---

## Minimum Playable Slice

Proposed floor for "this is a demo, not a tech test." Everything here already exists as a Need-tier
item in scope.md or a task in [current-task.md](current-task.md) — the demo doesn't invent new
scope, it picks a cutoff line partway through what's already planned.

1. **Base shop loop** — buy crates, shelve, sell, rent. Already exists. See Customer Roster below
   for which customer types the demo actually spawns.
2. **Locked crate tiers** — the ordering screen (currently the PC, migrating to the Grimoire's Shop
   page per current-task.md's Ongoing Decision) shows crate tiers above the demo's scope in the
   catalog rather than hiding them, but purchasing is disabled — see Locked Crate Tiers below. This
   is the systemic half of Content Walls above, and it's new UI work: the existing ordering screen
   doesn't have a locked/disabled item state today. The unlocked tiers include four **book
   lines** (mainstream, Basic Spell Books, Tarot for Beginners, potion books) — see Crate
   Specialization below.
3. **Book Product** — purchasable, placeable, sellable sealed or openable. Current-task.md item 3.
4. **Book-opening logic** — opening a book grants a reward into the player's collection.
   Current-task.md item 4.
5. **Four reward types: Spells, Tarot cards, Tarot spreads, Potion recipes** — the Grimoire's
   Spells and Tarot Deck pages and the Potion Grimoire (current-task.md item 2) all have to actually show
   what was gained, or the book-opening hook has nothing to prove. Recipes are a deliberate tease —
   see Potions in the Demo below.
6. **Foraging** — forage spots in the world, the bag, respawn timers. Foraged herbs are sold on
   shelves like any other stock. Needed because two of the demo spells (Show Magical Scents, Rain)
   only make sense with it in the build.
7. **Weather system, for Rain** — a purchased Unity Asset Store weather package (see Nature spells
   in spells.md), not in the project as of this writing. Committed to, specifically to support the
   Rain spell (see Spell Selection below) — real cost and timeline risk, not a small add. Only
   needs a rain state wired up; Storm isn't picked, so the demo doesn't need the full weather
   roster. Also touches Foraging: per foraging.md's Weather & Time Sensitivity, which plants
   actually respond to rain (growth speed, appearance) isn't mapped out yet and needs a per-
   ingredient design pass — recommend a simplified, flat effect for the demo (e.g. a global
   growth/spawn boost while it's raining) instead of that full pass, unless the design work happens
   anyway. See Open Questions below.
8. **Furniture buying** — ordering/placing furniture from the Furniture & Display System (see
   [game-overview.md](game-overview.md)). A good range of pretty pieces, not just the functional
   minimum — it's the money sink once the prompts end (see After the Prompts above). The **reading
   table** (see 9 below) is bought through this same flow. The working cauldron appears in the
   catalog but is locked — see Potions in the Demo below.
9. **Tarot readings at the reading table** — see Tarot in the Demo below. A second service point,
   working like the cashier area: when the table's open sign is on, reading customers queue at it
   and wait for the player.
10. **The opening sequence** — the contract (name entry, sigil choice, blood signing), then the shop building
    itself, the Six of Wands and the Devil. See The Opening above.
11. **The pub exterior + bouncer** — see below. One of the demo's three content walls (see Content
    Walls above), not the demo's ending — the player can walk away from this conversation and keep
    running the shop exactly as before.

This means the demo can't be scheduled until current-task.md items 2–4 are done; Foraging exists
(not started as of this writing — no forageable code in the project yet); the weather asset is
purchased and at least a rain state is wired up; Spells' and Tarot's Grimoire pages are playable
end to end; and the reading table works (queueing, spreads, card meanings shown). Swapping Potions
out for tarot readings removes the longest dependency in the old plan — Potions needed Foraging,
Private Ingredient Storage, a cauldron and craftable recipes in sequence. Foraging and readings no
longer depend on each other and can be built in parallel. Worth treating this chain as the real
target date for "the demo is possible," separate from whenever it's actually shown to people.

**Deliberately out:** Potion brewing (the cauldron is a content wall — see Potions in the Demo),
Crafting Accidents, Storm (the weather asset is being integrated for Rain
regardless, but Storm doesn't add anything Rain doesn't already cover), Helpers, Goblins,
romance/friendship progression, anything else from the "Want" or "Polish" tiers in scope.md.

---

## Crate Specialization

Already planned for the full game (see Progression in [game-overview.md](game-overview.md)): crates can
be specialized — nature-themed, spell-themed, divination-themed — to skew the odds toward the kind of
content the player is chasing. Since a crate holds copies of one book (see Books in
game-overview.md), specialization shows up as themed **book lines**, each with its own reward odds.

- Every book line can drop the occasional tarot card, so every player sees tarot coming out of
  books even if they never chase it.
- **In the demo, the store offers four book lines:**
  - **Mainstream books** — mostly for selling; suit Villagers, the bulk of early customers.
  - **Basic Spell Books** — weighted toward spells.
  - **Tarot for Beginners** — much higher odds of tarot cards and spreads. Buying these is the player
    choosing to work toward the reading table.
  - **Potion books** — grant potion recipes (see Potions in the Demo below).
- All must be in unlocked tiers — Tarot for Beginners especially, or reaching the table's 10-card
  unlock in a session is down to luck. Higher tiers stay behind the locked-crate wall. Nothing else in
  the store is greyed out apart from the cauldron.

---

## Locked Crate Tiers

The systemic content wall from Content Walls above. Where the pub requires a deliberate walk down
a road, this is the wall a player runs into just by playing normally and eventually wanting to
spend more Soul Shards than the demo's scope covers.

- The ordering screen shows crate tiers beyond the demo's scope **in the catalog**, not hidden —
  visible name, price, and whatever preview art normally exists, same as any purchasable crate.
- Purchasing is disabled: greyed out, a locked icon, a "Full Game" tag — something that reads
  immediately as "this exists and you can't have it yet," not as a bug or a missing asset. Same
  treatment as the locked cauldron — a wall has to look intentional or it just looks broken.
- This is **new UI work**, not a reuse of anything that exists today — the ordering screen (PC now,
  migrating to the Grimoire's Shop page per current-task.md) has no locked/disabled item state at
  all currently.
- **Why crate tiers specifically, rather than locking individual spells/potions/cards:** book
  contents are randomized rewards gated by crate tier already (see the "crate-tier gating" note
  repeated across spells.md, potions.md, and tarot.md) — a player never sees a book's exact
  contents before opening it regardless. Locking the tier itself is the one lock point that
  actually matches how the real game already hides higher-tier content, rather than inventing a
  second, demo-only content-gating mechanism on top of the one that already exists.
- Doubles as a second wishlist touchpoint alongside the bouncer (see Purpose above) — a locked
  crate's tooltip is a natural, low-friction place for a "wishlist to unlock the rest" nudge,
  encountered during normal play rather than only at the one deliberate pub visit.

---

## Tarot in the Demo

Cards and spreads collect normally from opened books, same mechanism as Spells, tracked on the
Grimoire's Tarot Deck page (current-task.md item 2). The player starts with two cards — the Six of
Wands and the Devil from The Opening above.

**Several source decks in the demo.** Cards drop from a few different decks (see Source Decks in
[tarot.md](tarot.md)), and the Grimoire shows every deck and card not yet unlocked — so the player
sees how much there is to collect. Decks mix and match freely, so cards from any source go into the
same reading deck.

Readings follow [tarot.md](tarot.md): the game shows each card, its meaning, and its meaning in its
spread position — it never explains the reading. Payout comes from **spread fit** (picking a spread
that suits the customer's question) and **deck taste** (some customers care about a full, single-
source deck), never from which cards are drawn.

### The Reading Table

The Divination Table from [tarot.md](tarot.md) — "reading table" here for short.

- Bought from the furniture catalog. Comes with its **own open sign**.
- Works like the cashier area: with the sign on, reading customers come to the table and wait for
  the player. With it off, nobody queues there.
- **Unlocks at 10 tarot cards.** It's visible in the catalog from the start with its requirement
  shown (e.g. "Requires 10 tarot cards — 4/10"), so the player can see the goal before reaching it. Once unlocked, it **costs Soul Shards** — mission rewards should cover the price.

### Card Minimum

A three-card spread needs three cards, but a three-card deck draws the same three cards every time.
The 10-card table unlock is sized so the three-card spread already draws from enough cards to vary
(roughly three times the spread size). Larger spreads can still carry their own per-spread minimum
deck size **in data**, so the numbers can be tuned after playtesting. Tarot for Beginners' drop rates
(see Crate Specialization above) need to make 10 cards reachable in roughly the first 10–15 minutes.

### Spreads in the Demo

Three, each doing a different job:

- **One-card draw** — the simplest; quick readings.
- **Three-card past/present/future** — the workhorse, and what the card minimum above is sized for.
- **A reach spread** — larger, needs more cards than most players will have in 30 minutes, but
  genuinely usable by a lucky or thorough player. Proof there's more depth than the demo shows.

### Scripted Moment

One: **the first reading customer.** Their question is clear and one of the player's spreads
obviously fits it, so the spread-fit idea lands without a tutorial screen. Every reading customer
after that spawns normally. Built on the same Ink pipeline as the bouncer.

### Who Wants Readings

Villagers (casual — don't care about the deck) and Hedge Witches (discerning — want a full single-
source deck, tip more for one). In practice no player completes a full deck in the demo, so the
Hedge Witch's reaction is mainly a tease that collecting matters. See Customer Roster below.

---

## Potions in the Demo

Potion brewing is a **content wall**, not a feature, in the demo:

- The broken cauldron sits in the shop from the start (as in the full game). Inspecting it gives a
  short line pointing at brewing in the full game.
- The working cauldron is visible in the furniture catalog with the same locked treatment as locked
  crate tiers.
- **Potion books are sold and grant recipes**, shown in the Potion Grimoire — even
  though nothing can be brewed. This deliberately overrides the earlier "no recipe you can't brew"
  rule, for three reasons:
  - It shows the player what potions will look like, without adding more greyed-out store entries —
    the cauldron stays the only locked item in the store.
  - It lets players make small money mistakes: Soul Shards spent on potion books aren't spent on
    Tarot for Beginners. Learning to focus is part of the game.
  - Recipes are real content the full game will use, so nothing is built just for the demo.
- Brewing gets a mention in the bouncer's "what the full game will have" beat (see below).

Why: market research (October 2026, Gamalytic) showed potion-crafting games sell reliably but are
crowded, while tarot inside a full game is nearly unoccupied. Book opening, which comparables like
TCG Card Shop Simulator show is the strongest hook, stays the center either way. The feedback prompt
(see below) measures how much players want brewing, without building it first.

---

## Spell Selection

Four spells picked from spells.md.

| Spell | Category | Why it's in |
|---|---|---|
| Show magical scents | Nature | Reveals every forageable in the world at once with a particle effect (see spells.md — simplified from the earlier trail/target-selection idea). Big, immediate "wow" moment. First in Nature's discovery order in spells.md (Early stage) precisely because it's cheap and attention-grabbing — the demo and the full game agree on this one. |
| Rain | Nature | Primarily an ambience/coziness pick, not an active one — cast it, watch the shop's mood change. What keeps it from feeling like nothing happened: mushroom forage spots visibly sprouting while it rains (spells.md already says rain "can make some plants appear that otherwise wouldn't"), and Mushroom Folk showing up as a customer — spells.md already ties rain to raised Mushroom Folk spawn odds, so this reuses an existing documented connection rather than inventing one. Needs the weather asset committed to in the Minimum Playable Slice above — real added cost. Recommend the simplified flat-effect version noted above for the rest of Foraging's plants, rather than a full per-ingredient design pass (see Open Questions) — the visible mushroom growth and the Mushroom Folk arrival are what need to land, not a complete weather-response matrix. |
| Touch of luck I | Household | Better odds on book-opening rewards. The strongest pick of the group — it doesn't sit beside the core loop, it amplifies the exact mechanic the demo is built around. Needs a luck-multiplier hook into the book-opening RNG the demo is already building for current-task.md item 4, not a separate system. |
| A single Wall Material spell | Household | Canonically "one of the very first spells found." Visually the flashiest — the shop changes in front of the player. Needs a wall-material-swap system that nothing else in the demo requires. Include if there's room for a customization beat; cut first if the schedule is tight. |

**Cut, and why:**
- **Cleaning I** — its only demo job was cleaning up Crafting Accidents, which left with potion
  brewing (see Potions in the Demo above).
- **Storm** — the weather asset is being integrated for Rain regardless, but Storm itself wasn't
  requested and doesn't serve a demo purpose Rain doesn't already cover.
- **Grow** — dropped in favor of this round's picks. Still cheap (reuses Foraging's respawn timer)
  and a fine full-game pick; just not in the demo lineup now.
- **Cleaning II** — needs Cleaning I's mess system as a prerequisite and is itself Mid-Late/low-
  incremental. With Cleaning I also cut, Cleaning II adds
  nothing the demo needs.
- **Goblin Repellant** — blocked on Goblins, which isn't in the demo.
- **Invocation spells, Touch of luck II/III** — Mid-Late/Late stage, need Helper/station systems
  the demo doesn't have.
- **Physical/Healing category** — parked in spells.md, not scheduled to any stage.

---

## Customer Roster

Five customer types, picked from [creatures.md](creatures.md)'s Customer Species against the same
constraint as the spells above: genuinely available this early, and no unbuilt unlock condition
standing in the way.

| Customer | Group | Why it's in |
|---|---|---|
| Villagers | Non-Magical Humans | Super Common, available from the start, no unlock condition — base template customer spawning already covers this. Interests span common books, herbs/flowers/mushrooms, and tarot decks, so a single customer type exercises nearly everything the demo has to sell. Also the casual reading customer — doesn't care what deck the player reads with. |
| Hunters | Non-Magical Humans | Also Common, also available from the start with no unlock condition. Interested in all books, all potions, all artifacts, and protection/luck spells — the one customer type that would specifically want Touch of Luck, one of the picked spells. |
| Hedge Witch | Magical Humans | Common, "Early, no portal needed" per creatures.md. Interests line up almost exactly with what the demo is built to show: common spell scrolls, herbs, tarot decks, common potion books — Spells, Tarot and the potion tease at once. Also the discerning reading customer — wants a full, single-source deck; see Who Wants Readings above. |
| Ogre | Forest Creatures | Baseline spawn is plain default customer logic, same fallback used for the rest of Forest Creatures (creatures.md's "Minimum to Get Something Working" note) — no documented arrival shortcut like Vampire's weather-sensitivity. Same placeholder interest/rarity data as the rest of the group. Picked partly for what it *isn't* (no character/arc anywhere in the docs, so nothing gets spoiled using it early, unlike Vampire or Werewolf below), and for visual distinctiveness. The earlier Ogre Attraction rule (a potion raising Ogre spawns) was dropped along with potion brewing. |
| Mushroom Folk | Forest Creatures | Picked specifically to give Rain (see Spell Selection above) a visible payoff — spells.md already ties rain to raised Mushroom Folk spawn odds, so unlike Ogre this one *does* have a documented arrival hook to reuse, no fallback-to-default-spawn-logic needed. Same placeholder interest/rarity data as the rest of the Forest Creatures group, though — still needs its own small design pass, just not on the arrival side. No character/arc anywhere in the docs is tied to Mushroom Folk, so it carries none of Vampire's spoiler risk either. |

**Cut, and why:**
- **Witches & Wizards** ("a normal witch") — hard-blocked, not just deferred. Requires the Forest
  Portal active; the Portal itself is unbuilt and "Want" tier per scope.md, and even built, it
  needs a known ritual *and* a full moon to activate — not reachable from a fresh save in a single
  30-minute session regardless of how much gets built. Same category as Storm getting cut for
  not being requested despite the weather asset now being committed to.
- **Druids, Arcanists** — Druids are local/early in small numbers but scale up specifically once
  the Portal is active (same blocker as above for the "bigger numbers" version); Arcanists require
  the Portal outright.
- **Vampire** — reconsidered and dropped. It's the one Forest Creature with a documented, already-
  working arrival mechanism (weather-sensitivity), which made it tempting, but it's tied up in
  Clarisse's whole arc in the-village.md and the game's "characters don't exist until the player is
  ready" design principle (npc-dialogue-and-relationships.md's Type Unlock Conditions). Using it as
  a throwaway early demo customer cheapens a reveal meant to land later. Same reasoning rules out
  **Werewolf**, which carries Aldric's secret.
- **Any other Forest Creature** — same placeholder-data cost as Ogre and Mushroom Folk, no
  particular reason to pick one over another beyond what those two already earn their spots with
  (visual distinctiveness for Ogre, Rain's payoff for Mushroom Folk).
- **High Fae & Demons** — end-game content, summoned via Invoke Minor Demon spells, which are
  themselves Invocation-tier and already cut from the Spell Selection above.

---

## The Pub & Bouncer

The pub exists as a physical building on the map — the player can walk up to it, same as in the
full game's eventual design (see [the-village.md](the-village.md), [npc-dialogue-and-relationships.md](npc-dialogue-and-relationships.md)).
Trying the door doesn't open it. It triggers a bouncer NPC blocking the way, with a real
conversation instead of a locked-door message. This doesn't end the demo — walking away from the
conversation drops the player right back into the shop loop, same as before (see Content Walls
above). The pub is one of three walls, not a finish line.

### Why a conversation instead of just a "not in this build" popup

The bouncer is one of the demo's three content walls, and its richest pitch moment. Instead of the
game quietly telling the player they've hit a wall, the wall talks back — breaks the fourth wall,
is upfront about being a demo, and does the selling job a store page would otherwise have to do
alone.

### Implementation: minimal slice of the real Ink system

The full character pipeline in npc-dialogue-and-relationships.md is marked "not started, planned
for later phase" — the bouncer is the first real thing built against it, scoped down hard:

- A real character file (`bouncer.yaml` + `bouncer-demo-dialogs.ink`), using the documented
  `INCLUDE ../_shared/dialog-functions.ink` pattern and the real condition/action functions —
  not a bespoke one-off script.
- **No friendship/romance scores, no presence weighting, no pub/shop file split.** The bouncer
  isn't a Full Character with an arc — just `unlock_flag` / `has_flag` to avoid repeating the same
  line twice, and Ink's native shuffle-bag (`{~...|...}`) for "still not letting you in" flavor
  lines on repeat attempts.
- This is a real first test of the Ink pipeline working end to end (compile, `story.ResetState()`
  on re-entry, the `EXTERNAL` function contract) on a small, low-stakes character before the full
  pub cast is built on top of it.

### Conversation content

What the bouncer actually talks about, per the brief:

- **Fourth-wall acknowledgment** — the bouncer knows this is a demo build, says so plainly.
- **What the full game will have** — a teaser list: potion brewing (the locked cauldron — see
  Potions in the Demo above), full tarot decks and bigger spreads, the forest portal and its
  creatures, the pub cast and their arcs, the personal mystery underneath it all. Doesn't need to
  over-promise specifics that aren't locked yet.
- **Who's working on it** — credits. *Placeholder — needs actual names/roles before this ships.*
- **The wishlist ask, stated directly** — this is the demo's real goal (see Purpose above), so the
  bouncer should say it outright rather than gesture vaguely at "the full game": something like "go
  wishlist it if you want back in." In-fiction, this is the price of admission the bouncer's
  actually asking for. Ideally paired with a real button/prompt here, not just the line — see
  Feedback below for the mechanism.
- **How to give feedback** — points at the in-game prompt (below) and/or wherever fuller feedback
  is meant to land. *Placeholder — needs a real destination decided (Discord/forms both work
  alongside a Steam demo; see Feedback below).*
- **Calling the player cheap** — a comic beat for repeated attempts to talk/bribe/sneak past the
  bouncer instead of accepting the wall. Doesn't need to be mean — needling, in on the joke with
  the player, consistent with the game's actual tone (see [collaboration.md](collaboration.md) /
  the calm-not-hype voice the game itself doesn't need to share, but the bouncer's ribbing does
  need to land as funny, not sour).

---

## Feedback

Two distinct jobs here, not one — the wishlist ask (Purpose goal 1) and the "what to prioritize"
signal (Purpose goal 2) want different mechanisms.

### The wishlist ask

Three touchpoints, since there's no single ending to hang it on: the bouncer conversation (the
richer, narrative one), locked crate tooltips, and the locked cauldron (the ones a player runs into
during normal play, possibly before ever finding the pub). Steam demos conventionally do this by popping the
Steam overlay straight to the store page (a wishlist button available to the client, not a custom
in-house system) — the bouncer's line and the crate tooltip are both just in-fiction/UI hooks into
that same one mechanism. **Open question:** whether the Steamworks API can tell the game if the
current user has already wishlisted the app — if it can't (this isn't confirmed), the prompt should
just always offer the button rather than trying to be clever about only showing it to players who
haven't.

### The prioritization signal

- **The bouncer mentions feedback verbally** — part of the conversation content above, pointing at
  wherever fuller feedback is meant to land (Discord, a form — both sit fine alongside a Steam
  demo's own wishlist flow).
- **An in-game feedback prompt**, shaped around Purpose goal 2, not just general sentiment.
  Lightweight — no backend exists yet, so this shouldn't assume one. Better than a plain thumbs-up/
  down: a quick "which of these did you want more of" pick from the demo's own systems (book-
  opening, tarot readings, spell casting, foraging, the shop floor itself) — that's the signal that
  actually tells us where to spend effort next, which a generic rating doesn't. Plus a second pick:
  "which locked thing do you want most" (potion brewing, the pub and its people, the forest portal)
  — a cheap way to measure demand for potions without building them first.
  Triggered either when the player leaves the bouncer conversation or when they choose to end the
  session, with an optional link/QR out to wherever fuller feedback is wanted. Not a survey the
  player is forced through — skippable, low-friction, matches the game's own no-moralizing,
  no-forced-interaction stance elsewhere (see [the-village.md](the-village.md)).

---

## Open Questions

- Team credits — who actually gets listed, and how. No single end screen exists to put them on
  (see Content Walls above) — most likely the bouncer dialogue, possibly also a main-menu/options
  credits entry, but not decided.
- Feedback destination for the fuller-feedback channel — Discord / a form link — separate from the
  wishlist CTA, which is Steam's own overlay/store-page flow.
- Whether the Steamworks API exposes "has this user already wishlisted this app" to the game
  client — not confirmed. If it doesn't, the wishlist prompt should just always offer the button
  rather than trying to hide it from players who've already wishlisted.
- Exact visual/UI treatment for locked crate tiers (see Locked Crate Tiers above) — greyed price,
  lock icon, tag copy, and how the tooltip's wishlist nudge is worded, none of which is decided yet.
- Whether the Wall Material spell makes the cut — it's the one demo spell needing a new system
  (wall-swap) purely for this build; keep if there's schedule room for a customization beat,
  cut first if not.
- Tarot card set size/composition for the demo — how many cards realistically enter circulation in
  a 30-minute session, and drop rates for Basic Spell Books vs. Tarot for Beginners that make the 10-card
  minimum reachable in roughly 10–15 minutes.
- Per-spread minimum deck sizes for larger spreads — ~3× spread size is the starting proposal, to be
  tuned. (The table itself unlocks at 10 cards — decided.)
- New mission goal categories needed for the prompt chain (fill a shelf, forage, reach location,
  talk to NPC) — see A Typical Session. (Prompts keep the money reward — decided; amounts not set.)
- Which spread is the "reach" spread, and how many cards it needs.
- Which source decks appear in the demo (Rider-Waite plus which others), and whether any deck is
  completable in a long free-play session. Depends on which licensed/commissioned decks exist by
  then — see Source Decks in tarot.md.
- Whether a Lost Card (tarot.md) can drop in the demo at all, or stays a full-game discovery.
- Potion book price and recipe count — enough to tempt, not so many that they swamp the store.
- How a reading customer's question is shown (dialogue line, category icon, both) — shared with
  tarot.md's Open Questions.
- What the shop-building-itself opening actually looks like — animation scope, and whether it's
  skippable on repeat plays.
- Ogre's and Mushroom Folk's actual interests (what they buy) and spawn rate/chance — placeholder
  in creatures.md like the rest of Forest Creatures, needs a real (if small) design pass rather
  than reusing the generic group-wide placeholder data as-is. Mushroom Folk's rain-spawn-odds
  boost is the one piece already specified; everything else about it isn't.
- Rain's in-demo effect scope — a full per-ingredient weather-response design pass (foraging.md
  flags this as not mapped out at all) vs. the simplified flat growth/spawn boost recommended
  above. Needs a decision before Foraging's ingredient list is finalized.
- What "mushroom forage spots visibly sprouting while it rains" actually looks like — a small VFX/
  animation beat, not yet designed, on top of whatever the simplified Rain effect ends up being.
