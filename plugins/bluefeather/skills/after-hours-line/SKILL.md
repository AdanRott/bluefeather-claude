---
name: after-hours-line
description: Build a phone assistant that covers calls outside business hours or when staff are busy, handles true emergencies by reaching the on-call person, and turns everything else into a clear message or next-morning booking. Use for after-hours, overflow, weekend, holiday, on-call, or emergency lines (plumbers, HVAC, property managers, clinics, vets, IT support).
---

# After-hours line

Follow the build-phone-assistant skill for the mechanics.

## Ask the owner

- What is a real emergency for this business, with examples, and what is not (for example a burst pipe is, a dripping tap is not).
- The on-call number for emergencies, and whether to transfer the call or send an urgent text or email instead.
- What to tell non-urgent callers about when they will hear back.
- Where messages go first thing in the morning (email, Slack, CRM, a sheet), and whether the assistant may book a next-day slot (see appointment-booker).

## Conversation shape

1. Greeting that says the office is closed and that the caller can still get help now.
2. Ask what is going on, then decide: emergency or not, using the owner's examples only.
3. **Emergency**: collect name, callback number (read back), and address if relevant, then transfer to on-call or send the urgent alert. Tell the caller exactly what happens next.
4. **Not urgent**: take a message or book a next-day slot, and say when they will hear back.
5. Close with a short summary.

## Rules

- When unsure whether something is an emergency, ask one clarifying question; if still unsure, treat it as urgent.
- If someone describes danger to life or safety, tell them to call 911 first.
- Never promise a technician arrival time the owner did not authorize.
