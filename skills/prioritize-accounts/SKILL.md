---
name: prioritize-accounts
description: "Finds the accounts worth going after, with the value proposition to lead with and evidence that is checked for accuracy, filtered for relevance, and cited so you can verify it. Use when the user asks which accounts to work, focus on, prioritize, or go after. Not for one named account."
user-invocable: true
argument-hint: [optional: how many, or a time window]
---

# Prioritize Accounts

Give the user a ranked list of priority accounts with the reason for each. Optional "$ARGUMENTS" can set how many to show or a window ("this week", "last 30 days").

## Examples

- `/syft:prioritize-accounts`
- `/syft:prioritize-accounts top 5`
- `/syft:prioritize-accounts last 30 days`
- "Who should I be reaching out to this week?"
- "Give me my top 5 accounts and why."

## Step 1: Get the list

Call `get_top_priority_accounts`.

- Syft re-prioritizes accounts weekly. The default window (about the last 10 days) covers the latest run. If the user named a window, set `since` and `until`.
- Default `limit` is 20. If the user asked for a number, request that many.
- Fetch one page. Only follow `next_cursor` if the user asks for more.

If the result is empty, say so plainly and suggest widening the window. Do not treat empty as "no accounts are a priority"; it means none were detected in that window.

If the call returns a permission or setup error, relay its message. It says who to contact.

## Step 2: Present the list

Rank by `priority_score` as returned (0 to 100: how real and costly the account's problem is, combined with how completely the user's products solve it; higher is stronger). For each account show:

| # | Account | Score | Why it is a priority | Source |
|---|---|---|---|---|

- **Why it is a priority**: one sentence from `rationale`. Do not paste the whole field.
- **Source**: from `account_source`. `tracked` means the workspace asked Syft to watch it; `syft_recommended` means Syft found it outside the tracked set. Managers and admins may see both.

After the table, for the top 3 accounts, add the strongest `evidence` item: its `reason` (a specific finding about the account and what it means for what the user sells), then the verbatim `quote` that proves it, with `source_url`. Lead with the reason; the quote is the proof.

If the user asked for the value proposition, include it as a column.

## Step 3: Offer next actions

Ask which the user wants:

1. **Go deeper on one account**: pass its `syft_account_id` to `get_account_priority_history` for how its score changed, and `get_account_relevant_context` for recent coverage.
2. **Find people there**: `search_contacts`, passing the account's `account_domain` as `company_domain`. Search is free. Enrichment (`enrich_contacts`) spends credits: name the contacts, get approval, then call with their `syft_contact_ids` and `confirm=true`.
3. **See more accounts**: fetch the next page.
4. **Change the window**: re-run with different `since` and `until`.

## Rules

- Never call `enrich_contacts` without explicit approval for the specific contacts.
- Syft does not know CRM state. If the user wants to exclude customers or open opportunities, ask them or use a connected CRM.
