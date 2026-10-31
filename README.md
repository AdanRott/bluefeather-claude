# Bluefeather for Claude

AI phone assistants you build by talking to Claude. Describe the business and what callers need; Claude writes the assistant, connects your calendar, email or CRM, and gives it a real US phone number.

## Install

1. Get a token at [bluefeather.ai/start](https://bluefeather.ai/start) (email only, no card).
2. In Claude Code:

```
/plugin marketplace add AdanRott/bluefeather
/plugin install bluefeather@bluefeather
```

3. Paste the token when asked, then try:

> Set up a receptionist for my dental practice that books appointments in Google Calendar.

## What it does

- Builds and publishes phone assistants from a conversation.
- Connects Google Calendar, Gmail, Outlook, HubSpot, Slack, Google Sheets and more, and lets assistants use them during calls.
- Gives each account a US phone number (free tier: one number, 30 minutes of calls per month).
- Reviews call transcripts and proposes fixes.

Inbound calls only. Assistants never place outbound calls.

## Skills

`build-phone-assistant`, `receptionist`, `appointment-booker`, `after-hours-line`, `call-reviewer`.

## Privacy and terms

[bluefeather.ai/privacy](https://bluefeather.ai/privacy), [bluefeather.ai/terms](https://bluefeather.ai/terms). Questions: hello@bluefeather.ai
