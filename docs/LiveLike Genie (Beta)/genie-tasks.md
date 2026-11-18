---
title: Tasks
excerpt: Put recurring work on a schedule.
deprecated: false
hidden: true
metadata:
  robots: index
---
A **Task** is a request Genie runs for you on a schedule. Anything you can ask Genie in chat — create content, pull a report, post to Slack, reset a leaderboard — can become a task.

**Good uses for tasks**

- **Twice-weekly report** — "Every Tuesday and Thursday at 9am New York time, post a video performance update to #engagement in Slack: top videos by views and watch time, and totals versus the week before."
- **Weekly reset** — "Every Monday at 6am, reset the weekly leaderboard and award the top 3 the *Weekly Champ* badge."
- **Pre-game content** — "Every Saturday at noon, create a first-goal prediction for that day's fixture."
- **Monitoring** — "Every hour on match days, check the derby chat room for abusive messages and list them."
- **Monthly report** — "On the 1st of every month, report quest completions by program for the previous month."

## Create a task

Tasks are created in chat, so Genie can work out the plan and check it with you.

1. Go to **Tasks** and click **New Task** (this starts a chat with `/task`), type `/task` in any chat, or simply describe a recurring job.
2. Say **what** should happen and **when**, including the time zone:
   > "/task Every weekday at 9am New York time, list widgets that ended yesterday with fewer than 100 responses and post them to #producers in Slack."
3. If anything is missing, Genie asks — typically the day and time, the time zone, and whether you want to be notified **always**, **only on failure** (the default) or **never**.
4. Genie shows a **plan preview**: the schedule, what happens on each run, the resources it will use (such as a Slack channel), and any choices it made for you.
5. Reply **confirm**. Genie saves the task and replies with its schedule and a **View the plan** link.

![Genie's plan preview for a new task, ending with "Reply confirm to save it, or cancel"](https://files.readme.io/893e4de47dd79fb298372ac21281169ab913e1df2a72d2432413f894829ddac3-08-chat-plan-confirm.jpg)

![After "confirm", Genie saves the task and shows each step it will run](https://files.readme.io/86b9fcab0268e1ee7353256eff1ea8414a2dbbe565504af204820576aeed9630-09-chat-task-saved.jpg)

If the task needs files (for example a spreadsheet of questions), attach them while creating it. They're saved with the task and checked before every run.

> 🚧 **Connectors must be healthy**
> A task can't be created, and won't run, while a connector it uses needs reconnecting. Reconnect it from **Connectors** and the next run goes ahead.

## The Tasks page

**Tasks** lists every scheduled task with its schedule and status (**Active** or **Paused**). Search by name, and use the filter button to sort by **Next Run** or **Status**.

![The Scheduled Tasks list](https://files.readme.io/a3a9e144815b66f0c901030db7595e701ccca2513e072bc470d9b088eeadb886-10-tasks-list.jpg)

Open a task to see everything about it:

![A task's page: description, status, schedule, plan summary and run history](https://files.readme.io/d56f8ff473555eb57ca85f8de7fbd080ae214a7416b534c554b9435abb4384a3-11-task-detail.jpg)

| | |
|---|---|
| **Status and schedule** | Active or Paused, when it runs, and the next run time. Use the pause button beside the status to **pause** or **resume**. |
| **Run Now** | Run it immediately, outside the schedule — the best way to test a new task. |
| **Plan** | A summary of the steps (e.g. *4 steps: LiveLike Analytics ×3, then Slack*) and the resources used. **Runs the saved plan** means every run follows the plan you confirmed. |
| **View plan** | Opens the full plan: each stage, which steps run together, which agent runs each step, and the named resources. |
| **History** | Every run with its time and result. Open a run to read the full conversation of what Genie did. |
| ✏️ **Edit** | Change the name, description and schedule. |
| 🗑 **Delete** | Remove the task and stop all future runs. |

![The plan drawer: stages, steps, agents and named resources](https://files.readme.io/d642dbde700a6fbbac9a783e8eaf0ae325ed3bb3dae1da28063723562838d0a9-12-task-plan.jpg)

## Editing a task

Click ✏️ to open **Edit Task**:

- **Task Name** and **Task Description**
- **Frequency** — **Daily**, **Weekly** (pick the days), **Monthly** (pick the day of the month), **Yearly**, **Interval** (every N minutes or hours), or **Custom (cron)**
- **At** — the time of day, and **Timezone**

Click **Save** to apply.

The **Prompt** is read-only here. To change what the task does, click **Edit in Chat** — Genie re-plans it and re-checks your connectors, so the saved plan always matches the instruction.

![The Edit Task drawer with frequency, days, time and Edit in Chat](https://files.readme.io/c62aacf082adae90a1e5bb6e8489563ccf1bfea90b5c610fd3e2e76d054c17f8-13-task-edit.jpg)

## Managing tasks from chat

You can do everything from the conversation too:

- "List my tasks."
- "Pause the weekly leaderboard reset until further notice."
- "Run the daily recap now."
- "Change the pre-game task to 11am instead of noon."
- "Notify me after every run of the daily recap task."

## Tips

- **Be explicit about time zones.** "9am" is ambiguous for a global audience — say "9am London time".
- **Test with Run Now** before relying on the schedule, then read the run in History.
- **Name resources precisely.** "The *Season 2026* leaderboard" or "#producers in Slack" survives better than "the leaderboard" or "the team channel".
- **Read the "choices I made" list** in the plan preview — it's where Genie tells you what it assumed.
- **Pair tasks with skills.** If every report should follow a format, put that format in a skill — the task will pick it up on every run.
