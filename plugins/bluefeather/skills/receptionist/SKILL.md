---
name: receptionist
description: Set up an AI phone receptionist for a small business (salon, barbershop, clinic, law office, contractor, restaurant, agency) that answers calls, answers common questions, takes messages, and routes urgent calls to a person. Use when someone asks for a receptionist, front desk, answering service, or "something to pick up my phone".
---

# AI receptionist

Follow the build-phone-assistant skill for the mechanics. This skill supplies what a good receptionist needs.

## Ask the owner

- Business name, address, hours, timezone, and how to say the name out loud.
- The top 5 questions callers ask, with the real answers (prices, services, parking, payment, cancellation policy).
- What counts as urgent, and the number to transfer urgent calls to. Outside which hours is transfer not allowed?
- Where messages should go: email (Gmail or Outlook), Slack, a CRM, or a spreadsheet.
- Should it also book appointments? If yes, use the appointment-booker skill for that part.

## Conversation shape

1. **Greeting**: business name and an open question ("Thanks for calling Fade Studio, how can I help?").
2. **Understand the request**: classify into answer-a-question, take-a-message, urgent, or booking.
3. **Answer** from the owner's facts only. If the answer is not in the facts, offer to take a message.
4. **Take a message**: name, callback number (read it back digit by digit), reason. One item per turn.
5. **Urgent**: confirm it is urgent, then transfer to the owner's number during allowed hours; otherwise take a message and say when someone will call back.
6. **Close**: summarize what will happen next and end the call.

## Apps

- Messages by email: connect `gmail` (or `outlook`) and use the send-email action, sending to the owner, not the caller.
- Messages to a team: `slack` send-message to the channel the owner picks.
- Log every call: `googlesheets` add-row or the owner's CRM.
Use `find_app_actions` to get the exact actions; do not guess their names.

## Success criteria

- The caller never waits in silence and always knows what happens next.
- Every message captured has a name, a verified callback number, and a reason.
- Nothing is promised that the owner did not provide.
