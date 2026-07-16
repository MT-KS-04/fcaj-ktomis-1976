---
title: "Week 10 Worklog"
date: 2026-07-06
weight: 10
chapter: false
pre: " <b> 1.10. </b> "
---

### Week 10 Goals:

- Build guest sessions via QR scan, without needing an account.
- Build a public menu with allergen warnings by severity level (red/yellow/green).
- Build ordering and manage orders through a status pipeline.
- In parallel: sync the frontend to S3 and verify via CloudFront.

### Activities Implemented During the Week:

| Day | Activities                                                                                                                                                                                                                                                                                                              | Start Date | Completion Date | Reference                                    |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | -------------------------------------------- |
| 2   | - Designed the Session model: <br>&emsp; + restaurantId, tableNumber <br>&emsp; + allergens, preferences <br>&emsp; + status, expiresAt <br> - **Hands-on:** <br>&emsp; + Wrote `POST /sessions`, verifying `qrSecret` before creating a session                                                                        | 06/07/2026 | 06/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 3   | - Built session expiration and allergen declaration: <br>&emsp; + Sessions auto-expire after inactivity <br>&emsp; + Guests declare allergens and preferences <br> - **Hands-on:** <br>&emsp; + Wrote `PATCH /sessions/:id/allergens`                                                                                   | 07/07/2026 | 07/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 4   | - Built the public menu with allergen warnings: <br>&emsp; + Matched each item's allergens against the guest's declaration <br>&emsp; + Red label (contains) / yellow (may contain) / green (safe) <br> - **Hands-on:** <br>&emsp; + Wrote `GET /public/restaurants/:id/menu`                                           | 08/07/2026 | 08/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 5   | - Designed the Order model and ordering function: <br>&emsp; + sessionId, items, customerNotes, status <br>&emsp; + Verified items belong to a published, available menu <br> - **Hands-on:** <br>&emsp; + Wrote `POST /orders` for guests <br> - **AWS:** <br>&emsp; + Synced the frontend build to S3 (`aws s3 sync`) | 09/07/2026 | 09/07/2026      | <https://000057.awsstudygroup.com>           |
| 6   | - Built the order status pipeline: <br>&emsp; + `pending` → `confirmed` → `preparing` → `ready` → `served` → `completed` <br>&emsp; + Blocked backward or skipped status transitions <br> - **Hands-on:** <br>&emsp; + Wrote `PATCH /orders/:id/status` <br>&emsp; + Wrote `GET /orders` and `GET /orders/session/:id`  | 10/07/2026 | 10/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 7   | - Coordinated with the frontend to wire up the tablet and owner apps <br> - **AWS:** <br>&emsp; + Created a CloudFront distribution with an S3 origin <br>&emsp; + Created invalidations to refresh new content <br>&emsp; + Verified the end-to-end flow on AWS                                                        | 11/07/2026 | 11/07/2026      | <https://000094.awsstudygroup.com>           |

### Achievements During Week 10:

- Completed guest session functionality:
  - Guests scan the table QR to open a session, no account registration needed
  - `qrSecret` is verified before creating a session; a revoked QR can't be used
  - Sessions auto-expire after a period of inactivity
  - Guests declare allergens and preferences tied to the session

- Completed the public menu with allergen warnings:
  - Returns the published menu with its list of items
  - Matches each item's allergens against the guest's declaration
  - Applies warning labels at 3 levels:
    - Red: the item contains something the guest is allergic to
    - Yellow: the item may contain it
    - Green: the item is safe

- Completed ordering for guests:
  - Order by session, no login required
  - Per-item notes and general order notes
  - Verified items must belong to a published, currently available menu

- Completed order management through a status pipeline:
  - One-directional pipeline: pending → confirmed → preparing → ready → served → completed
  - Blocked backward or skipped status transitions
  - Owners view and process their restaurant's orders
  - Guests track their own order status

- Deployed and verified the project on AWS:
  - Synced the frontend build to S3
  - Created a CloudFront distribution with an S3 origin
  - Created invalidations to refresh content after each build
  - Verified the end-to-end flow on AWS

- Ran a complete scenario: scan QR → view menu → order → owner processes → guest sees updates.
