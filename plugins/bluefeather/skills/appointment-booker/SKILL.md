---
name: appointment-booker
description: Build a phone assistant that checks real availability and books, moves, or cancels appointments in the business's calendar (Google Calendar, Outlook, Calendly, Cal.com) during the call, then confirms by email. Use for bookings, scheduling, reservations, consultations, and appointment lines.
---

# Appointment booker

Follow the build-phone-assistant skill for the mechanics. This skill covers the booking logic.

## Ask the owner

- Which calendar holds bookings (connect `googlecalendar`, `outlook`, `calendly`, or `cal` via `connect_app`), and the calendar id if there are several (`run_app_action` with the list-calendars action to find it).
- Services, the length of each, buffer time between appointments, and the booking window (for example, at least 2 hours ahead and at most 30 days ahead).
- Opening hours and timezone. Callers in another timezone must hear times in the business's timezone.
- What to collect: name, phone, email (for confirmation), service, any notes.
- Policies to mention: cancellation, deposits, late arrivals.

## Conversation shape

1. Greeting, then ask which service.
2. Ask for a preferred day, then check free slots with the find-free-slots action. Offer at most two or three times, spoken naturally ("Tuesday at three, or Wednesday at ten thirty?").
3. Collect name, then phone number (read it back), then email if a confirmation is wanted (spell it back).
4. Read the full booking back and ask for a clear yes.
5. Only after that yes, create the event with the service and caller details in the title and description. If creation fails, apologize, offer another time once, and otherwise take a message.
6. Send the confirmation email if the owner wants one, then close.

For changes and cancellations, find the existing event by the caller's name and date first, confirm it is theirs, then patch or delete it.

## Rules

- Never say a time is available without checking it during this call.
- Never create an event before the caller says yes to the read-back.
- Always pass the timezone in calendar actions.
- One question per turn.
