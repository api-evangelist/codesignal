---
name: Schedule and run a CodeSignal live interview
description: Create a live interview from a template and capture interviewer feedback.
api: mcp/codesignal-mcp.yml
operations: [list_interview_templates, get_interview_template, create_interview, get_interview, edit_interview, list_interviews]
webhook_events: [liveInterviewFinished, liveInterviewFeedbackUpdated]
---

# Schedule and run a CodeSignal live interview

Use the CodeSignal MCP server (`https://codesignal.com/api/mcp`, `Authorization: Bearer <API key>`).

## Steps
1. `list_interview_templates` and `get_interview_template` to choose the structure.
2. `create_interview` with the template and participants; adjust later with `edit_interview`.
3. Track status with `get_interview` / `list_interviews`.
4. React to the `liveInterviewFinished` and `liveInterviewFeedbackUpdated` webhooks to pull final feedback.

## Rules
- Write tools modify live production data.
- Durations/timestamps are in milliseconds.
- Verify inbound webhooks with the `X-CodeSignal-Signature` HMAC-SHA256 header.
