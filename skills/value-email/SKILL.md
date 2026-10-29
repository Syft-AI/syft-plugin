---
name: value-email
description: "Writes a recommended value-focused cold email for one priority account from Syft's evidence: an observation about the account, the challenge it implies, how the user's products solve it, a customer story, and a soft ask. Use when the user asks to write, draft, or suggest an email, outreach, or first touch for a named account Syft rates a priority. Not for follow-ups, replies, or sequences of several steps."
user-invocable: true
argument-hint: [account name or domain]
---

# Value Email

Write one value-focused cold email for the account in "$ARGUMENTS" (or the one the user named), grounded in Syft's evidence. The user sends it; never send it.

## Examples

- `/syft:value-email Acme`
- "Write an email to Acme based on why they are a priority."
- "Draft outreach for the top account on my list."

## Step 1: Get the account's evidence

Call `get_top_priority_accounts` with `since` 90 days ago and `limit` 100, and find the account by name or domain. Follow `next_cursor` until you find it or the pages run out. If the user did not name an account, ask which one, or offer their top accounts.

If the account is not in the results, say Syft has no current priority evidence for it and that the email needs that evidence. Stop there.

Keep the account's `rationale`, `value_proposition`, and every `evidence` item (`reason`, `quote`, `source_type`, `source_url`). If the user picked one evidence item, use it as the observation.

## Step 2: Get products and customer stories

Call `get_workspace_setup` with `include` set to `products` and `customer_stories`.

If it returns an admin-only error, continue without it: use `value_proposition` for what we solve, and skip the customer story unless the user gives one. Tell the user once that a workspace admin's setup adds customer stories.

## Step 3: Write the email

Write it to this brief. Treat the rationale and evidence as the research.

<!-- Do not edit this brief without rerunning the value-email eval (syft-plugin-private, value-email-eval/). -->

> Write a short, value-focused cold email from the research, products, and customer stories given. Invent nothing.
>
> No greeting. One sentence each, blank line between: an observation from the research (source mentioned casually, quote only unique phrases), a specific non-obvious challenge it implies, how we solve it (value first, no product names), the best-fitting customer story if any, and a soft question like "Is this worth exploring?" No colons or dashes. Under 110 words.
>
> Output "Subject: <3-5 words>", a blank line, then the body.

## Step 4: Present it

Show the subject and body in one block the user can copy. Below it, list what the email rests on so the user can check it: the evidence quote with its `source_url`, and the customer story used, if any.

Then offer:

1. **Another angle**: rewrite it from a different evidence item.
2. **Find people there**: `search_contacts` with the account's `account_domain`. Enrichment (`enrich_contacts`) spends credits: name the contacts, get approval, then call with `confirm=true`.
3. **Put it in a sequence**, if a sequencer is connected. Ask before creating anything.

## Rules

- Every fact in the email must come from the evidence, products, or customer stories. Never add metrics, names, or dates.
- Never call `enrich_contacts` without explicit approval for the specific contacts.
