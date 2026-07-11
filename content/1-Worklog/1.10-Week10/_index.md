---
title: "Week 10 Worklog"
date: 2026-07-05
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

## General Information

| Content | Details |
| --- | --- |
| Time | 05/07/2026 - 11/07/2026 |
| Internship Week | Week 10 |
| Phase | SmartMenu - Guest session, public menu view, and ordering |
| Role | Full-stack, responsible for backend; assisted with frontend |
| Main Focus | Guest session via QR, public menu view, orders + status pipeline |

## Week 10 Direction

This week is for the **guests** - the other half of the product. Guests scan a QR on the table to open a session (no account registration needed), view the published menu, declare their allergies so the system warns them about safe/unsafe dishes, and then place orders. On the owner's side, they receive the orders and push the order status along a fixed pipeline. This is when the isolated modules from previous weeks start connecting.

## Week 10 Objectives

- Guest session: create a session by scanning QR (verify qrSecret), auto-expire when inactive.
- Declare allergies/preferences tied to the session.
- Public menu view: return the published menu with matching allergen tags (red/yellow/green).
- Orders: guests place orders, owners manage orders through the `pending -> ... -> completed` pipeline.

## Work Carried Out During the Week

### Day 1 - Monday, 06/07/2026

Create guest session.

- Designed the `Session` model: restaurantId, tableNumber, allergens, preferences, status, expiration time.
- Wrote `POST /sessions`: receives restaurantId + tableNumber + qrSecret, verifies the secret matches the table before creating a session.
- This connects to Week 8's QR logic: if the owner revoked it, the old secret fails verification, preventing session creation.

```bash
curl -X POST http://localhost:3000/api/v1/sessions \
  -H "Content-Type: application/json" \
  -d '{"restaurantId":"'"$RESTAURANT_ID"'","tableNumber":5,"qrSecret":"'"$QR_SECRET"'"}'
```

### Day 2 - Tuesday, 07/07/2026

Session expiration + declaring allergies.

- Added logic for sessions to auto-expire after a period of inactivity (save `expiresAt`, check on usage).
- Wrote `PATCH /sessions/:sessionId/allergens` for guests to declare allergies and preferences.
- Considered using Mongo's TTL index for expiration, but temporarily checking manually against `expiresAt` for easier control; noted for future optimization.

### Day 3 - Wednesday, 08/07/2026

Public menu view + allergen tagging.

- Wrote `GET /public/restaurants/:restaurantId/menu?sessionId=...&lang=vi`: returns published menu + items.
- Match tagging logic: compares the item's allergens with the guest's declared allergens in the session -> tags it red (contains allergen), yellow (may contain), or green (safe).
- This is the best part: Week 9's allergen data is finally being used in a real scenario.

Had a bug: when a session hadn't declared allergies yet, all items were green - which is correct, but initially I left it as null, causing a crash. Defaulting to an empty array fixed it.

### Day 4 - Thursday, 09/07/2026

Ordering (guest) + Order model.

- Designed `Order` model: sessionId, list of items (menuItemId, quantity, notes), customerNotes, status, restaurantId.
- Wrote `POST /orders` for guests (no auth required, scoped by sessionId).
- Validation: ordered items must belong to the currently published menu and be `available`.

```bash
curl -X POST http://localhost:3000/api/v1/orders \
  -H "Content-Type: application/json" \
  -d '{"sessionId":"'"$SESSION_ID"'","items":[{"menuItemId":"'"$ITEM_ID"'","quantity":2,"notes":"Less onions"}],"customerNotes":"Very spicy"}'
```

### Day 5 - Friday, 10/07/2026

Status pipeline + owner order management.

- Finalized a one-way pipeline: `pending -> confirmed -> preparing -> ready -> served -> completed`, or `cancelled`.
- Wrote `PATCH /orders/:orderId/status` for owners, blocking backward or skipped status jumps.
- Wrote `GET /orders` (owners view restaurant orders) and `GET /orders/session/:sessionId` (guests poll their own orders).

Initially I allowed free status changes, but realized it was dangerous (a completed order going back to pending), so I wrote a valid transition table to only allow moving forward.

### Day 6 - Saturday, 11/07/2026

FE tablet + owner integration.

- Connected the tablet app (guest ordering screen) with the session -> menu -> order flow.
- Connected the owner app with the order list screen and status change buttons.
- Fixed a few time formatting and status name issues to match FE's i18n.
- Tested an end-to-end loop: scan QR -> view menu -> place order -> owner pushes status -> guest sees update.

## Week Achievements

- Guests can create a session via QR with secret verification and expiration.
- Allergy declaration and public menu view with red/yellow/green warning tags.
- Ordering and tracking orders by session.
- Owners manage orders via a one-way pipeline with controlled status transitions.
- Successfully ran an end-to-end loop between the tablet, owner, and backend.

## Difficulties Encountered

- Allergy tag logic crashed when the session hadn't declared anything due to a null value; fixed by defaulting to an empty array.
- A free-form status pipeline is a recipe for messy data; had to implement a strict transition table for peace of mind.
- Testing end-to-end requires many variables (restaurantId, qrSecret, sessionId, itemId), so I wrote a small script to set variables for easier typing.

## Lessons Learned

- Data prepared last week (allergens) "came alive" this week - showing that designing properly early on makes integration later very smooth.
- Business statuses should strictly constrain the workflow direction; never trust the API caller to change it correctly.
- Having a working end-to-end flow early helped me and the FE spot API contract mismatches much faster.

## Week 11 Plan

- Cash payment: mark open orders of a session as completed, record Payment.
- Payments: list, paginate, refund.
- Reservations and Operating Hours.

## End-of-week Remarks

This week the product actually worked in a "full loop," which is quite exciting. Seeing a guest scan a QR and the order pop up on the owner's side made the effort of laying the foundation in previous weeks visibly pay off. Still have payments and reservations to complete the business logic.
