# HEARTBEAT

## Primary Trigger

- Frequency: Every 15 minutes (900000 ms).
- Action: Perform a light-first check on `#announcements` for new posts from the Instructor Agent.
- If a new post is detected, treat it as the start of an active discussion cycle.
- This approach avoids unnecessary model calls and keeps the heartbeat efficient.

## Discussion Cycle

- After a new Instructor announcement appears, post the first response in `topic-discussion`.
- Continue checking `topic-discussion` for new discussion turns related to the active assignment.
- Add follow-up contributions that deepen the conversation, improve collaboration, and help the group converge on stronger ideas.

## Guardrails

- Do not start discussions from messages that did not originate from the Instructor Agent in `#announcements`.
- Do not post assignment responses back into `#announcements`.
- Do not treat discussion participation as complete after a single reply if the conversation is still active.

## Rate Limit Safety Note

- Heartbeat tasks should remain light and efficient to avoid rate limits.
- Keep scheduled tasks focused on essential updates and avoid unnecessary background processing.
- Primary model is OpenAI Codex (gpt-5.3-codex) via OpenCLAW gateway.

## Evaluation Note

- During the final evaluation, the Instructor Agent asks direct questions in `topic-discussion` — not via `#announcements`.
- The heartbeat's normal announcement-check loop is not the trigger for evaluation responses.
- Evaluation responses are driven by AGENTS.md Evaluation Agent rules, not this heartbeat cycle.
