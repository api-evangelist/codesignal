---
name: Track organization learning progress via the Learn API
description: Read organization members, their skill sets, and their learning progress from the CodeSignal Learn Public API.
api: openapi/codesignal-learn-openapi.json
operations:
  - GET /api/v1/organizations/members
  - GET /api/v1/organizations/members/{memberId}
  - GET /api/v1/organizations/members/skill-sets
  - GET /api/v1/organizations/members/progress
  - GET /api/v1/organizations/members/{memberId}/progress
---

# Track organization learning progress

Uses the CodeSignal Learn Public API (base `https://codesignal.com/learn`).

## Auth
1. Get an OAuth 2.0 access token via client credentials:
   `POST https://codesignal.com/learn/api/v1/oauth/token` with the `openid` scope.
2. Send it as `Authorization: Bearer <access_token>`.

## Steps
1. `GET /api/v1/organizations/members` — page through the roster with `page` / `per_page`, optionally `search` / `role` / `sort_by` / `sort_order`.
2. `GET /api/v1/organizations/members/{memberId}` — a single member.
3. `GET /api/v1/organizations/members/skill-sets` — skill sets (filter by `member_id`).
4. `GET /api/v1/organizations/members/progress` (all) or `GET /api/v1/organizations/members/{memberId}/progress` (one) — learning progress.

## Rules
- Pagination is page-number based (`page`, `per_page`).
- Handle `400` (bad parameters) and `401` (missing/expired token) responses.
