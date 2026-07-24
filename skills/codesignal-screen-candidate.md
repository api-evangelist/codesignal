---
name: Screen a candidate with a CodeSignal assessment
description: Pick an assessment, send it to a candidate, and collect the graded result.
api: mcp/codesignal-mcp.yml
operations: [list_tests, get_test, create_test_session, resend_test_session, lookup_ats_test_sessions, grade_test_result, mark_test_result_graded]
webhook_events: [companyTestSessionCreated, companyTestSessionStarted, companyTestSessionFinished]
---

# Screen a candidate with a CodeSignal assessment

Use the CodeSignal MCP server (`https://codesignal.com/api/mcp`, `Authorization: Bearer <API key>`).
Timestamps and durations are in milliseconds.

## Steps
1. `list_tests` (optionally `list_test_labels` to filter) to find the assessment; confirm details with `get_test`.
2. `create_test_session` for the candidate (email/name). If the invite needs re-sending, call `resend_test_session`.
3. Wait for the `companyTestSessionFinished` webhook (or poll with `get_test_session` / `lookup_ats_test_sessions` when integrating with an ATS via `externalId`).
4. For manually graded results, call `grade_test_result` then `mark_test_result_graded`.

## Rules
- Write tools modify live production data — confirm the candidate and test before creating a session.
- Verify inbound webhooks with the `X-CodeSignal-Signature` HMAC-SHA256 header (see conventions/codesignal-conventions.yml).
- Handle 401 by refreshing/rotating the API key; keys carry granular permissions.
