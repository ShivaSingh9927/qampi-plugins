---
name: qampi-outreach
description: Use when the user wants to find LinkedIn prospects, add leads to Qampi, build or launch a Qampi campaign, or check how a campaign is doing (who connected, who replied).
---

# LinkedIn outreach with Qampi

Qampi runs LinkedIn outreach from the user's own LinkedIn account. Every action
reaches a real person under the user's name, so work in this order and never
skip the confirmation step.

## 1. Check the account first

Call `qampi_status` before planning anything. It tells you:

- whether LinkedIn is connected and healthy. If not, stop and tell the user to
  reconnect in the Qampi app; no other tool will work.
- today's remaining budget for invitations, messages and searches. The
  invitation allowance grows with the account's age and acceptance rate, so
  plan around the number it returns, not a fixed one.
- the mode. In `read-only` mode you can only look. If the user asks you to add
  leads or run a campaign, tell them to switch the plugin's mode to `full`.

## 2. Find people carefully

`qampi_search_people` uses up one search from a monthly allowance. Build one
precise query (title, company, location) instead of several broad ones, and
show the user the results before adding anyone.

## 3. Add leads and build the campaign

- `qampi_add_leads` and `qampi_enroll_leads` contact nobody. They are safe to
  run once the user has agreed on the list.
- Campaigns are created from templates. Call `qampi_list_templates` and pick
  the one that fits the user's goal. Explain in plain words what it will do,
  for example "visits their profile, invites them, then messages them two days
  after they accept".
- A new campaign starts as a draft.

## 4. Launch only on an explicit yes

`qampi_launch_campaign` starts real outreach and cannot be undone: a sent
invitation can't be taken back, and a withdrawn one can't be re-sent for three
weeks. Before calling it, tell the user:

- the campaign name and template,
- how many people it will reach,
- what the first action is.

Then wait for a clear yes in this conversation. Pass `confirm: true` only after
that. Don't treat a general request earlier on ("set it all up") as the yes.

Qampi still enforces its own daily limits and pacing after launch, so a launch
spreads over days. Tell the user that, so they don't expect everything to
happen at once.

## 5. Report results

Use `qampi_get_campaign` and `qampi_campaign_leads` to report progress. Lead
with what the user cares about: who accepted, who replied, and anything that
failed or is stuck. Replies belong to the user to answer; don't draft or send a
reply unless they ask.
