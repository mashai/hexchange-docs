# Current Tasks

## In Progress

### 1. Scene Blockout — *solo* 🔴 CURRENT
Getting the scene to a stable rough draft before any gameplay work begins. Not final art — just correct layout and working systems.

**Remaining:**
- [ ] **[URGENT] Resolve navmesh situation** — legacy baked navmesh from template, no NavMeshSurface found. Need to install AI Navigation package and set up NavMeshSurface to take over baking. Do this before any geometry changes.
- [ ] Adjust entrance to align with new exterior
- [ ] Raise interior floor to match entrance level
- [ ] Investigate why patio area is inaccessible
- [ ] Add dedicated space for the cauldron
- [ ] Add summoning circle area for deliveries
- [ ] Reposition the till
- [ ] Remove PC setup (keep for now, remove later)
- [ ] Verify navmesh still works after all changes

**Later (not blocking blockout):**
- [ ] Create textures/materials for walls, floors, roof

**Done:**
- [x] Stripped template back to bare bones
- [x] Rough environment placed
- [x] Adjusted store room bounds to fit new environment
- [x] General scene cleanup — floors added, layout tidied

---

### 2. Shelf Model — *solo*
Replacing the default CheckoutFrenzy shelf with one that fits the game's aesthetic. Blocked until scene blockout is stable.

### 3. Book Product — *solo/help TBD*
Creating a book as a product in the game — model, basic data definition. Blocked until scene blockout is stable.

### 4. Delivery Box — *solo/help TBD*
Creating the box that arrives when a book order is placed. Flagged as complex. Blocked until scene blockout is stable.

> **Design note (not in scope yet, but important):** When ordering e.g. "Basic Spell Book Level 1", the delivery should be a box *full* of that book type — same stats, but with different visual appearance variants. This is so shelves can be stocked with individual books. Keep this in mind when designing the box and book systems.

---

## Main Focus — Core Book Flow *(needs Claude's help)*
Getting the end-to-end "stock the shop with books" loop working:

1. Player orders a box of books
2. Box appears in the summoning circle
3. Player opens the box
4. Player picks up a book, opens it, collects contents (spells/tarot/knowledge/recipes)
5. Book becomes an available product on the shelf
6. Customers can purchase it

---

## Up Next (Not Current)

### Payment System Overhaul — *major, needs Claude's help*
Replace the CheckoutFrenzy dollar/coin system with Soul Shards. Flagged as a large task — not started yet.

---

## Done
- Reviewed base template (CheckoutFrenzy) structure
- Reviewed and configured MCP Unity
- Contributed README improvement to MCP Unity upstream repo
- Set up docs folder and CLAUDE.md
