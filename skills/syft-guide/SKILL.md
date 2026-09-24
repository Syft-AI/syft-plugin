---
name: syft-guide
description: "How to get the most from Syft in a connected sales stack: getting started, and which parts of the user's routine Syft can automate with their CRM, sequencer, and other tools. Use when the user has just connected Syft, asks how to use it or what they can do with it, or when a Syft request could be taken further with a connected system."
user-invocable: true
argument-hint: [optional: what you are trying to do]
---

# Syft Guide

Goal: help the user get the most value from Syft inside their connected ecosystem, automating as much of the rep's sales routine as makes sense while keeping results good. This skill notices when a workflow could go further and offers the play; the plays live in `references/workflows.md`, and what each connected tool adds is in `references/connected-systems.md`.

Syft finds priority accounts, each with a score, a rationale, the value proposition to lead with, and evidence that is checked for accuracy, filtered for relevance, and cited so you can verify it. Reps see their territory. Managers and admins see the whole workspace, including accounts nobody is tracking yet.

## Getting started

1. Call `whoami` once to confirm the user is connected and learn their role.
2. If the workspace returns a setup or permission error, relay the message; it says who to contact.
3. Offer three things to try:
   - "Who should I be reaching out to this week?" (runs `prioritize-accounts`)
   - "Is [company] worth my time right now?"
   - "Give me my top 5 accounts and why."
4. Ask what else is connected (CRM, sequencer, call recordings, contact provider). That decides which plays are available.

## When to offer a play

Watch for these and suggest the matching play from `references/workflows.md`. Suggest, do not assume; the user decides.

| Signal | Offer |
|---|---|
| User just got a priority list and has a sequencer connected | Load the accounts into a sequence, sorted by value proposition |
| User has a CRM connected | Create or tag the accounts; check for stalled or churned opportunities to revive; alert on open deals with new evidence |
| User is preparing outreach or a call for a named account | Pull its priority history and relevant context to inform the message |
| User is a manager reviewing pipeline or messaging | Compare opportunities to priority accounts; analyze priority accounts by theme |
| User asks what to connect | `references/connected-systems.md` |

Offer one play at a time and say what it would automate. If the user has a better idea, go with theirs.

## Guardrails

- Read-only tools can run without asking. `enrich_contacts` spends credits: name the contacts, get approval, then call with `confirm=true`.
- Suggest a connected contact provider before Syft enrichment when one is available.
- Syft does not know CRM state. Offer to filter customers and open opportunities through the CRM; do not filter unless the user wants it.
- Recommend tagging records created from Syft data as "syft" for attribution. Do not tag without asking.
- If a tool fails with an auth error, call `whoami` and relay what it says.
