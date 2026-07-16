---
title: "Week 11 Worklog"
date: 2026-07-13
weight: 11
chapter: false
pre: " <b> 1.11. </b> "
---

### Week 11 Goals:

- Build cash payment functionality and manage payment history and refunds.
- Build reservation functionality (owner-created and guest self-booked).
- Build operating hours configuration for each day of the week.
- In parallel: complete the CloudFront configuration for the frontend apps on AWS.

### Activities Implemented During the Week:

| Day | Activities                                                                                                                                                                                                                                                                                                                                       | Start Date | Completion Date | Reference                                    |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | -------------------------------------------- |
| 2   | - Designed the Payment model: <br>&emsp; + sessionId, restaurantId <br>&emsp; + total amount, status (completed / refunded) <br> - **Hands-on:** <br>&emsp; + Wrote `POST /orders/session/:id/cash-payment` <br>&emsp; + Aggregated open orders, computed the total, blocked repeat payment                                                      | 13/07/2026 | 13/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 3   | - Built the payment list and pagination: <br>&emsp; + Filter by status <br>&emsp; + Pagination (page, limit) <br> - **Hands-on:** <br>&emsp; + Wrote `GET /payments` <br>&emsp; + Standardized the paginated response for the frontend                                                                                                           | 14/07/2026 | 14/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 4   | - Built the refund functionality: <br>&emsp; + Only refund payments currently completed <br>&emsp; + Blocked double refunds <br> - **Hands-on:** <br>&emsp; + Wrote `POST /payments/:id/refund` <br> - **AWS:** <br>&emsp; + Configured a CloudFront behavior for `/api/*` pointing to the Lambda Function URL                                   | 15/07/2026 | 15/07/2026      | <https://000094.awsstudygroup.com>           |
| 5   | - Designed the Reservation model and the owner-side booking function: <br>&emsp; + customerName, customerPhone, time, partySize <br>&emsp; + Pipeline: pending → confirmed → seated → completed <br> - **Hands-on:** <br>&emsp; + Wrote `POST /reservations`, `GET /reservations`, `PATCH /reservations/:id/status`                              | 16/07/2026 | 16/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 6   | - Built guest self-booking and operating hours: <br>&emsp; + Public route for guests to self-book (defaults to pending, awaiting approval) <br>&emsp; + OperatingHours model: isOpen, openTime, closeTime <br> - **Hands-on:** <br>&emsp; + Wrote `GET/PATCH /operating-hours` <br>&emsp; + Validated that `openTime` must be before `closeTime` | 17/07/2026 | 17/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 7   | - Completed the remaining public routes <br> - Coordinated with the frontend to wire up the payments, reservations, and booking form screens <br> - **AWS:** <br>&emsp; + Configured a CloudFront Function to handle SPA routing for the 3 apps <br>&emsp; + Re-synced the build to S3 and created invalidations                                 | 18/07/2026 | 18/07/2026      | <https://github.com/MT-KS-04/smart-menu-fe>  |

### Achievements During Week 11:

- Completed cash payment functionality:
  - Aggregated all open orders for a session to compute the total
  - Only counted orders that hadn't been cancelled
  - Marked the orders as completed and recorded a Payment
  - Blocked repeat payment for an already-paid session

- Completed payment history management:
  - Listed payments with status filtering
  - Standard pagination (total, page, limit, data)
  - Refund functionality for completed payments
  - Blocked double refunds with a clear error message

- Completed reservation functionality:
  - Owners create, list, and approve reservations
  - Guests self-book via a public route, defaulting to pending status awaiting approval
  - Status pipeline: pending → confirmed → seated → completed, or cancelled / no_show
  - Filtering by status and pagination

- Completed operating hours configuration:
  - Configured per day of the week (Monday - Sunday)
  - Each day has an open/closed state and opening/closing time
  - Validated valid hours (`openTime` must be before `closeTime`)
  - Public route so the landing page/tablet can display opening hours

- Completed the AWS deployment configuration:
  - Configured the CloudFront behavior for `/api/*` pointing to the Lambda Function URL
  - Configured a CloudFront Function to handle SPA routing for the 3 apps (owner, tablet, landing)
  - Synced the build to S3 and created invalidations after each update
