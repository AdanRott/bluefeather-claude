---
name: build-phone-assistant
description: Build, change, connect, and publish a Bluefeather AI phone assistant that answers or makes real phone calls. Use whenever someone wants a voice agent, AI receptionist, phone bot, call automation, or wants an existing assistant to do something new during calls (book appointments, look things up, update a CRM, send emails). The recipe skills (receptionist, appointment-booker, after-hours-line) build on this one. Bluefeather assistants answer inbound calls only.
---

# Build a phone assistant

Bluefeather assistants run live phone conversations: they listen, decide, speak, and can use the customer's connected apps mid-call. You build them through the `bluefeather` MCP tools. Work in four stages and keep the customer involved, because only they know their business rules.

## 1. Plan with the customer

1. Call `get_voice_prompting_guide` with `stage: "plan"` and follow it.
2. Ask the customer, a few questions at a time:
   - Business name, what callers usually want, opening hours, timezone.
   - The call's single goal and what counts as success.
   - What the assistant must collect (name, phone, reason, date...) and what it must never do.
   - When to hand off to a human, and to which number.
   - What should happen after the call (email a summary, add to CRM, book in calendar).
3. Propose a short plan: persona, the ordered conversation steps, how the call can end, and which apps it needs. Keep the first version small. Get a yes before writing anything.

## 2. Connect the apps it needs

1. `list_connected_apps` to see what is already connected.
2. For each missing app, `connect_app` and give the customer the link. Links expire within minutes, so create the link right when they are ready, and make a new one if they report an expired link.
3. `find_app_actions` with a plain-English use case ("find free slots and book an appointment in Google Calendar"). Note the action identifiers and their app.
4. Use `run_app_action` for read-only lookups the assistant will need, such as the calendar id or a CRM pipeline name. Never run actions that change the customer's data just to test.

## 3. Write the assistant

1. Call `get_voice_prompting_guide` with `stage: "create"`, and with `topic: "common_guidelines"` before writing the global step.
2. `list_node_types`, then `get_node_type` for every step type you use (`startCall`, `agentNode`, `endCall`, `globalNode`, `webhook`).
3. If the assistant uses apps during the call, it needs an id first: create the assistant, then call `give_assistant_app_actions` with its id and the actions, and add the returned `tool_uuid` to the `tool_uuids` of each step that uses them.
4. Write the code with `@bluefeather/sdk` and call `create_assistant`. On `created: false`, read `error_code` and `error`, fix the whole source, and resubmit.
5. Later edits: `get_assistant_code`, change it, `save_assistant_draft`. Drafts do not affect live calls.

Prompt rules that matter most on the phone:
- One question per turn, and every turn ends with a question or a clear nudge.
- Spell out exactly when each tool fires ("only after the caller confirms the time").
- Say dates, times, and numbers the way a person would speak them.
- Include the timezone in every calendar action.
- Never invent availability, prices, or policies; use an action or say a person will follow up.

## 4. Review, publish, test

1. `get_voice_prompting_guide` with `stage: "review"`; fix what it flags.
2. `publish_assistant` once the customer approves. Callers get the new version only after publishing.
3. `get_phone_number` with the assistant id (and a preferred area code if the customer has one). The free tier includes one US number per account; calling it again with another assistant id moves the number. Tell the customer the number and ask them to call it.
4. `get_usage` shows minutes used against the monthly included minutes. When the account is over, the number stops answering until next month; say so plainly if calls stop.
5. After real calls, use the call-reviewer skill to improve it.

## When something fails

- A tool error that names an app or connection: the app is probably not connected or the connection expired. Run `list_connected_apps` and reconnect.
- `validation_error` or `graph_validation` from create/save: re-read the node type with `get_node_type` and fix the field it names.
- Do not make up identifiers: action names come from `find_app_actions`, assistant ids from `list_assistants`.
