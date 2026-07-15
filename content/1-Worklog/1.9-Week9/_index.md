---
title: "Week 9 Worklog"
date: 2026-06-29
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

## General Information

| Content | Details |
| --- | --- |
| Time | 29/06/2026 - 05/07/2026 |
| Internship Week | Week 9 |
| Phase | SmartMenu - Menus, dishes, and allergen tagging |
| Role | Full-stack, responsible for backend; assisted with frontend |
| Main Focus | Versioned menus, menu item CRUD, allergen tagging |

## Week 9 Direction

This week is about the "core" of the product: the menu and dishes. The part I pondered most was **menu versioning** - when an owner updates the menu, the old one shouldn't vanish but be archived, and only one menu can be "published" for guests at a time. I also implemented allergen tagging for dishes, which is SmartMenu's killer feature over traditional paper menus.

## Week 9 Objectives

- `Menu` model with a draft -> published -> archived lifecycle.
- Auto-archive the currently published menu when a new one is published.
- `MenuItem` CRUD: name, price, category, description, status.
- Allergen tagging: list allergens, confidence (contains / may_contain), source (AI suggested / owner verified).

## Work Carried Out During the Week

### Day 1 - Monday, 29/06/2026

Designed the menu lifecycle.

- Charted the menu states: `draft` (editing) -> `published` (visible to guests) -> `archived` (old menus).
- Designed `Menu` model: name, imageUrl, status, restaurantId, version.
- Decision: A restaurant can have many menus but only one `published` at a time.

### Day 2 - Tuesday, 30/06/2026

Create menu + publish.

- Wrote `POST /menus/upload` to create a new draft menu.
- Wrote `POST /menus/:menuId/publish`: sets this menu to published, and simultaneously finds the previously published menu to archive it.
- Had to be careful here: if I publish A while B is published and forget to archive B, there will be two published menus. Rewrote it as a two-step operation within a single transaction/flow to prevent this.

```bash
curl -X POST http://localhost:3000/api/v1/menus/$MENU_ID/publish \
  -H "Authorization: Bearer $ACCESS_TOKEN"
```

### Day 3 - Wednesday, 01/07/2026

Menu + Item CRUD.

- Wrote `GET /menus` (list all versions), `PATCH /menus/:menuId`, `DELETE /menus/:menuId`.
- `MenuItem` model: nameVi, price, category, descVi, status (available / sold_out), menuId.
- Wrote `POST /menus/:menuId/items` and `GET /menus/:menuId/items`.

```bash
curl -X POST http://localhost:3000/api/v1/menus/$MENU_ID/items \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"nameVi":"Pho Bo","price":65000,"category":"Main course","descVi":"Traditional beef pho","status":"available"}'
```

### Day 4 - Thursday, 02/07/2026

Edit/delete items + mock data.

- Wrote `PATCH /menus/:menuId/items/:itemId` (change price/status/desc) and `DELETE`.
- Tested changing an item to `sold_out`:

```bash
curl -X PATCH http://localhost:3000/api/v1/menus/$MENU_ID/items/$ITEM_ID/status \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"price":70000,"status":"sold_out"}'
```

- Added some mock data (a few pho, rice, and drink items) so the FE has something to render instead of a blank screen.

### Day 5 - Friday, 03/07/2026

Allergen tagging.

- Finalized a list of 14 allergens based on EU standards (gluten, peanuts, milk, eggs, seafood, etc.) and put them in constants.
- Design: each item has an `allergenTags` array, each tag has `allergen`, `confidence` (contains / may_contain), and a `verified` flag (has the owner confirmed it).
- Wrote `PATCH /menus/:menuId/items/:itemId/allergens`.

```bash
curl -X PATCH http://localhost:3000/api/v1/menus/$MENU_ID/items/$ITEM_ID/allergens \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"allergenTags":[{"allergen":"gluten","confidence":"contains"},{"allergen":"soy","confidence":"may_contain"}],"verified":true}'
```

Future idea: later we can let AI suggest allergens from the dish name/description, and the owner just clicks to confirm (`verified = true`). For now, I only built the data and API layer, no AI yet.

### Day 6 - Saturday, 04/07/2026

Bug fixing and FE integration.

- Checked validation: price cannot be negative, category cannot be empty, allergens must be in the allowed 14 types.
- Fixed a bug: deleting a menu without deleting its items left orphaned items. Added a step to delete items by menuId when a menu is deleted.
- Integrated with FE: they built the owner app's menu management screen; I adjusted a few field names to match and added clearer error messages.

## Week Achievements

- Menu has a draft/published/archived lifecycle; publishing auto-archives old ones.
- Full CRUD for menus and menu items.
- Allergen tagging with confidence levels and verified flags, restricted to 14 standard types.
- Mock data populated for FE rendering and testing.

## Difficulties Encountered

- The "only one published menu" rule required careful coding to avoid race conditions or accidental double-publishing.
- Orphaned items bug when deleting menus reminded me that Mongo doesn't have native foreign keys; I have to manage data integrity manually.
- Initially typing the 14 allergens by hand led to typos; moving them into shared constants ensured BE and FE consistency.

## Lessons Learned

- Versioning adds complexity but aligns with real restaurant needs - we shouldn't just allow in-place overrides out of laziness.
- Without foreign keys, you must handle data integrity yourself, especially during deletions.
- Extracting shared data (like allergens) into constants keeps the whole system consistent and prevents BE/FE mismatches.

## Week 10 Plan

- Guest session: guests scan QR to create a session (no account needed), declare allergies.
- Public menu view: guests view the published menu with allergen warnings (red/yellow/green).
- Orders: guests place orders, owners manage orders via a status pipeline.

## End-of-week Remarks

This was the heaviest week so far because the menu is the heart of the product. Finishing the versioning and allergen features made the product feel "unique" rather than just standard CRUD. I've noted down the AI allergen suggestion idea to work on after the core flow is stable.
