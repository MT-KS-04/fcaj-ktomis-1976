---
title: "Week 8 Worklog"
date: 2026-06-22
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

## General Information

| Content | Details |
| --- | --- |
| Time | 22/06/2026 - 28/06/2026 |
| Internship Week | Week 8 |
| Phase | SmartMenu - Restaurant, tables, QR codes, and floor plans |
| Role | Full-stack, responsible for backend; assisted with frontend |
| Main Focus | Restaurant module, QR generation per table, revoke QR, Floor Tables |

## Week 8 Direction

With auth in place, this week is about building the "frame" of the restaurant: each owner can create a restaurant, and the system automatically generates a list of tables with QR codes. The QR code is the gateway for guests to order, so it must be secure, including a revocation mechanism. Concurrently, we are starting the floor tables module for owners to arrange tables by floor/zone.

## Week 8 Objectives

- Model `Restaurant` + `Table`, each owner has one restaurant.
- Auto-generate tables + QR secret based on `tableCount` upon restaurant creation.
- API to get table QR and revoke/regenerate QR.
- Model + CRUD for `FloorTable` (floor, zone, seats, tableNumber).

## Work Carried Out During the Week

### Day 1 - Monday, 22/06/2026

Design and create the restaurant.

- Designed `Restaurant` model: name, address, phone, status, ownerId. Enforced unique constraint so each owner has only one restaurant.
- Wrote the create restaurant controller, receiving `tableCount` to know how many tables to generate.
- Finalized data idea: each table has a `tableNumber` + random `qrSecret`.

```bash
curl -X POST http://localhost:3000/api/v1/restaurants \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"name":"Pho 24","address":"123 Test Street","tableCount":10,"phone":"0987654321"}'
```

### Day 2 - Tuesday, 23/06/2026

Generate tables + QR secret.

- Wrote a function to generate `tableCount` tables, assigning a random `qrSecret` using `crypto` to each.
- Initially planned to store tables as a separate collection, but since the number of tables is small, I embedded the `tables` array into the Restaurant document for easier joining - adjusted schema accordingly.
- Added `GET /restaurants/me` for owners to fetch their restaurant.

### Day 3 - Wednesday, 24/06/2026

API to fetch QR per table.

- Wrote `GET /restaurants/:restaurantId/tables/:tableNumber/qr` returning data for FE to render the QR.
- Agreed with FE: backend returns payload (restaurantId + tableNumber + qrSecret), drawing the QR image is handled client-side by an FE library to reduce server load.
- Adjusted logic: only the owning restaurant owner can view the QR, added permission checks.

### Day 4 - Thursday, 25/06/2026

Revoke / regenerate QR.

- Wrote `POST /restaurants/:restaurantId/tables/:tableNumber/qr/revoke`: generates a new `qrSecret`, rendering the old one invalid.
- Reason: if a QR is photographed and posted elsewhere, the owner can revoke it.
- Tested the flow: create restaurant -> get QR -> revoke -> old QR can't be used to create sessions anymore.

Minor bug: forgot to call `.save()` after changing the secret during revoke, so it kept returning the old secret. Adding `save` fixed it.

### Day 5 - Friday, 26/06/2026

Started Floor Tables.

- Designed `FloorTable` model: floor, zone, seats, tableNumber, status, restaurantId. This is separate from the QR tables list because it serves the physical layout mapping.
- Wrote `POST /floor-tables` and `GET /floor-tables`.

```bash
curl -X POST http://localhost:3000/api/v1/floor-tables \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"floor":1,"zone":"Garden","seats":4,"tableNumber":5}'
```

### Day 6 - Saturday, 27/06/2026

Completed Floor Tables + FE integration.

- Wrote `PATCH /floor-tables/:id` (change zone/seats/status) and `DELETE /floor-tables/:id`.
- Added a public route `GET /public/restaurants/:restaurantId/floor-tables` for guests to view the layout (no auth required).
- Paired with the FE dev to integrate the owner app's table management screen with these APIs, fixing field names to match FE types.

## Week Achievements

- Owners can create restaurants; system auto-generates tables + QRs.
- QR fetching and revoking APIs are functional with ownership checks.
- Floor Tables module CRUD completed, with a public layout route for guests.
- FE owner app successfully integrated the table management section.

## Difficulties Encountered

- Debated between embedding tables or keeping them in a separate collection. Decided to embed for simplicity, but had to rewrite the schema I already drafted.
- Forgetting `.save()` when modifying `qrSecret` made me think the revoke logic was wrong; took a while to realize it wasn't persisting to the DB.
- Two similar "table" concepts caused confusion: QR-attached tables and floor plan tables. Had to name them clearly (`tables` vs `floor-tables`) so the team wouldn't mix them up.

## Lessons Learned

- QR codes are security-sensitive, so building revocation from day one was the right move to avoid patching it later.
- With Mongo, embedding vs referencing depends on query patterns and volume. Here, embedding was the right call.
- Naming similar concepts distinctly helps the whole team avoid misunderstandings during API integration.

## Week 9 Plan

- Menu module: versioned menus (draft -> published -> archived).
- Menu items: CRUD, categorization, pricing, status.
- Allergen tagging: tag items with allergens (14 types based on EU standards).

## End-of-week Remarks

Things are taking shape this week: we have a restaurant, tables, and QRs - things the FE can render visibly, which brings more motivation. Coding while actively syncing with the FE dev made me pay closer attention to field naming and consistent responses.
