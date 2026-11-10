# Missions

Inherited from the CheckoutFrenzy template, unmodified so far. A single linear chain of goals the
player works through one at a time — not a quest board, not parallel objectives. Referenced here
because the Grimoire's Profile page displays the current mission (see
[GrimoireMissionWidget](../Assets/Hexchange/Scripts/UI/Grimoire/GrimoireMissionWidget.cs)), which is
being rebuilt on top of this system rather than replacing it.

---

## How a Mission Is Defined

A `Mission` ([Mission.cs](../Assets/CheckoutFrenzy/Scripts/Core/Data/Mission.cs)) is a
`ScriptableObject` asset with five fields:

| Field        | Meaning                                                              |
|--------------|-----------------------------------------------------------------------|
| `missionId`  | Position in the sequence. Missions run in ascending order, one at a time. |
| `goalType`   | Which of the 6 fixed goal categories this mission is (see below).    |
| `targetId`   | The specific product/furniture/license ID this mission cares about (unused for Checkout/Revenue). |
| `goalAmount` | How much of `goalType` to accumulate before it's complete.           |
| `reward`     | Money paid out when the player collects the completed mission.       |

Every mission asset lives in `Assets/CheckoutFrenzy/Resources/Missions/`, named `Mission001`,
`Mission002`, etc. `MissionManager` loads all of them at startup
(`Resources.LoadAll<Mission>("Missions")`) into a dictionary keyed by `missionId` — that's the
entire mission database, no other config file involved.

## The 6 Goal Categories

Defined in [MissionGoal.cs](../Assets/CheckoutFrenzy/Scripts/Core/Enums/MissionGoal.cs) — this is a
fixed enum, not data:

- **Checkout** — complete N checkouts (any product). No target.
- **Revenue** — earn a specific amount of money (in cents). No target.
- **Sell** — sell N units of one specific product.
- **Restock** — purchase N units of one specific product via the PC's ordering.
- **Furnish** — purchase and place N pieces of one specific furniture item.
- **License** — purchase one specific product license (always `goalAmount = 1`).

## How Progress Gets Reported

There's no polling or auto-tracking — gameplay code calls `MissionManager.UpdateMission(goalType,
progressAmount, itemId)` directly at the moment something relevant happens:

- `CheckoutCounter.ScanItem()` — reports `Revenue` (price scanned) and `Sell` (the product) on every scan.
- `CheckoutCounter` (checkout completion) — reports `Checkout`.
- `PC` (placing a stock/furniture order) — reports `Restock` or `Furnish` per item ordered.
- `StoreManager` (buying a license) — reports `License`.

`UpdateMission()` checks the report against the *current* mission only — if the goal type doesn't
match, or if `itemId` doesn't match the mission's `targetId` (for Sell/Restock/Furnish/License), the
report is silently ignored. Progress clamps at `goalAmount` and flips `IsComplete`.

## Advancing the Chain

The player collects a completed mission's reward (via `MissionManager.AdvanceMission()`, wired to a
button + `M` key in the tracker UI). That pays out the reward and looks up the *next* mission by the
smallest `missionId` greater than the current one — so mission order is entirely driven by
`missionId`, not by array position or anything else. If a mission has `License` as its next goal
type, progress for it is checked immediately in case the player already owns that license.

Only one `MissionData` (the save-data half — `MissionID`, `Progress`, `IsComplete`) exists at a time,
in `DataManager.Data.CurrentMission`. There's no history of completed missions kept beyond that.

## Editing Missions: the Mission Manager Window

`Tools > Checkout Frenzy > Mission Manager` ([MissionManagerWindow.cs](../Assets/CheckoutFrenzy/Scripts/Editor/MissionManagerWindow.cs))
is a custom editor window, not the Inspector — it lists all mission assets in order, and per mission
lets you: change goal type, pick the target (product/furniture/license dropdown, shown only when
relevant), set goal amount and reward, reorder with ↑/↓ (swaps `missionId`s), delete, or renumber
everything at once. "Add New Mission" creates a new asset and auto-assigns the next `missionId`.

**Adding or removing individual missions is fully data-driven** — no code involved, just this window.
That fits the project's data-driven content principle for the *instances*.

## Adding or Removing a Goal Category

This is the part that isn't data-driven — `goalType` is a fixed C# enum, not something the window (or
players) can extend. Adding a genuinely new category (say, a future "Brew Potions" or "Cast Spells"
goal for Hexchange) means touching code in several places:

1. **`MissionGoal.cs`** — add the enum value.
2. **`MissionManager.UpdateMission()`** — add a branch if the new goal needs target-matching logic
   (like Sell/Restock/Furnish do); goals with no target (like Checkout/Revenue) need nothing extra
   here, they fall into the existing "any item counts" branch.
3. **Wherever the triggering gameplay happens** — add the `UpdateMission(MissionGoal.NewThing, ...)`
   call at the moment of the relevant action, same as `CheckoutCounter`/`PC`/`StoreManager` do now.
4. **UI** — `MissionTracker` (and now `GrimoireMissionWidget`, which duplicates its display logic —
   see [current-task.md](current-task.md)) each need a new `LocalizedString` field and a case in
   `GetFormattedGoalLocalized()` for the goal's label text.
5. **`MissionManagerWindow.ShowMissionDetails()`** — add a target-picker branch (mirroring
   `ShowProductDropdown()`/etc.) if the new goal needs one, so it's still editable from the window
   without hand-editing asset files.

Removing a category means reversing all of the above, plus making sure no existing `Mission` assets
still reference the removed `goalType` (they'd silently point at a renumbered/nonexistent enum value
otherwise).

So: new *missions* are cheap, new *categories* are a small but real code change touching 4-5 files.
Worth knowing before assuming a new kind of goal can be added the same way a new mission can.

## Planned Hexchange Goal Types (Not Built Yet)

Six goal categories are planned for later, once their underlying systems exist. None of them need
anything beyond what "Adding or Removing a Goal Category" above already describes — every one fits
the existing untargeted-counter / targeted-counter split (the same shape as Checkout vs. Sell today).
Listed here for scope, not as a build order.

- **Open a book** — untargeted ("open N books") or targeted ("open *this* book N times", `targetId` =
  book ID). Blocked on the Book Product and book-opening logic existing at all
  (current-task.md items 3-4).
- **Collect tarot cards** — untargeted ("collect N cards total") or targeted ("collect *this* card",
  `targetId` = tarot card ID). Blocked on the Tarot data structure and book-opening actually granting
  cards (current-task.md item 2, item 4).
- **Complete potions** — untargeted ("brew N potions total") or targeted ("brew *this* recipe N
  times", `targetId` = potion recipe ID). Blocked on the Potions system (cauldron, crafting —
  scope.md "Need", third in build order, itself blocked on Foraging).
- **Tarot reading** — now designable: untargeted ("do N readings") or targeted ("do a reading
  with *this* spread", `targetId` = spread ID). Readings are spec'd in [tarot.md](tarot.md); the demo's
  "do a reading" prompt uses the untargeted form (see [demo.md](demo.md)).
- **Find knowledge** — the least defined of the six. No Knowledge system exists yet at all — it's
  explicitly parked in current-task.md as "expected to be a hard one, revisit later."
- **Cast spells** — untargeted ("cast N spells, any") or targeted ("cast *this* spell N times",
  `targetId` = spell ID). Blocked on Spells having an actual casting mechanic — the Grimoire's Spells
  page is still a placeholder.

Each one, once its underlying system exists, follows the same checklist as any new category: enum
value, an `UpdateMission()` target-matching branch (targeted variants only), the trigger call at the
point of the action, a UI label + name lookup, and a `MissionManagerWindow` target-picker (targeted
variants only).
