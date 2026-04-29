# Scenario: No Reply (Unresponsive)

## Context
Vendor was asked for: pricing, certifications, delivery terms, after-sales, company profile, bank account.
Vendor has not responded after the response deadline has passed.

## Email

(No email received)

## Timeline
- Initial outreach sent: 2026-04-15
- Response deadline: 2026-04-29 (14 calendar days)
- Current date: 2026-04-30
- Days overdue: 1

## Expected Behavior — Round 1 (first follow-up)
- No data to extract
- Action: draft a polite follow-up reminder email referencing the original request
- Include: original subject line, restate what was requested, new deadline (7 days)
- Tone: professional, assume the email may have been missed
- outreachStatus: "in_progress"
- outreachRound: 1

## Expected Behavior — Round 2 (second follow-up, if still no reply)
- Action: draft a second follow-up, shorter and more direct
- Include: "This is our second follow-up regarding..."
- New deadline: 5 days
- outreachStatus: "in_progress"
- outreachRound: 2

## Expected Behavior — Round 3 (final attempt)
- Action: draft a final notice
- Include: "This is our final attempt to reach you. If we do not hear back by [date], we will proceed without your participation."
- New deadline: 3 days
- outreachStatus: "in_progress"
- outreachRound: 3

## Expected Behavior — After Round 3 (still no reply)
- Action: NO further follow-up
- outreachStatus: "unresponsive"
- dataComplete: false
- Recommendation: exclude from evaluation or proceed with whatever data was collected during online research
