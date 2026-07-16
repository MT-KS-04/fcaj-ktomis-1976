---
title: "Week 8 Worklog"
date: 2026-06-22
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
---

### Week 8 Goals:

- Build the Restaurant module: each restaurant owner manages one restaurant.
- Automatically generate a list of tables with QR codes, with a revoke mechanism.
- Build the Floor Tables module (table layout by floor/zone).

### Activities Implemented During the Week:

| Day | Activities                                                                                                                                                                                                                                                                                              | Start Date | Completion Date | Reference                                    |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | -------------------------------------------- |
| 2   | - Designed the Restaurant model: <br>&emsp; + name, address, phone, status <br>&emsp; + Constraint: one restaurant per owner <br> - **Hands-on:** <br>&emsp; + Wrote `POST /restaurants` accepting an extra `tableCount` <br>&emsp; + Tested the API with curl                                          | 22/06/2026 | 22/06/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 3   | - Built the table and QR secret generation mechanism: <br>&emsp; + Auto-generated `tableCount` tables <br>&emsp; + Each table gets a random `qrSecret` via crypto <br> - **Hands-on:** <br>&emsp; + Adjusted the schema: embedded a tables array in Restaurant <br>&emsp; + Wrote `GET /restaurants/me` | 23/06/2026 | 23/06/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 4   | - Built the API to retrieve each table's QR: <br>&emsp; + Backend returns the payload, FE renders the QR image <br>&emsp; + Checked restaurant ownership <br> - **Hands-on:** <br>&emsp; + Wrote `GET /restaurants/:id/tables/:tableNumber/qr`                                                          | 24/06/2026 | 24/06/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 5   | - Built the QR revoke/regenerate function: <br>&emsp; + Generated a new `qrSecret`, invalidating the old QR <br>&emsp; + Purpose: handle cases where a QR is copied <br> - **Hands-on:** <br>&emsp; + Wrote `POST /.../qr/revoke` <br>&emsp; + Tested the flow: create → fetch QR → revoke              | 25/06/2026 | 25/06/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 6   | - Designed the FloorTable model: <br>&emsp; + floor, zone, seats <br>&emsp; + tableNumber, status <br>&emsp; + Kept separate from QR-linked tables <br> - **Hands-on:** <br>&emsp; + Wrote `POST /floor-tables` and `GET /floor-tables`                                                                 | 26/06/2026 | 26/06/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 7   | - Completed Floor Tables: <br>&emsp; + `PATCH /floor-tables/:id` <br>&emsp; + `DELETE /floor-tables/:id` <br>&emsp; + Public route for guests to view the layout <br> - Coordinated with the frontend to wire up the owner app's table management screen                                                | 27/06/2026 | 27/06/2026      | <https://github.com/MT-KS-04/smart-menu-fe>  |

### Achievements During Week 8:

- Completed the Restaurant module:
  - Restaurant owners can create a restaurant with basic information
  - Constraint enforced: each owner can only own one restaurant
  - API `GET /restaurants/me` to fetch the owner's own restaurant

- Built the automatic table and QR code generation mechanism:
  - Auto-generated table numbers based on `tableCount` when creating a restaurant
  - Each table has its own random `qrSecret`
  - Backend returns the payload; the frontend renders the QR image client-side to reduce server load

- Completed the QR code security mechanism:
  - The API for fetching a QR checks restaurant ownership
  - Revoke/regenerate functionality when a QR is copied or leaked
  - Old QR automatically becomes invalid after revoke

- Completed the Floor Tables module (floor plan):
  - Full CRUD: create, view, edit, delete
  - Managed by floor, zone, seat count, status
  - Public route for guests to view the layout and pick a table without needing to log in

- Gained experience designing data with MongoDB:
  - Weighing embedding vs. separate collections depending on data volume and query patterns
  - Naming closely related concepts clearly (`tables` vs `floor-tables`)

- Coordinated with the frontend to wire up the owner app's table management screen.
