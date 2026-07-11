---
title: "Week 12 Worklog"
date: 2026-07-09
weight: 12
chapter: false
pre: " <b> 1.12. </b> "
---

## General Information

| Content | Details |
| --- | --- |
| Time | 19/07/2026 - 25/07/2026 |
| Internship Week | Week 12 |
| Phase | SmartMenu - Polish, security, testing, and demo |
| Role | Full-stack, responsible for backend; assisted with frontend |
| Main Focus | Rate limits, permission checks, writing tests, FE integration, demo prep |

## Week 12 Direction

For the final week of this phase, I'm not adding major features but focusing on making the system **solid and secure**: adding rate limits, re-checking owner permissions across routes, writing tests for core flows, cleaning up code, and finishing frontend integration to prepare for the demo. This is the least "glamorous" part but dictates whether the product is actually usable.

## Week 12 Objectives

- Add rate limiting and review basic security flaws.
- Review all owner routes to ensure correct authorization.
- Write tests for auth, orders, and a few critical flows.
- Finish FE integration, clean code, prepare demo and docs.

## Work Carried Out During the Week

### Day 1 - Monday, 20/07/2026

Security review.

- Added `express-rate-limit` to sensitive routes (login, register) to prevent brute force attacks.
- Reviewed security headers with `helmet`, configured `cors` to allow exact origins of the owner/tablet/landing apps instead of `*`.
- Read through all routes to check if I missed the `authenticate` middleware anywhere.

Found an exposed `floor-tables` route that wasn't checking permissions; anyone with a token could edit another restaurant's tables. Fixed it by adding an ownerId check.

### Day 2 - Tuesday, 21/07/2026

Authorization and ownership checks.

- Established a rule: every operation on a restaurant's resource must verify that the resource belongs to the currently logged-in owner.
- Wrote a shared ownership-check helper for menu, order, reservation, payment, and floor-table instead of repeating the check in every controller.
- Tested it: used owner A's token to try editing owner B's menu -> correctly blocked with 403.

### Day 3 - Wednesday, 22/07/2026

Writing tests.

- Set up Vitest/Jest for the backend, wrote tests for auth (register/login with wrong password, refresh token).
- Wrote tests for the order flow: valid orders, ordering a sold-out item (must fail), skipping status in the pipeline (must fail).
- Running tests revealed some inconsistent status codes (400 vs 422); standardized them.

### Day 4 - Thursday, 23/07/2026

Code cleanup and logging.

- Reviewed winston/morgan loggers, removed leftover `console.log` statements from debugging.
- Standardized error messages returned to the FE, grouped error codes in one place.
- Formatted everything with Prettier, fixed remaining TypeScript type warnings.

### Day 5 - Friday, 24/07/2026

Final FE integration and full system run.

- Sat with the FE dev to review all 3 apps (owner, tablet, landing) to ensure they call the real APIs instead of mocks.
- Fixed a few CORS errors when FE called from different origins, and fixed mismatched field names between FE types and BE responses.
- Ran a full end-to-end scenario: owner creates restaurant -> drafts menu -> publishes -> guest scans QR -> orders -> owner processes order -> payment -> views payment history.

### Day 6 - Saturday, 25/07/2026

Demo prep and wrap-up.

- Rewrote the backend README: description, how to run, env variables, list of endpoints with curl examples.
- Prepared clean demo data so the presentation runs smoothly.
- Summarized everything done in the 6-week project, noted features saved for later (AI allergen suggestions, real-time orders, optimizing sessions with TTL index).

## Week Achievements

- Added rate limits, tightened CORS, and patched a permission flaw in floor-tables.
- Created a shared ownership-check helper for consistent authorization across the system.
- Built a test suite for auth and orders, standardized status codes.
- 3 FE apps running with the real backend, completed end-to-end demo script.
- README and demo data are ready.

## Difficulties Encountered

- The permission flaw in floor-tables almost slipped by - reminded me to systematically review permissions instead of assuming "I probably checked it."
- Inconsistent status codes caused tests to fail randomly; had to unify conventions.
- Integrating with the real backend revealed mismatched field names that weren't visible when using mock APIs.

## Lessons Learned

- Security and permissions must be reviewed systematically; forgetting one check creates a vulnerability.
- Writing tests takes time but catches inconsistencies that reading code usually misses.
- Mock APIs are great for parallel FE development, but you must test against the real backend early to catch contract differences.

## Project Phase Summary (Weeks 7-12)

After 6 weeks, our team completed most of the SmartMenu MVP. On the backend (which I handled entirely), I built everything from scratch: owner auth, restaurant and QR management, versioned menus with allergen tagging, guest QR sessions, orders with status pipelines, payments and refunds, reservations, operating hours, and public routes for guests. A teammate handled the UI for the 3 apps (owner, tablet, landing), and I coordinated on API contracts and integration.

Saved for later: AI allergen suggestions from dish descriptions, real-time order updates instead of guest polling, and optimizing session lifecycles.

## End-of-week Remarks

Wrapping up the project phase, I feel much more confident than when I just finished learning the theory. Building the entire backend of a real system taught me what it feels like to go from ideation, data design, coding, refactoring, to integrating with the frontend and handling security. Working with the FE dev also taught me how to collaborate effectively rather than just working in a silo.
