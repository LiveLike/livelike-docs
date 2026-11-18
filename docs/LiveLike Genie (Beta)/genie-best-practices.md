---
title: Getting the best out of Genie
excerpt: How to write requests, combine features and work safely.
deprecated: false
hidden: true
metadata:
  robots: index
---
## Write requests like a brief

Genie does best with the same information you'd give a producer.

| Instead of | Try |
|---|---|
| "Make a poll." | "Create a text poll in the *Saturday Derby* program: 'Who scores first?' — Home, Away, No goal. Schedule it for kick-off at 3pm UK time." |
| "How are quests doing?" | "Show quest completion rate per quest for the last 14 days, highest first." |
| "Send the results to the team." | "Post the top 3 poll results to #matchday in Slack." |

**Include:** the program or resource by name · the exact copy or options · timing with a time zone · where results should go.

## Name things precisely

Refer to programs, leaderboards and quests by their exact titles (or IDs). If several resources share a name, Genie will ask — but being specific saves a round trip.

## Bring your source material

Have a run-sheet, question bank or reward list? **Attach it.** "Create a quiz widget for each row in this CSV" is faster and more accurate than pasting it in.

## Do big jobs in one request

Genie plans multi-step work and runs independent steps in parallel. Ask for the whole job:

> "For Saturday's derby: create the program, add a first-goal prediction and two halftime polls, link it to the season leaderboard, and create a match chat room."

Review the plan, adjust anything ("make the polls image polls"), then reply **confirm**.

## Build up from chat → skill → task

1. **Chat** — do the job once in conversation and refine it until it's right.
2. **Skill** — capture the rules you had to repeat ("always name it…", "always include a badge…") as a [skill](/docs/genie-skills).
3. **Task** — if it recurs, make it a [task](/docs/genie-tasks). It will follow your skills on every run.

## Let Genie check before it changes

- Read the plan preview before replying **confirm** — it lists the steps, the resources used and the choices Genie made for you.
- For bulk or destructive changes, ask for a dry run first: "List the widgets you'd delete, but don't delete them yet."
- Ask "Who am I?" if you work across several applications, before making changes.

## Ask about the data, not the database

You don't need to know table names. Ask a business question — "Which programs had the most poll votes per viewer last month?" — and Genie's Analytics agent finds the data, runs the query and explains the result. Ask follow-ups to slice it differently.

## Troubleshooting

| Symptom | What to do |
|---|---|
| Genie can't see your programs, widgets or connectors | Open the account menu (your name, bottom-left) → **Access Token** and check the application, then ask "Who am I?" to confirm. |
| A connector shows a warning | Open it and **Reconnect** (OAuth) or **Reconfigure** (API key). |
| A task run is **Failed** or **Partial** | Open the run from **History** to read the transcript; fix the cause, then use **Run Now**. |
| A skill isn't being applied | Check it's in **Installed Skills**. Make its description name the situations it's for, or apply it directly with **＋ → Add Skill**. |
| A request goes to the wrong agent | Pick the agent with `/` (e.g. `/widget`), or check you haven't left **Standalone** mode on in Preview Settings. |
| An answer is wrong or unhelpful | Reply with the correction, and use the feedback buttons so the team can improve it. |
