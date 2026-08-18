# Mystery: The Crop Field

> **Not core content — a moddability showcase.** This is optional background flavor, not part
> of the required game loop (see [scope.md](scope.md) — it lives entirely inside the pub/village
> system, itself a "Want," not a "Need"). Nothing else depends on it.
>
> It ships as a built-in pub conversation arc, but its real job is to be a worked example: proof
> of the kind of self-contained story a modder can build entirely through the dialogue/relationship
> system with no engine changes (see [npc-dialogue-and-relationships.md](npc-dialogue-and-relationships.md)).
> The goal is for a modder examining it to see a complete, replicable pattern: an NPC-driven
> mystery gated by book knowledge, built entirely in Ink and Lua.

## What It Is

A village mystery that unfolds entirely through conversation — the player never goes to the fields.
Crops in one section of the field are failing in a strange pattern. The village suspects the
supernatural. The actual cause is mundane and rooted in a long-running dispute between two
villages.

The design intent is contrast: in a world where vampires are real and the witch shop is open
for business, the actual threat to the village is a bucket of salt and vinegar and a decades-old
grievance over a personal insult.

---

## The Setup

Crops in one section of the field are dying in a way nobody can explain. The pattern is irregular,
the timing is suspicious, and the village has arrived at the obvious conclusion: something unnatural
is responsible. People bring it to the player — partly because a witch might know, partly because
it's something to talk about.

The player receives all information secondhand, through whoever walks through the door and
whoever they talk to at the pub. There is no direct investigation.

---

## The Red Herrings

Four supernatural explanations, all wrong, all plausible enough to take hold in the village.

**1. The ring shape**
The dying crops form an irregular ring at the edge of the affected area. Old written accounts —
findable in the right books — describe this as a classic sign of a Hollow Fae feeding ground.
A fae presence consuming the land from the boundary inward.

What it actually is: the shape of the path the neighbours walked when they spread the concoction
around the boundary of the area. They went around the edge. That's why the edge died first.

**2. The crows**
Crows have been gathering at that section of the field in unusual numbers. In bestiary lore,
crows are drawn to places touched by death magic — they sense it before humans can. Crows
gathering in numbers is a traditional omen in this setting's folklore, which is why the village
treats it as significant.

What it actually is: the rendered fat in the concoction is going rancid in the soil, and to a
scavenger that smells like something worth investigating. The crows are not reacting to anything
supernatural — they're behaving as scavengers do around a food-adjacent smell.

**3. The smell**
At dusk, near the worst rows, there's a faint sulfurous, sour smell. The classic marker of
an infernal presence — sulfur has meant demons and hellwork in every tradition anyone can name.

What it actually is: the same concoction, doing two different things to the soil. The sourness
is the vinegar. The sulfurous edge comes from the patch of soil itself — wet, greasy, and
organically overloaded from the fat and the dying crops rotting into it, exactly the low-oxygen
conditions that let soil bacteria produce a faint hydrogen-sulfide smell. It only becomes
noticeable at dusk because the cooling air sinks and traps the smell close to the ground instead
of carrying it off. Nobody in the village is close enough to the ground at dusk for long enough
to recognise either component.

**4. The new moon timing**
It started right after the last new moon. Maren brings this up with considerable certainty —
there is a specific curse cycle that operates on new moon alignment, and she has done her
reading. Rook says this is probably coincidence and should be ruled out before anything else.
Maren's explanation prevails socially. Rook's is correct.

What it actually is: the neighbours waited for the new moon so they wouldn't be seen in the field
at night. The timing carries no meaning beyond that.

---

## The Truth

The neighbouring village spread a homemade concoction — salt, vinegar, rendered fat — across
the crops at night. They made it themselves. They carried it in buckets. They walked the
boundary of the area and spread it as they went, then left before dawn.

Every supernatural clue maps directly onto the mundane cause. The ring is where they walked.
The smell is the vinegar and the decaying soil the fat created. The crows are drawn to that same fat,
not driven off by it. The timing is them waiting for darkness.

### Why They Did It

They believe someone from this village has been stealing their chickens and eating them before
anyone can be accused. The chicken losses are real — they're just not caused by a person.

The chickens are being taken by a fox. The eggs by fairies. Neither village knows this.
This is background truth only and is never revealed in-game. The chicken mystery remains
open at the end of the arc. The fox and the fairies carry on undisturbed.

### The Deeper Grudge

The chicken suspicion sits on top of a much older wound. The two villages have had a bad
relationship for decades. The original cause is disputed, and multiple versions circulate:

- The neighbouring village says someone from this village seduced their grandmother away
  from her fiancé, stealing the marriage.
- This village says the grandmother broke off the engagement herself, and did so because
  the fiancé made a comment about her bosom.
- Other versions exist. None are fully reliable.

---

## How It Unfolds

All through conversation. The player is never present for any of it directly.

### Act 1 — The Reports Come In

Wren brings it to the player first, enthusiastic and fully committed to the fae theory, despite
being wrong about it.

Emery gives a slightly different account — the ring, the crows, possibly the smell, in a different
order, with different emphasis. The accounts don't quite match, and something in his delivery
suggests reservations he hasn't voiced yet.

Aldric mentions it in passing, unimpressed — he has heard about this sort of thing before and
isn't worried.

### Act 2 — The Red Herrings Take Hold

NPCs return with updates. The pattern deepens. The new moon alignment surfaces (Maren, confidently).
Rook checks it out at someone's request or out of mild professional interest, comes back with
"probably nothing" and a suggestion to look for mundane causes first. The village favors Maren's
confident explanation over Rook's skepticism.

The player may be drawn in more directly here: asked to check the bestiary for information on
Hollow Fae or death magic, or to sell a protective item to someone who's now worried about
their own crops. This lends the supernatural explanation false credibility without the player
necessarily meaning to endorse it.

### Act 3 — The Trap

Emery, who has been quietly unconvinced for a while, floats a stakeout idea. If whatever is
doing this is coming to the field at night, catch it. He recruits help, including Wren, whose
involvement complicates the stakeout considerably.

Emery reports back across several conversations, and the account becomes progressively harder
to follow — something has clearly gone wrong, non-linearly, with Wren involved throughout.

### Act 4 — The Reveal

Emery comes back barely holding himself together. The stakeout caught someone. Several someones.
From the neighbouring village. With a bucket.

Wren is mortified — she was fully committed to the fae theory, and she was present when the
neighbours were caught.

Later, Aldric comes into the shop and says only, "I knew," then leaves without elaborating.

---

## NPC Investment Levels

| Character | Investment | Accuracy | Notes |
|---|---|---|---|
| Aldric | Low | Highest | Never thought it was magic. Unimpressed throughout. |
| Emery | Medium | Good | Quietly skeptical early. Drives the stakeout. Delivers the reveal. |
| Wren | High | Very wrong | Full commitment to the fae theory. Genuinely embarrassed at the end. |
| Maren | Political | Confidently wrong | Uses the mystery for social standing. Least interested in the truth. |
| Rook | Brief | Correct | Mildly annoyed at being ignored. Says the right thing, gets dismissed. |

---

## What the Player Knows vs. What Gets Revealed

The player never sees the field. They receive information second- and third-hand, from people
with different investment levels and different levels of attention to detail. The accounts
don't fully align. A player paying close attention will notice the discrepancies before
the reveal — the descriptions of the ring, the smell, the timing, never quite add up to the
same picture twice.

The player can ask questions, sell protective items, reference the bestiary. None of this
changes the outcome. The trap happens, the neighbours are caught, the reveal lands.

What is never revealed in-game: the fox, the fairies, and the full cause of the original feud.
The background truth exists so the world feels like it has more going on than the player
can see. The chicken mystery remains open at the end of the arc, with no confirmation given
in dialogue.

---

## The Resolution

The neighbours are caught with the bucket and are embarrassed; no further consequence is scripted.

There is no apology, confrontation scene, or resolution ceremony. The feud loses momentum rather
than resolving — it is not designed to conclude, only to de-escalate. Damaged crops remain
damaged; unaffected crops are unaffected. No further story beat follows.

Wren recovers from the embarrassment over time, eventually finding humor in it. Maren does not
reference the lunar curse theory again. Rook, if still present in the village, does not comment
on having been correct.

---

## Pacing & Knowledge Gates

*First pass — subject to change.*

The mystery gates itself to the player's book knowledge. Each red herring only surfaces once
the player has read something that makes it plausible. The design intent: the player's own
research is what makes the supernatural explanation convincing. The more they've learned,
the more they fall for it — until the reveal deflates everything at once.

**Act 1 — No knowledge required**
Wren brings the basics. Emery gives a slightly different account. Aldric shrugs.
The ring shape is visible in their descriptions but nobody has a framework for it yet.
The mystery remains open, with no explanation yet available to the player.

**Red Herring 1 — Hollow Fae feeding ground**
Unlocks after the player reads a fae or nature lore book.
Emery draws the connection tentatively, treating it as newly plausible knowledge — sourced
either from his own reading or from word of the player's reading circulating in the village.

**Red Herring 2 — Crow behaviour**
Unlocks after a book on crow omens or death magic.
Wren brings this one. She's been watching the field and the crows have been gathering there —
and now she knows what that means. She arrives fully convinced. The bestiary entry the
player unlocked is exactly what she's describing.

**Red Herring 3 — The smell**
Unlocks after a book on infernal or demonic signatures.
Someone raises the smell near the worst rows at dusk. The player's reading on infernal
markers lends it credibility — the description fits closely enough that it's hard to dismiss.
The player's knowledge is what makes the room take it seriously.

**Red Herring 4 — Lunar timing**
Unlocks after a book on curse cycles or lunar magic.
Maren arrives with certainty. The new moon alignment maps onto a specific curse cycle,
and she has her facts in order. The player's knowledge confirms it socially — they've read
the same framework she's referencing. Rook says it's probably coincidence and should be
ruled out first. Maren's account prevails socially; Rook's is correct.

**Act 3 onward — No knowledge gate**
The stakeout, the trap, and the reveal play out through conversation and time. No further
knowledge gates apply — everything the player has learned up to this point turns out to be
incorrect, and the reveal requires no additional setup.
