---
title: "Week 12 Worklog"
date: 2026-07-20
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

### Week 12 Goals:

- Strengthen security: rate limiting, reviewing authorization across the whole system.
- Write tests for the main flows and clean up the source code.
- Complete the AWS deployment and prepare the project demo.

### Activities Implemented During the Week:

| Day | Activities                                                                                                                                                                                                                                                                                                                                       | Start Date | Completion Date | Reference                                    |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | -------------------------------------------- |
| 2   | - Reviewed system security: <br>&emsp; + Added express-rate-limit for login/register <br>&emsp; + Configured cors with the correct origin instead of `*` <br>&emsp; + Reviewed security headers with helmet <br> - **Hands-on:** <br>&emsp; + Reviewed every route to check the `authenticate` middleware                                        | 20/07/2026 | 20/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 3   | - Standardized authorization and ownership checks: <br>&emsp; + Every operation must verify the resource belongs to the currently logged-in owner <br> - **Hands-on:** <br>&emsp; + Wrote a shared ownership-check helper <br>&emsp; + Tested that owner A's token calling owner B's API is blocked with 403                                     | 21/07/2026 | 21/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 4   | - Wrote tests for the main flows: <br>&emsp; + Auth: register, login with wrong password, refresh token <br>&emsp; + Order: valid order, ordering a sold_out item, skipping a status transition <br> - **Hands-on:** <br>&emsp; + Standardized returned status codes                                                                             | 22/07/2026 | 22/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 5   | - Cleaned up the source code: <br>&emsp; + Reviewed winston/morgan logging, removed console.log <br>&emsp; + Centralized error codes in one place <br>&emsp; + Formatted with Prettier, fixed TypeScript warnings <br> - **AWS:** <br>&emsp; + Configured environment variables for Lambda <br>&emsp; + Checked logs and debugged via CloudWatch | 23/07/2026 | 23/07/2026      | <https://000008.awsstudygroup.com>           |
| 6   | - Coordinated with the frontend to trial-run the whole system: <br>&emsp; + The 3 apps (owner, tablet, landing) call the real API instead of mocks <br>&emsp; + Fixed CORS errors and mismatched field names <br> - **AWS:** <br>&emsp; + Verified the entire flow on CloudFront + S3 + Lambda                                                   | 24/07/2026 | 24/07/2026      | <https://github.com/MT-KS-04/smart-menu-fe>  |
| 7   | - Prepared the demo and wrapped up the project: <br>&emsp; + Wrote the README: setup guide, environment variables, endpoint list <br>&emsp; + Prepared demo data <br>&emsp; + Summarized the work and noted follow-up items                                                                                                                      | 25/07/2026 | 25/07/2026      | <https://github.com/MT-KS-04/smart-menu-api> |

### Achievements During Week 12:

- Strengthened system security:
  - Added rate limiting on sensitive routes (login, register) to prevent brute force
  - Tightened CORS configuration to each app's correct origin instead of allowing everything
  - Reviewed security headers with helmet
  - Found and patched an authorization vulnerability in the floor-tables module

- Standardized authorization across the whole system:
  - Unified principle: every operation must verify the resource belongs to the currently logged-in owner
  - Wrote a shared ownership-check helper for menu, order, reservation, payment, floor-table
  - Verified that one owner's token cannot operate on another owner's resources

- Built a test suite for important flows:
  - Tested the auth module: registration, wrong-password login, refresh token
  - Tested the order flow: valid ordering, blocking sold_out orders, blocking skipped status transitions
  - Standardized returned status codes for consistency

- Cleaned up and polished the source code:
  - Standardized logging with winston/morgan
  - Centralized error codes and messages in one place
  - Formatted the entire codebase, fixed remaining TypeScript warnings

- Completed the AWS deployment:
  - Architecture: CloudFront (CDN) + S3 (frontend) + Lambda Function URL (backend API)
  - Configured environment variables for Lambda
  - Checked logs and debugged via CloudWatch
  - Successfully ran the entire flow on AWS

- Completed the end-to-end demo scenario: owner creates a restaurant → builds a menu → publishes it → guest scans QR → orders → owner processes the order → payment → reviews payment history.

- Wrapped up the SmartMenu project after 6 weeks:
  - Backend: fully complete (auth, restaurant, QR, menu versioning, allergen, session, order, payment, reservation, operating hours)
  - Frontend: completed alongside a team member across 3 apps (owner, tablet, landing)
  - Next steps identified: AI-suggested allergens, realtime order updates, optimizing the session lifecycle
