---
title: "Week 7 Worklog"
date: 2026-06-15
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Goals:

- Kick off the **SmartMenu** project - a digital menu & QR-based ordering system for restaurants.
- Finalize the architecture, tech stack, and database schema design.
- Complete the Authentication module for restaurant owners.
- Role: Full-stack, responsible for the entire backend; frontend supported by a team member.

### Activities Implemented During the Week:

| Day | Activities                                                                                                                                                                                                                                                                                                                                                        | Start Date | Completion Date | Reference                                    |
| --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | -------------------------------------------- |
| 2   | - Team meeting to finalize the project's MVP scope <br> - Finalized the backend tech stack: <br>&emsp; + Node.js + TypeScript <br>&emsp; + Express <br>&emsp; + MongoDB (Mongoose) <br> - **Hands-on:** <br>&emsp; + Set up the project folder structure <br>&emsp; + Installed dependencies, configured nodemon + ts-node <br>&emsp; + Built the `/health` route | 15/06/2026 | 15/06/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 3   | - Designed the database schema: <br>&emsp; + Owner, Restaurant <br>&emsp; + Menu, MenuItem <br>&emsp; + Order, Session, Token <br> - **Hands-on:** <br>&emsp; + Wrote `lib/mongoose.ts` to connect to MongoDB <br>&emsp; + Built the Owner model with a unique index on email <br>&emsp; + Configured TypeScript path aliases                                     | 16/06/2026 | 16/06/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 4   | - Built the registration flow: <br>&emsp; + Validated input with express-validator <br>&emsp; + Hashed passwords with bcryptjs <br> - **Hands-on:** <br>&emsp; + Wrote the register controller <br>&emsp; + Built middleware to handle validation errors <br>&emsp; + Tested the API with curl                                                                    | 17/06/2026 | 17/06/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 5   | - Built the login flow and JWT: <br>&emsp; + Short-lived access token <br>&emsp; + Refresh token in an httpOnly cookie <br> - **Hands-on:** <br>&emsp; + Wrote the login controller <br>&emsp; + Wrote `lib/jwt.ts` to centralize token sign/verify functions                                                                                                     | 18/06/2026 | 18/06/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 6   | - Built refresh token, logout, and auth middleware: <br>&emsp; + Stored the refresh token in a Token collection so it could be revoked <br>&emsp; + `authenticate` middleware verifying the Bearer token <br> - **Hands-on:** <br>&emsp; + Wrote the refresh-token and logout routes <br>&emsp; + Configured cookie-parser                                        | 19/06/2026 | 19/06/2026      | <https://github.com/MT-KS-04/smart-menu-api> |
| 7   | - Standardized responses and basic security: <br>&emsp; + Centralized success/error helper functions <br>&emsp; + Added helmet, cors, compression <br> - Aligned the API contract with the frontend team member <br> - **Hands-on:** <br>&emsp; + Wrote the `.env.example` file                                                                                   | 20/06/2026 | 20/06/2026      | <https://github.com/MT-KS-04/smart-menu-fe>  |

### Achievements During Week 7:

- Finalized the architecture and tech stack for the SmartMenu project:
  - Backend: Node.js, TypeScript, Express, MongoDB (Mongoose)
  - Frontend: React 18, Vite, Tailwind, MUI (UI handled by a team member)
  - Reason for choosing MongoDB: menu/order data is flexible, suited to the early stage

- Finished a working backend skeleton with a clear structure:
  - config, controller/v1, router/v1
  - model, middleware
  - lib, utils

- Designed the core collections in MongoDB:
  - Owner, Restaurant
  - Menu, MenuItem
  - Order, Session, Token

- Completed the full Authentication module:
  - Registration with input validation and password hashing via bcryptjs
  - Login and issuing a JWT access token
  - Refresh token stored in an httpOnly cookie, revocable
  - Logout revokes the refresh token

- Built shared components for later modules:
  - `authenticate` middleware verifying the Bearer token
  - Centralized error-handling middleware
  - Standardized success/error response helpers
  - Basic security with helmet, cors, compression

- Aligned the API contract with the frontend on the base URL, token format, and login flow.
