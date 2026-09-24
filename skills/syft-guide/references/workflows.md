# Workflows

Plays that combine Syft with the user's other tools. Each is a starting point; adapt to what is connected and to what the user wants. Tool names in backticks are Syft MCP tools. Other steps use whatever CRM, sequencer, or data source the host has available.

Each play has a goal and a suggested cadence. Cadences are recommendations; the user sets their own.

## Account in play

Goal: bring Syft's evidence into work the user is already doing on one account.
When: any time the user is preparing outreach, a call, or a deal review for a named company, if they want it.

1. `search_accounts` by name or domain to get its `syft_account_id`.
2. `get_account_priority_history` for the current score and how it changed.
3. `get_account_relevant_context` for recent coverage (default 7 days; widen to 30 if empty).
4. Use the rationale, value proposition, and evidence as context for the task. If there is no score, say so and continue without it.

## Outbound

### Weekly prioritization

Goal: a short list of accounts to work this week, with the reason for each.
When: weekly, after Syft's run.

Run `prioritize-accounts`. If a CRM is connected, mention which accounts are customers or have an open opportunity; leave them in the list unless the user wants them out.

### Load priority accounts into sequences

Goal: get priority accounts and the right contacts into outreach with the value proposition already in the message.
When: weekly, after prioritization.

1. `get_top_priority_accounts` for the window the user wants.
2. If a CRM is connected, note which accounts are customers or have open opportunities. Ask the user whether to include them.
3. If other data is connected (ABM, intent, website traffic, inbound), pull it for the accounts and use it to sharpen the value proposition. Where it disagrees with Syft's evidence, say so.
4. Find contacts. Use the recommended buyer titles from the account's priority history to pick titles. Suggest a connected contact provider first; fall back to `search_contacts`. Enrich only with approval (`enrich_contacts`, `confirm=true`).
5. Route to sequences. With several sequences, sort accounts into the one that matches their value proposition, rationale, or product (if products are visible). Example: three sequences that all open with the value message, then diverge by product or value proposition; the assistant routes each account and its contacts to the right one. Fill custom variables per contact from the rationale and value proposition where the sequencer supports them.
6. If no suitable sequence exists, ask whether to create one (see below).
7. Recommend tagging created records "syft" for attribution. Optionally brainstorm with the user what the next automated step could be.

### Create a value sequence

Goal: a sequence whose first touch leads with the account's value proposition and cites one piece of evidence.
When: once per value proposition or product; reuse after.

Draft the steps, keep claims to what the evidence supports, get approval, then create it in the sequencer.

### Populate the CRM

Goal: every priority account exists in the CRM so activity is tracked.
When: weekly, or on demand.

For each priority account, check whether it exists in the CRM and offer to create it if not. Recommend the "syft" tag. Do not create contacts without approval if creation triggers enrichment.

## Pipeline

### Revive churned and stalled

Goal: re-open conversations where new evidence gives a reason to return.
When: weekly or biweekly.

1. `get_top_priority_accounts`.
2. For each, search the CRM for a closed-lost, churned, or stalled opportunity.
3. If found, pull the contacts on that opportunity and any call transcripts. Look for a way the new evidence solves a problem they raised.
4. Draft a re-engagement note for approval.

### Alert on active opportunities

Goal: tell the rep when an open deal has new evidence.
When: weekly, or on each Syft run.

1. Pull active opportunities from the CRM.
2. Match by domain against `get_top_priority_accounts`.
3. For matches, tell the user which open deals have new evidence and what it says.

## Analysis

### Compare opportunities to priority accounts

Goal: learn how many opportunities Syft flagged first, and how early.
When: weekly or monthly. Limit to opportunities created in the last one to two weeks unless the user wants a longer look.

1. Pull the opportunity list from the CRM for the period.
2. For each opportunity, `search_accounts` by domain to get its `syft_account_id`, then `get_account_priority_history`. This is one call per opportunity and cheaper than paging through the whole priority list.
3. Compare the earliest `detected_at` in the history with the opportunity's created date.
4. Report: how many opportunities were priority accounts first, how many were not, and any common themes.

### Analyze priority accounts by theme

Goal: find what reasons and value propositions recur, to improve messaging and targeting.
When: monthly, quarterly, or when building a territory plan.

1. `get_top_priority_accounts` for the period. This can take several pages; ask before paging through many.
2. Group by rationale, value proposition, and evidence themes.
3. Report the most common reasons accounts are a priority, and what that suggests for messaging and targeting.
