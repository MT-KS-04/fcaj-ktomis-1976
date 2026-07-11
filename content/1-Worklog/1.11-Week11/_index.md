---
title: "Week 11 Worklog"
date: 2026-07-09
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

## General Information

| Content | Details |
| --- | --- |
| Time | 12/07/2026 - 18/07/2026 |
| Internship Week | Week 11 |
| Phase | SmartMenu - Payments, reservations, and operating hours |
| Role | Full-stack, responsible for backend; assisted with frontend |
| Main Focus | Cash payment, Payments + refund, Reservations, Operating Hours |

## Week 11 Direction

With the ordering loop running, this week I am filling in the missing business logic to make it a real restaurant system: cash payments and payment history (including refunds), reservations (both owner-created and guest self-booking), and operating hours by day of the week. These parts aren't technically hard, but they have many business constraints that require care.

## Week 11 Objectives

- Cash payment: close all open orders of a session and record a Payment.
- Payments: list/paginate, refund a completed payment.
- Reservations: owners create/list and change status; guests self-book via public route.
- Operating Hours: configure open/close times by day (Mon-Sun).

## Work Carried Out During the Week

### Day 1 - Monday, 13/07/2026

Cash payment.

- Designed `Payment` model: sessionId, restaurantId, total amount, status (completed / refunded), timestamp.
- Wrote `POST /orders/session/:sessionId/cash-payment`: sums all open orders of a session, marks them as completed, and creates a Payment.
- Had to ensure correctness here: excluding cancelled orders, and blocking a session from paying twice.

```bash
curl -X POST http://localhost:3000/api/v1/orders/session/$SESSION_ID/cash-payment
```

### Day 2 - Tuesday, 14/07/2026

Payment list + pagination.

- Wrote `GET /payments` with status filtering and pagination (page, limit).
- Standardized pagination response (total, page, limit, data) to make table rendering easy for FE.
- Added mock payment data to ensure pagination doesn't break on page 2.

### Day 3 - Wednesday, 15/07/2026

Refund.

- Wrote `POST /payments/:id/refund`: only `completed` payments can be refunded, changes status to `refunded`.
- Block double refunds: returns a clear error if already refunded.
- Discussed whether to "re-open" orders upon refund; the team agreed the MVP will just mark the payment refunded without reverting orders - noted for future updates.

### Day 4 - Thursday, 16/07/2026

Reservations (owner side).

- Designed `Reservation` model: customerName, customerPhone, time, partySize, tableNumber, notes, status.
- Pipeline: `pending -> confirmed -> seated -> completed`, or `cancelled` / `no_show`.
- Wrote `POST /reservations`, `GET /reservations` (status filter + pagination), `PATCH /reservations/:id/status`.

```bash
curl -X POST http://localhost:3000/api/v1/reservations \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"customerName":"Nguyen Van A","customerPhone":"0987654321","time":"2026-07-20T18:30:00.000Z","partySize":4,"tableNumber":5}'
```

### Day 5 - Friday, 17/07/2026

Reservations (guest side) + Operating Hours.

- Wrote public route `POST /public/restaurants/:restaurantId/reservations`: guests self-book, always created with `pending` status for owner approval.
- Designed `OperatingHours`: each day has `isOpen`, `openTime`, `closeTime` in `HH:mm` format.
- Wrote `GET /operating-hours` and `PATCH /operating-hours` (update one or multiple days).

```bash
curl -X PATCH http://localhost:3000/api/v1/operating-hours \
  -H "Authorization: Bearer $ACCESS_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"monday":{"isOpen":true,"openTime":"09:00","closeTime":"21:00"}}'
```

Time validation bug: initially I didn't check that `openTime` must be before `closeTime`; entering them backward still saved. Added a time comparison check.

### Day 6 - Saturday, 18/07/2026

Remaining public routes + FE integration.

- Added `GET /public/restaurants/:restaurantId/operating-hours` so landing/tablet apps can display open hours.
- Integrated with FE: owner app built the payments screen (table + refund button) and reservations; landing app built the guest booking form.
- Adjusted some date/time and currency formatting to align BE and FE.

## Week Achievements

- Cash payment sums session orders and records a Payment.
- Payment listing/pagination and refunding (with double-refund blocking).
- Full reservations: owner create/approve and guest public booking.
- Operating hours by day, with valid time checks.
- FE successfully integrated payments, reservations, and booking forms.

## Difficulties Encountered

- Cash payment required careful calculation of valid orders (skipping cancelled ones) and preventing double payments - more business logic than technical.
- Forgot to validate `openTime < closeTime`, allowing reversed times to be saved. Had to add explicit checks.
- Multiple status pipelines (order, reservation) are similar; had to cleanly separate each transition table to avoid mixing them up.

## Lessons Learned

- "Deceptively simple" features like payments and reservations are full of constraints. Coding them to run is fast, coding them correctly takes effort.
- Input data validation (time, money, statuses) must be thorough; bugs like reversed times slip through easily.
- When there are multiple similar pipelines, keeping them strictly separated from the start is less confusing than combining them for "brevity."

## Week 12 Plan

- Security review: rate limiting, re-checking permissions on owner routes.
- Write tests for main flows.
- Finalize and polish FE integration, prep for demo/deployment.

## End-of-week Remarks

After this week, most of the business logic is complete: ordering, payment, booking, and operating hours. The backend is almost fully formed; what's left is security checks, writing tests, and solidifying everything before the demo. It's starting to look like a real system rather than a collection of APIs.
