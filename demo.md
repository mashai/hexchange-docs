# 30-Minute Demo

A free Steam demo whose job is threefold: earn wishlists, tell us what to actually spend
development effort on, and — once the full game ships — convert into purchases. "30-minute" is a
rough estimate of how much content is actually in the build, not a timer — see Content Walls, Not
a Time Limit below. The point is to tease and leave the player wanting more, not to cut them off.

---

## Purpose

Three goals, in order of what the demo has to do first:

1. **Wishlists** — the immediate, on-Steam ask. Everything about the demo's content walls (the
   bouncer, the locked crate tiers, the feedback prompt) should point at this directly, not just
   imply it.
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

No timer, no forced end screen. The player can keep running the shop — buying crates, foraging,
brewing, shelving — for as long as they want. What limits the demo is content, fenced off in two
different ways depending on how the player runs into it:

1. **Location-triggered** — the pub. The player can walk the road to it at any time; the door
   doesn't open, and the bouncer stops them with a real conversation (see The Pub & Bouncer below).
   This doesn't end anything — the player just leaves and keeps playing the shop like before.
2. **Systemic, inside the shop loop itself** — locked crate tiers. Ordering crates above the
   demo's scope shows them in the catalog rather than hiding them, but purchasing is blocked (see
   Locked Crate Tiers below). This is the wall a player runs into naturally, during normal play,
   without needing to go looking for it the way the pub requires a deliberate walk.

Both walls exist at the same time, encountered independently and in whatever order the player
finds them. Neither is "the ending" — the demo doesn't have one. It just gets narrower the further
a player pushes, until everything left to reach is on the other side of a wishlist.

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
   doesn't have a locked/disabled item state today.
3. **Book Product** — purchasable, placeable, sellable sealed or openable. Current-task.md item 3.
4. **Book-opening logic** — opening a book grants a reward into the player's collection.
   Current-task.md item 4.
5. **Two reward types: Spells + Tarot cards** — the Grimoire's Spells page and Tarot Deck page
   (current-task.md item 2) both have to actually show what was gained, or the book-opening hook
   has nothing to prove. **Tarot readings and the Divination Table are not in the demo** — see
   Tarot in the Demo below.
6. **Foraging** — forage spots in the world, the bag, respawn timers. Needed on its own merits
   (per scope.md it's what makes Spells and Potions mean anything), because two of the four demo
   spells below only make sense with it in the build, and because Potions (below) depends on it too.
7. **Weather system, for Rain** — a purchased Unity Asset Store weather package (see Nature spells
   in spells.md), not in the project as of this writing. Committed to, specifically to support the
   Rain spell (see Spell Selection below) — real cost and timeline risk, not a small add. Only
   needs a rain state wired up; Storm isn't picked, so the demo doesn't need the full weather
   roster. Also touches Foraging: per foraging.md's Weather & Time Sensitivity, which plants
   actually respond to rain (growth speed, appearance) isn't mapped out yet and needs a per-
   ingredient design pass — recommend a simplified, flat effect for the demo (e.g. a global
   growth/spawn boost while it's raining) instead of that full pass, unless the design work happens
   anyway. See Open Questions below.
8. **Furniture buying** — ordering/placing furniture, at least Bookcase/Shelf and one or two other
   types from the Furniture & Display System (see [game-overview.md](game-overview.md)). Doesn't
   need the full furniture roster, just enough that shelving/displaying feels real. The working
   cauldron purchase (see Potions below) is naturally part of this same beat — the shop starts with
   a broken, non-functional cauldron per [potions.md](potions.md).
9. **Potions — minimum crafting interaction as the committed baseline** — open the cauldron menu,
   pick a known recipe, craft instantly if ingredients are in stock (the "Minimum version" in
   potions.md). Requires **Private Ingredient Storage**, which potions.md flags as not built yet
   either — a customer-inaccessible ingredient area, enforced physically and logically.

   **Conditional stretch, tied to Cleaning I:** the plan is to also build timed crafting
   (potions.md's stretch goal — ingredients added at the right moment during the brew) and Crafting
   Accidents (the resulting mess, cleanable only by Cleaning I) specifically so that spell has
   something real to do in the demo. This is explicitly conditional, not committed like the rest of
   this list — if potion-crafting doesn't land solidly enough to support it, drop Crafting Accidents
   (and Cleaning I with it) rather than ship a rushed version. The baseline instant-craft
   interaction stands regardless of how this resolves.

   **Three recipes, all unlocked through normal book-opening RNG** (no demo-only exceptions —
   decided against a guaranteed/pre-known recipe, keeping the demo consistent with the real game's
   unlock rules), each doing a different job:
   - **Starter recipe** — cheap/common ingredients, the one most likely to actually get crafted in
     a given session.
   - **Foraged recipe** — needs an ingredient the player has to actually go pick, not just buy.
     This is the one that proves out the Foraging → Potions link scope.md cites as the reason
     Potions depends on Foraging existing first; without it the cauldron would demo just as well
     standalone.
   - **Reach recipe — Ogre's favorite.** From a pricier crate tier, rarer/costlier ingredients,
     likely out of reach in most 30-minute sessions but genuinely completable by a lucky or
     thorough player. Its book also grants Bestiary knowledge that Ogres want this potion — see
     Ogre Attraction below for the mechanic this powers. Fits Ogre's existing (if placeholder)
     "advanced potions" interest in creatures.md better than the other two recipes would, so this
     isn't an arbitrary pairing.

   **All three recipes must be fully craftable in the demo build** — no recipe should sit in the
   player's known list needing an ingredient that doesn't actually exist anywhere in the demo's
   world. A recipe that can't finish reads as a bug, not a tease, and risks burning real minutes
   of a short session on a dead end. If a "there's more than this" moment is wanted for Potions
   generally, it belongs in the bouncer's dialogue (see Tarot in the Demo above for the same
   pattern with Tarot reading) — not as a half-functional recipe.

   **Ogre Attraction — first real instance of species-attraction condition-matching.** Stocking the
   reach recipe's potion increases Ogre spawn/arrival rate specifically, not just Ogre purchase
   preference. Worth being precise about scope here: creatures.md flags per-species attraction
   conditions as "not designed at all," and a full condition-matching table (temperature, moon
   phase, potions on display, artifacts present, spells cast) is explicitly filed as a "Perfect
   World / Cool Idea, not committed." The demo isn't building that system — it's building the
   smallest possible instance of it: one hardcoded rule, one creature, one potion. Ogre's baseline
   spawn logic (see Customer Roster below) stays the plain default fallback; this is a single
   condition layered on top of it, not a general framework other species could plug into yet. The
   Bestiary entry the book grants is informational, not a gate — the effect runs whether or not the
   player has read it, same "learned, not told" pattern foraging.md already uses for ingredient
   night-potency.
10. **The pub exterior + bouncer** — see below. This is one of the demo's two content walls (see
    Content Walls above), not the demo's ending — the player can walk away from this conversation
    and keep running the shop exactly as before.

This means the demo can't be scheduled until current-task.md items 2–4 are done; Foraging exists
(not started as of this writing — no forageable code in the project yet); the weather asset is
purchased and at least a rain state is wired up; Spells' and Tarot's Grimoire pages are playable
end to end; and Potions has a working cauldron, Private Ingredient Storage, and at least a few real
recipes. That's a real chain, not a checklist — Potions depends on Foraging existing first (per
scope.md's build order), so those two can't be parallelized away. The timed-crafting/Crafting
Accidents stretch (and Cleaning I riding on it) sits outside this chain deliberately — cut it first
if it threatens the date, rather than treating it as a hard dependency like the rest of this list.
Worth treating the base chain as the real target date for "the demo is possible," separate from
whenever it's actually shown to people.

**Deliberately out:** Tarot readings/Divination Table, Storm (the weather asset is being integrated
for Rain regardless, but Storm wasn't requested and doesn't add anything Rain doesn't already
cover), Helpers, Goblins, romance/friendship progression, anything else from the "Want" or "Polish"
tiers in scope.md. Potion timed-crafting/Crafting Accidents are **conditional**, not deliberately
out — see Potions above.

---

## Locked Crate Tiers

The systemic content wall from Content Walls above. Where the pub requires a deliberate walk down
a road, this is the wall a player runs into just by playing normally and eventually wanting to
spend more Soul Shards than the demo's scope covers.

- The ordering screen shows crate tiers beyond the demo's scope **in the catalog**, not hidden —
  visible name, price, and whatever preview art normally exists, same as any purchasable crate.
- Purchasing is disabled: greyed out, a locked icon, a "Full Game" tag — something that reads
  immediately as "this exists and you can't have it yet," not as a bug or a missing asset. The
  distinction matters for the same reason it did for the potion recipes and the tarot reveal
  earlier — a wall has to look intentional or it just looks broken.
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

Cards collect normally from opened books, same mechanism as Spells, tracked on the Grimoire's Tarot
Deck page (current-task.md item 2). What's cut is everything downstream of a *full* set: the
Divination Table (readings, deck assembly) per [tarot.md](tarot.md) only unlocks once a complete
matching set is collected — which isn't realistic in a 30-minute session anyway. So "hinted but not
available" isn't an artificial demo restriction so much as the natural shape of the game's own
early-game pacing, just made explicit rather than left implicit.

The hint itself is dialogue, not a mechanic — a natural line for the bouncer's "what the full game
will have" beat (see below): readings, the Divination Table, full deck collecting and selling. No
locked/greyed-out Divination Table prop needs to exist in the demo build for this; the tease can
live entirely in conversation.

---

## Spell Selection

Five spells picked from spells.md. Four are committed; the fifth, Cleaning I, is conditional on the
Crafting Accidents stretch in Potions above actually landing.

| Spell | Category | Why it's in |
|---|---|---|
| Show magical scents | Nature | Reveals every forageable in the world at once with a particle effect (see spells.md — simplified from the earlier trail/target-selection idea). Big, immediate "wow" moment. First in Nature's discovery order in spells.md (Early stage) precisely because it's cheap and attention-grabbing — the demo and the full game agree on this one. |
| Rain | Nature | Primarily an ambience/coziness pick, not an active one — cast it, watch the shop's mood change. What keeps it from feeling like nothing happened: mushroom forage spots visibly sprouting while it rains (spells.md already says rain "can make some plants appear that otherwise wouldn't"), and Mushroom Folk showing up as a customer — spells.md already ties rain to raised Mushroom Folk spawn odds, so this reuses an existing documented connection rather than inventing one. Needs the weather asset committed to in the Minimum Playable Slice above — real added cost. Recommend the simplified flat-effect version noted above for the rest of Foraging's plants, rather than a full per-ingredient design pass (see Open Questions) — the visible mushroom growth and the Mushroom Folk arrival are what need to land, not a complete weather-response matrix. |
| Touch of luck I | Household | Better odds on book-opening rewards. The strongest pick of the group — it doesn't sit beside the core loop, it amplifies the exact mechanic the demo is built around. Needs a luck-multiplier hook into the book-opening RNG the demo is already building for current-task.md item 4, not a separate system. |
| A single Wall Material spell | Household | Canonically "one of the very first spells found." Visually the flashiest — the shop changes in front of the player. Needs a wall-material-swap system that nothing else in the demo requires. Include if there's room for a customization beat; cut first if the schedule is tight — worth reweighing now that Rain and the Cleaning/Crafting-Accidents stretch are also competing for build time. |
| Cleaning I — **conditional** | Household | Only functional if the timed-crafting/Crafting Accidents stretch (see Potions above) actually lands — it cleans the mess that mechanic produces. Drops from the demo alongside that stretch if it doesn't come together; nothing else in the demo gives it a job. |

**Cut, and why:**
- **Storm** — the weather asset is being integrated for Rain regardless, but Storm itself wasn't
  requested and doesn't serve a demo purpose Rain doesn't already cover.
- **Grow** — dropped in favor of this round's picks. Still cheap (reuses Foraging's respawn timer)
  and a fine full-game pick; just not in the demo lineup now.
- **Cleaning II** — needs Cleaning I's mess system as a prerequisite and is itself Mid-Late/low-
  incremental. Even if Cleaning I makes the cut via the conditional stretch, Cleaning II adds
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
| Villagers | Non-Magical Humans | Super Common, available from the start, no unlock condition — base template customer spawning already covers this. Interests span common books, common potions, herbs/flowers/mushrooms, and tarot decks, so a single customer type exercises nearly everything the demo has to sell. |
| Hunters | Non-Magical Humans | Also Common, also available from the start with no unlock condition. Interested in all books, all potions, all artifacts, and protection/luck spells — the one customer type that would specifically want Touch of Luck, one of the picked spells. |
| Hedge Witch | Magical Humans | Common, "Early, no portal needed" per creatures.md. Interests line up almost exactly with what the demo is built to show: common spell scrolls, herbs, common potion books/potions, tarot decks — Spells, Potions, and Tarot all at once. |
| Ogre | Forest Creatures | Baseline spawn is plain default customer logic, same fallback used for the rest of Forest Creatures (creatures.md's "Minimum to Get Something Working" note) — no documented arrival shortcut like Vampire's weather-sensitivity. On top of that baseline, one specific condition now exists: stocking the reach potion recipe raises Ogre spawn/arrival rate — see Ogre Attraction under Potions above. Same placeholder interest/rarity data otherwise as the rest of the group. Picked over the rest of the group partly for what it *isn't* (no character/arc anywhere in the docs, so nothing gets spoiled using it early, unlike Vampire or Werewolf below) and now also for the concrete potion tie-in. |
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
above). The pub is one of two walls, not a finish line.

### Why a conversation instead of just a "not in this build" popup

The bouncer is one of the demo's two content walls, and its richest pitch moment. Instead of the
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
- **What the full game will have** — a teaser list: Tarot readings and the Divination Table (the
  demo only lets the player collect cards, not read with them — see Tarot in the Demo above), the
  pub cast and their arcs, the personal mystery underneath it all. Doesn't need to over-promise
  specifics that aren't locked yet.
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

Two touchpoints, not one, since there's no single ending to hang it on: the bouncer conversation
(the richer, narrative one) and locked crate tooltips (the one a player runs into during normal
play, possibly before ever finding the pub). Steam demos conventionally do this by popping the
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
  opening, potion brewing, spell casting, tarot collecting, the shop floor itself) — that's the
  signal that actually tells us where to spend effort next, which a generic rating doesn't.
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
- Which specific three Potion Recipes fill the starter/foraged/reach roles above, and which
  foraged/purchased ingredients they need — not decided yet, and blocked on Foraging's ingredient
  list existing first. Every ingredient any of the three needs must actually exist and be
  obtainable in the demo build (see note above on why a dead-end recipe is worse than no recipe).
- Tarot card set size/composition for the demo — how many cards realistically enter circulation in
  a 30-minute session, and whether that's enough to make the Tarot Deck Grimoire page feel alive
  rather than empty.
- Ogre's and Mushroom Folk's actual interests (what they buy) and spawn rate/chance — placeholder
  in creatures.md like the rest of Forest Creatures, needs a real (if small) design pass rather
  than reusing the generic group-wide placeholder data as-is. Mushroom Folk's rain-spawn-odds
  boost is the one piece already specified; everything else about it isn't.
- Rain's in-demo effect scope — a full per-ingredient weather-response design pass (foraging.md
  flags this as not mapped out at all) vs. the simplified flat growth/spawn boost recommended
  above. Needs a decision before Foraging's ingredient list is finalized.
- What "mushroom forage spots visibly sprouting while it rains" actually looks like — a small VFX/
  animation beat, not yet designed, on top of whatever the simplified Rain effect ends up being.
- Ogre Attraction's actual numbers — how much stocking the reach potion boosts Ogre spawn odds by,
  whether the potion needs to be continuously in stock and unsold or just present once, and how
  quickly an Ogre shows up after it's shelved. None of this is decided; the mechanic's existence is
  agreed, its tuning isn't.
- Where the line is for "potion-crafting doesn't land solidly enough" to justify committing to
  timed crafting + Crafting Accidents for Cleaning I. No concrete bar set yet — currently a
  judgment call at build time, not a measurable gate.
