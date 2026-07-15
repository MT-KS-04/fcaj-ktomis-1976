---
title: "Week 7 Worklog"
date: 2026-06-15
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

## General Information

| Content | Details |
| --- | --- |
| Time | 15/06/2026 - 21/06/2026 |
| Internship Week | Week 7 |
| Phase | Starting SmartMenu project - Initialization & Authentication |
| Project | SmartMenu (digital menu & ordering system via QR code) |
| Role | Full-stack, responsible for the entire backend; assisted with frontend |
| Main Focus | Architecture, schema design, API skeleton setup, and auth module |

## Week 7 Direction

Starting this week, our team transitioned from the learning phase to the actual project: **SmartMenu** - a system that allows restaurant owners to manage menus, tables, and orders; while guests scan a QR code on their table to view the menu and order without an account. Since I am handling the backend, the first week focused on laying the foundation: deciding the tech stack, directory architecture, schema design, and finishing the authentication module for restaurant owners.

Frontend is handled by another team member who focuses on the UI. I primarily align data flows and API contracts so both sides match.

## Week 7 Objectives

- Finalize the tech stack and set up the backend project skeleton.
- Preliminary design of collections in MongoDB.
- Implement the auth module: register, login, JWT access token + refresh token.
- Build authentication and centralized error handling middleware.

## Work Carried Out During the Week

### Day 1 - Monday, 15/06/2026

Finalized the approach and initialized the project.

- Had a team meeting to finalize the MVP scope: restaurant owners manage menus/orders, guests scan QR codes to order.
- Decided on the backend stack: Node.js + TypeScript + Express + MongoDB (Mongoose). The reason for choosing Mongo is that menu/order data is quite flexible, making it easier to constantly migrate schemas in the early stages.
- Ran `npm init`, set up the directory structure: `config`, `controller/v1`, `router/v1`, `model`, `middleware`, `lib`, `utils`.
- Installed `express`, `mongoose`, `dotenv`, set up `nodemon` + `ts-node` for dev.

By the end of the day, I had the server running via `npm run dev` on `http://localhost:3000/api/v1` with the `/health` route returning ok.

### Day 2 - Tuesday, 16/06/2026

Designed schemas and connected the database.

- Sketched out the main collections on paper first: `Owner`, `Restaurant`, `Menu`, `MenuItem`, `Order`, `Session`, `Token`. The rest (Payment, Reservation, FloorTable) will be handled in the coming weeks.
- Wrote `lib/mongoose.ts` to connect to Mongo via `MONGOOSE_URL`, logging the connection status with Winston.
- Created the `Owner` model with email + passwordHash, added a unique index for email.

Encountered an issue where TypeScript path aliases (`@/...`) weren't working. Had to add `tsconfig-paths` to nodemon to use absolute imports instead of `../../..`.

### Day 3 - Wednesday, 17/06/2026

Implemented the registration flow.

- Wrote the `register` controller: validated email/password using `express-validator`, hashed the password using `bcryptjs`, and saved the Owner.
- Built middleware to catch validation errors and return a consistent format.
- Tested via curl:

```bash
curl -X POST http://localhost:3000/api/v1/auth/register \
  -H "Content-Type: application/json" \
  -d '{"email":"owner@example.com","password":"Password123!"}'
```

Initially forgot `await` when hashing the password, causing `passwordHash` to be saved as a Promise (`[object Promise]`), which took me a while to figure out. Adding `await` fixed it.

### Day 4 - Thursday, 18/06/2026

Implemented login + JWT flow.

- Wrote the `login` controller: found the owner by email, compared passwords with `bcrypt.compare`, and signed an access token using `jsonwebtoken`.
- Decided on a 2-token mechanism: a short-lived access token returned in the response, and a long-lived refresh token set as an httpOnly cookie for security.
- Created `lib/jwt.ts` to group signing/verifying functions.

```bash
curl -X POST http://localhost:3000/api/v1/auth/login \
  -c cookies.txt \
  -H "Content-Type: application/json" \
  -d '{"email":"owner@example.com","password":"Password123!"}'
```

### Day 5 - Friday, 19/06/2026

Refresh token + logout + auth middleware.

- Saved the refresh token to the `Token` collection for revocation capabilities (logout deletes it).
- Wrote the `refresh-token` route: reads the cookie, verifies it, and issues a new access token.
- Wrote the `authenticate` middleware: reads the `Authorization: Bearer` header, verifies the access token, and attaches `ownerId` to the request.
- Added a `logout` route that revokes the current refresh token.

Encountered an issue where refreshing kept failing. Turns out I forgot to use `cookie-parser`, so `req.cookies` was undefined. Added the middleware and it worked.

### Day 6 - Saturday, 20/06/2026

Clean-up and synchronization with frontend.

- Standardized response formats (grouped success/error functions in `utils`) to make parsing easier for the frontend.
- Added `helmet`, `cors`, and `compression` to the app.
- Met with the frontend developer to align on base URLs, token formatting, and the login flow to integrate into the owner app.
- Documented environment variables in `.env.example`.

## Week Achievements

- Successfully set up a running backend skeleton with a `/health` endpoint.
- Connected to MongoDB and finalized the core schema designs to get started.
- Completed the auth module: register, login, refresh token, logout.
- Established auth and centralized error-handling middlewares for future modules.

## Difficulties Encountered

- TypeScript path aliases took some time early in the week. Importing was messy until I added `tsconfig-paths`.
- Forgetting `await` when hashing the password was a silly mistake that took long to debug because the code looked fine; I only realized it when I checked the DB and saw `[object Promise]`.
- Refresh token failed due to missing `cookie-parser` - a reminder that missing small middlewares can break the entire flow.

## Lessons Learned

- Take the time to sketch out schemas on paper before coding to avoid constant refactoring, even though Mongo is flexible.
- Separating tokens into a short-lived access token and an httpOnly refresh token is extra work but much more secure. It's worth investing time in this early on.
- Finalizing the API contract with the frontend early saves a lot of back-and-forth later caused by misunderstandings.

## Week 8 Plan

- Work on the Restaurant module: each owner has one restaurant, automatically generating tables + QR codes based on `tableCount`.
- Implement functionality to retrieve and revoke QR codes per table.
- Start the Floor Tables module (table mapping by floor/zone).

## End-of-week Remarks

The first week of the project was mostly about setting up the foundation, so there aren't many "visible" features yet. However, building the auth and architecture solidly means later modules will be integrated much faster. I found that working on a real project is quite different from studying; you have to think ahead about scalability, not just write code that "runs".
