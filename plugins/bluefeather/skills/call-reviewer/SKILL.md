---
name: call-reviewer
description: Review a Bluefeather phone assistant's recent calls and transcripts, find where callers got stuck, confused, or dropped off, and propose and apply concrete prompt fixes as a draft. Use when someone asks how their phone assistant is doing, why calls fail, for call summaries or analytics, or to improve an assistant.
---

# Call reviewer

## Gather

1. `list_assistants` and confirm which assistant to review.
2. `list_calls` for it, newest first. Skip very short calls unless the owner asks about hang-ups; look at 10 to 20 calls.
3. `get_call_transcript` for each call worth reading.

## Look for

- Calls that ended without reaching the goal, and the turn where it went wrong.
- Questions the assistant could not answer, and answers it made up.
- Repeated questions, long monologues, talking over the caller, or silence after a tool call.
- App actions that failed or fired at the wrong moment.
- Callers asking for things the assistant was not built for, which may be worth adding.

## Report

Give the owner a short summary: number of calls reviewed, how many reached the goal, the top three problems each with a one-line quote from a transcript, and a fix for each. Never invent numbers; count only the calls you read.

## Fix

With the owner's approval, follow the review stage of the build-phone-assistant skill: `get_assistant_code`, change only what the fixes need, `save_assistant_draft`, and `publish_assistant` once the owner says yes.
