---
title: "Week 9 Worklog"
date: 2026-06-29
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Goals:

- Build a versioned Menu module (draft → published → archived).
- Build CRUD for menu items (MenuItem) with category, price, and status.
- Build allergen tagging based on the EU's 14-category standard.
- In parallel: configure S3 and Lambda to prepare for deploying the project on AWS.

### Activities Implemented During the Week:

| Day | Activities                                                                                                                                                                                                                                                                                                                                       | Start Date | Completion Date | Reference                                                                  |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | -------------------------------------------------------------------------- |
| 2   | - Designed the menu lifecycle: <br>&emsp; + `draft` → `published` → `archived` <br>&emsp; + Only one published menu per restaurant <br> - Designed the Menu model: name, imageUrl, status, version                                                                                                                                               | 29/06/2026 | 29/06/2026      | <https://github.com/MT-KS-04/smart-menu-api>                               |
| 3   | - Built menu creation and publishing: <br>&emsp; + `POST /menus/upload` creates a draft menu <br>&emsp; + `POST /menus/:id/publish` auto-archives the old menu <br> - **Hands-on:** <br>&emsp; + Handled the constraint of only one published menu at a time                                                                                     | 30/06/2026 | 30/06/2026      | <https://github.com/MT-KS-04/smart-menu-api>                               |
| 4   | - Built CRUD for menu and menu items: <br>&emsp; + `GET /menus`, `PATCH`, `DELETE` <br>&emsp; + MenuItem model: nameVi, price, category, descVi, status <br> - **Hands-on:** <br>&emsp; + Wrote `POST /menus/:id/items` and `GET /menus/:id/items`                                                                                               | 01/07/2026 | 01/07/2026      | <https://github.com/MT-KS-04/smart-menu-api>                               |
| 5   | - Completed editing/deleting menu items: <br>&emsp; + Changed price, status (available / sold_out) <br>&emsp; + Added sample data for the frontend to test rendering <br> - **AWS:** <br>&emsp; + Created an S3 bucket to hold the frontend build <br>&emsp; + Configured an IAM policy granting S3 access                                       | 02/07/2026 | 02/07/2026      | <https://000057.awsstudygroup.com> <br> <https://000002.awsstudygroup.com> |
| 6   | - Built allergen tagging: <br>&emsp; + Finalized the 14 EU-standard allergen categories into constants <br>&emsp; + Levels: contains / may_contain <br>&emsp; + `verified` flag (confirmed by owner) <br> - **Hands-on:** <br>&emsp; + Wrote `PATCH /menus/:id/items/:itemId/allergens`                                                          | 03/07/2026 | 03/07/2026      | <https://github.com/MT-KS-04/smart-menu-api>                               |
| 7   | - Reviewed validation and fixed bugs: <br>&emsp; + Non-negative price, non-empty category <br>&emsp; + Allergens must be within the 14 allowed categories <br>&emsp; + Handled orphaned items when a menu is deleted <br> - **AWS:** <br>&emsp; + Trial-deployed the backend via Lambda Function URL <br>&emsp; + Verified the API worked on AWS | 04/07/2026 | 04/07/2026      | <https://000022.awsstudygroup.com>                                         |

### Achievements During Week 9:

- Completed the Menu module with version management:
  - A clear lifecycle: draft (being edited) → published (visible to guests) → archived (old menu)
  - Publishing a new menu automatically archives the currently published one
  - Ensured the constraint of only one published menu at a time
  - Old menus are preserved rather than overwritten

- Completed CRUD for menu items (MenuItem):
  - Add, edit, delete items
  - Managed by name, price, category, description
  - Toggled status between available / sold_out

- Completed allergen tagging:
  - Standardized the 14 EU-standard allergen categories into shared constants
  - Distinguished levels: contains and may_contain
  - `verified` flag for owner confirmation
  - Constraint: allergens must be within the allowed list

- Gained experience working with MongoDB:
  - No foreign-key constraints like SQL, so relationships must be cleaned up manually on delete
  - Extracted shared data into constants to keep the frontend and backend consistent

- Made initial progress deploying the project on AWS:
  - Created an S3 bucket to hold the frontend build
  - Configured an IAM policy granting S3 access (`s3:ListBucket` on the bucket ARN, object-level actions on the `/*` ARN)
  - Trial-deployed the backend via Lambda Function URL and verified the API worked
