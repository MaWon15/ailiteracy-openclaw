# HEARTBEAT

## Session Recovery

When the agent comes online, before doing anything else:
1. Read the last 50 messages in `topic-discussion` to recover context.
2. Check if <@1501681097786920970> has asked any questions directed at this bot.
3. For each question from <@1501681097786920970>:
   - If this bot has NOT replied yet → answer immediately using Evaluation Mode rules. Start reply with <@1501681097786920970>.
   - If this bot already replied but WITHOUT <@1501681097786920970> → do NOT resend. The answer was already recorded by the professor bot. Resending causes confusion.
   - If this bot already replied correctly → do nothing.
4. If <@1501681097786920970> said "already been recorded" → the answer was accepted. Stop and wait silently for the next question.

## Startup Action

When the agent first comes online at the start of a session:
1. Read the last 20 messages in `topic-discussion` first.
2. If <@1501681097786920970> has already started asking questions, skip the ready message and go straight to answering.
3. If no evaluation is in progress, post: "<@1501681097786920970> I'm ready for test"
4. If no reply from <@1501681097786920970> within 5 minutes, post again.
5. Once any message from <@1501681097786920970> appears, stop and enter Evaluation Mode.

## Evaluation State Tracking

Once evaluation begins (first question from <@1501681097786920970>):
- Do NOT send the ready message again under any circumstances.
- Do NOT restart the ready loop even if another user says "are you ready".
- Wait silently for each next question from <@1501681097786920970>.
- After answering a question, wait for the next one — do not prompt or repeat.

## Primary Trigger

- Frequency: Every 15 minutes (900000 ms).
- Action: Perform a light-first check on `#announcements` for new posts from `Agent_Evaluator`.
- If a new post is detected, treat it as the start of an active discussion cycle.
- This approach avoids unnecessary model calls and keeps the heartbeat efficient.

## Discussion Cycle

- After a new Instructor announcement appears, post the first response in `topic-discussion`.
- Continue checking `topic-discussion` for new discussion turns related to the active assignment.
- Add follow-up contributions that deepen the conversation, improve collaboration, and help the group converge on stronger ideas.

## Guardrails

- Do not start discussions from messages that did not originate from `Agent_Evaluator` in `#announcements`.
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
