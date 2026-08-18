# NPC Dialogue and Relationships

A system for conversational interactions with named characters, centered around a pub the player can visit. Fully moddable — players can write their own characters, dialogue, and story arcs.

---

## Overview

The player can visit a pub where recurring NPCs hang out. Talking to them reveals lore, unlocks story beats, and builds relationships over time. This is the social layer of the game, separate from the shop floor.

Characters can also appear as customers in the shop, and may be seen walking the path through the woods towards the pub or village. The player cannot enter the village.

Knowledge gained from reading books in the shop feeds directly into conversation options — connecting the two systems.

---

## Character Tiers

There are two tiers of character:

### Full Characters
Named, recurring individuals with a folder of files defining their personality, dialogue, and arc. They can appear in the pub, the shop, or both.

### Ambient Customers
Minimal data. They show up in the shop, contribute to the bestiary, and have no pub presence or arc.

---

## File Structure

Each full character lives in their own folder:

```
characters/
  clarisse/
    clarisse.yaml
    clarisse-pub-dialogs.ink
    clarisse-shop-dialogs.ink     # also covers path encounters
    clarisse-presence.lua
```

The engine scans the character folder automatically. Files are matched by naming convention — no manual registration needed. Missing files mean that context has no dialogue. Ambient customers only need a YAML.

---

## Character Data File (YAML)

```yaml
id: clarisse
name: Clarisse
type: human                    # human / vampire / fae / werewolf / witch / sorcerer / etc.
prefab: npc_female_01
description: A regular at the pub. Always has her nose in a book.

pub_frequency: 0.7             # 0 = never, 1 = always (when space allows)

# Optional visual variant slots
variants:
  glasses: true
  hair_colour: auburn

# Optional — overrides global friendship tier thresholds for this character
friendship_tiers:
  acquaintance: 20
  friend: 40
  close_friend: 50

open_to_romance: false         # whether this character can be romanced at all
```

Ambient customer YAML:

```yaml
id: ambient_wolf_01
type: werewolf
prefab: npc_hooded_01
```

---

## Global Default Tiers

Defined once by the engine, used by all characters unless overridden:

```yaml
tiers:
  acquaintance: 25
  friend: 50
  close_friend: 75
  intimate: 90
```

---

## Relationships

Each full character has two independent scores:

- **Friendship** — how well you know and engage with this person
- **Romance** — your romantic connection

They influence each other. What you say about a character to someone else can affect both scores. Romance declining can pull friendship down too.

### Relationship Status Flags

Romance is not a single score state — it's a set of flags representing the nature of the relationship:

```
has_romance
is_exclusive
```

These are set through dialogue actions, not static traits. A character can start with `is_exclusive = true` from their init (it's just who they are), or it can be set later when a specific conversation happens. The player and character agreeing to exclusivity would fire `set_relationship_flag("clarisse", "is_exclusive", true)`.

The game is LGBT and poly friendly. No storyline forces a particular relationship type. Some characters will never be interested in romance; some only open up under specific conditions; some won't care if you pursue others; some will.

---

## Pub & Shop Presence

### How Spawning Works

Each time the engine populates the pub or shop, it:

1. Checks engine-level type unlock conditions — if not met, the character is not eligible, regardless of anything else
2. Calls the character's `presence.lua` function to get a weight (0–1)
3. Selects which eligible characters actually appear by balancing weights against each character's recent appearance frequency — characters who are underrepresented relative to their target frequency get higher selection priority

Available slots are limited. The engine fills them from the weighted pool.

### Type Unlock Conditions

Each creature type has engine-defined unlock conditions that modders cannot override. A vampire won't appear until the player meets the vampire type's requirements. Characters simply do not exist in the world until the player is ready for them — no hints, no mysterious figures.

Individual characters can have additional conditions on top of the type check via their presence function.

### Presence Function (Lua)

```lua
-- clarisse-presence.lua
function pub_presence()
    return 0.7
end

function shop_presence()
    if time_of_day() == "night" then return 0 end
    if friendship("clarisse") >= 50 then return 0.6 end
    return 0.2
end
```

Any engine-exposed condition can be checked here — time of day, weather, moon phase, story flags, relationship scores, etc.

### Meetups

Dialogue actions can temporarily boost presence. Ink function calls are positional only —
no named arguments — so this is three separate functions rather than one function with
optional/named args:

```
set_meetup_once("clarisse")        # shows up once then resets
set_meetup_days("ernst", 3)        # expires after 3 days
set_meetup_persistent("clarisse")  # stays until cancelled
cancel_meetup("clarisse")
```

---

## Dialogue System

Dialogue is written in **Ink**, a narrative scripting language designed to be readable by non-programmers. Ink handles conversation flow, branching, conditions, and actions.

Modders can test their `.ink` files in **Inky**, a standalone editor, without opening Unity —
or compile with the `inkjs` compiler directly, which is what these files are actually
verified against (see Ink Syntax Notes below).

### Line Pools

Ink has native syntax for a pool of interchangeable lines — no custom function needed:

```ink
{~Hi.|Hey there.|Hello.}
```

This is a **shuffle bag**: it plays through all the options in random order before
reshuffling for the next pass. It doesn't guarantee the line right before a reshuffle
can't be picked again right after — good enough for flavor lines, not a strict
no-immediate-repeat guarantee.

Two related forms:
- `{&Hi.|Hey there.|Hello.}` — cycles in a fixed sequence, wrapping around forever.
- `{!Hi.|Hey there.|Hello.}` — plays each once, in order, then produces nothing further.

### One-Time vs Repeatable Options

```ink
* {not seen("clarisse_first_meet")} [Is this seat taken?]   // one-time
* [Good to see you again.]                                   // always available
```

### Character Init

Each character has an optional init block that runs **once per playthrough** on first encounter. Use it to set starting flags, relationship status, or personality-driven state:

```ink
=== ernst_init ===
~ set_relationship_flag("ernst", "is_exclusive", false)
~ unlock_flag("ernst_met")
-> END
```

Not every character needs one — Clarisse's, for example, is empty (`-> END` only), since
none of her state needs a one-time setup step.

### Arc Completion

When a character's arc is complete, set a flag. Other characters' Ink files can check it:

```ink
~ unlock_flag("clarisse_arc_complete")
```

---

## Condition Functions

Readable functions usable inside Ink files to gate dialogue options. `friendship("clarisse")
>= close_friend` reads naturally but isn't valid Ink — tier names aren't accessible inside
`.ink` files, so compare against the raw number instead (63, in this example):

```
has_knowledge("how_to_attract_vampires")
friendship("clarisse") >= 63
romance("ernst") < 10
talked_to("ernst", 5)
completed_arc("clarisse")                        // shorthand for has_flag("clarisse_arc_complete")
has_flag("ernst_arc_unlocked")
has_relationship_flag("clarisse", "is_exclusive")
story_level() >= 3
seen("clarisse_first_meet")
has_item("vampire_lure")
bestiary_has_info("vampire", "weaknesses")
has_variant("clarisse", "red_hair")
time_of_day() == "night"
is_full_moon()
```

`seen(id)` isn't an Ink built-in, despite reading like one — Ink's own way to check a visit
count is to reference the knot/stitch name directly (`{ not clarisse_first_meet: ... }`).
It's listed here as a custom binding instead, purely so every file can keep writing
`seen("knot_name")` consistently. See Ink Syntax Notes below.

## Action Functions

Functions that fire when a dialogue option is chosen. Can target any character, not just the one being spoken to:

```
take_item("vampire_lure")
gain_friendship("clarisse", 15)
lose_friendship("clarisse", 10)
gain_romance("clarisse", 5)
lose_romance("clarisse", 20)
set_relationship_flag("clarisse", "is_exclusive", true)
unlock_flag("ernst_arc_started")
lock_flag("ernst_arc_started")
give_knowledge("how_to_attract_vampires")
set_variant("clarisse", "hair_colour", "red")
set_meetup_once("clarisse")
cancel_meetup("clarisse")
```

`unlock_flag` and `lock_flag` are the set-true / set-false pair — Ink can't give a function
optional arguments, so a flag you need to clear later needs its own function rather than a
second argument on `unlock_flag`.

---

## Ink Syntax Notes

The vocabulary above is the readable, documentation-friendly shorthand. The actual `.ink`
files have a few hard constraints that shorthand can hide:

- **Function calls are positional only.** No array literals, no named/keyword arguments.
  `lines([...], strategy: x)` and `set_meetup("id", expires_after_visit: true)` both look
  reasonable and are both invalid Ink — see Line Pools and Meetups above for the real forms.
- **Multi-line conditionals use `- else:`, not `} else {`:**
  ```ink
  { condition:
      content
  - else:
      other content
  }
  ```
- **Every custom function must be declared `EXTERNAL` before it's called**, or the file
  won't compile. Rather than repeating declarations in every character file, they live in
  one shared, included file:
  `Assets/Hexchange/Characters/_shared/dialog-functions.ink`. Every character's `.ink`
  files should start with:
  ```ink
  INCLUDE ../_shared/dialog-functions.ink
  ```
  Keep that file in sync with the Condition/Action Functions lists above — it's the
  authoritative contract the C#/Lua-side bindings need to implement, arity included.
- **Engine integration:** if a character's conversation can be re-entered more than once
  in a session (the normal case — every repeat visit to the pub or shop), the engine needs
  to call `story.ResetState()` before `story.ChoosePathString(knotName)` on each entry.
  Re-entering a knot that was left via a player choice, without resetting state first,
  throws a runtime error. This is expected — all of the actual game state (friendship,
  flags, knowledge, items) already lives outside Ink, in the external bindings, so
  resetting Ink's own internal state on each entry is the correct pattern, not a
  workaround.
- **A choice with visible text right before a `->` divert into a knot that opens with
  action calls (`~ gain_friendship(...)`, `~ give_knowledge(...)`, etc.) runs those action
  calls twice.** This is an `inkjs` bug, not a mistake in the content — reproduced in
  isolation and confirmed to depend specifically on the *source* choice printing text
  immediately before the divert (a divert straight after the choice bracket, or after a
  logic-only line like `~ unlock_flag(...)`, is unaffected). Avoid the pattern rather than
  working around the symptom: if a choice needs to say something distinct before handing
  off to shared content, set a flag with a logic-only line instead of printing text, and
  let the destination knot print the reaction conditionally on that flag. See
  `clarisse_shared_book` in `clarisse-pub-dialogs.ink` for a worked example (the
  "I've watched the YouTube—" branch).

These files are verified to compile and run cleanly against the `inkjs` compiler/runtime;
worth checking new character files the same way rather than assuming Inky-clean means
engine-clean.

---

## The Bestiary

The bestiary tracks **creature types**, not individual characters. It is filled by:

- Meeting a type for the first time (engine-controlled, cannot be triggered by modders)
- Receiving information about a type from an NPC via dialogue
- Reading a knowledge sheet from a book

Each bestiary entry represents what the player knows about that type of being, and grows as they learn more.

---

## Visual Variants

Characters can have toggleable or swappable visual slots defined in their YAML (hat, glasses, hair colour, etc.). Variants can be set at init, changed by dialogue actions, and checked as conditions:

```ink
{ has_variant("clarisse", "red_hair") :
    * [Love the new look.]
      ~ gain_friendship("clarisse", 5)
}
```

---

## Shop & Path Dialogue

Shop dialogue (including brief path encounters) lives in `{id}-shop-dialogs.ink`. It is:

- Short and lightweight — no deep branching
- Focused on brief exchanges and setting up pub visits
- Able to nudge pub presence via `set_meetup_once` / `set_meetup_days` / `set_meetup_persistent`

---

## Saving State

NPC and dialogue state (relationship scores, flags, init status, meetup state, bestiary) is saved separately from the main shop save file, in a parallel `HexchangeData` save using the existing `SaveSystem` infrastructure. This keeps our data cleanly separated from the CheckoutFrenzy base.

---

## Moddability

Players can add characters by dropping a folder into the characters directory. The engine picks it up automatically.

Modders have access to all condition and action functions listed above. A reference sheet will be provided. The only hard constraint is that engine-level type unlock conditions cannot be bypassed — a modder can make an encounter harder to trigger, never easier than the engine allows.

---

## Relationship Visibility

There is no UI showing relationship scores. The player reads the relationship through the warmth and content of dialogue — what options are available, how characters respond, what they volunteer. A debug UI will be available during development to inspect scores and flags directly.

---

## Open Questions

- What is the exact folder path for modded characters?
- Are story flags scoped globally or per-playthrough?
- How does the engine handle a modded character referencing a flag set by a base-game arc?
- Full list of engine-exposed functions for Lua presence scripts — what can modders query?

---

## Status

Not started. Planned for a later phase after the core shop loop is complete.
