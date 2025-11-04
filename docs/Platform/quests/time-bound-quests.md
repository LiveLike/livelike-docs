---
title: Time Bound Quests
excerpt: ''
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## What are Time Bound Quests?

Time-bound quests refer to quests that are constrained by a defined time duration, whether in terms of days elapsed or specific calendar dates. Any quest with a temporal limitation falls under the category of time-bound quests.

## Types of Time Bound Quests

1. **No Time Limit**: This option is utilized when there is no requirement for the quest to adhere to a specific start or end time. It is ideal for scenarios where quests can be undertaken without any time constraints or deadlines.

2. **Scheduled Start/End**: This feature enables the scheduling of quest start and end times, ensuring participants are informed about the commencement and conclusion of the event. For instance, it can be employed for events such as holiday specials, which may begin on a designated date, such as December 24th, and conclude on January 5th.
   1. You can configure a quest to commence on a **specified start date without defining an end date.**
   2. Alternatively, you can set **both start and end dates** to delineate the duration of the quest.
   3. Another option is to **specify an end date** for the quest **while omitting the start date**. In such cases, the start date defaults to the current date and time at the moment of quest creation.

3. **User-Specific Timer**: This functionality allows administrators or moderators to establish precise time constraints for individual quests. The flexibility of this feature permits the specification of durations in various units such as seconds, minutes, days, weeks, months, or years, depending on the complexity and nature of the task at hand

For instance, in a gaming environment or an educational platform, administrators can leverage this feature to customize time limits based on the specific requirements of quests or assignments. This functionality allows for the setting of timers ranging from a few hours for short challenges, to several days for more intricate missions, or even several months for extensive, long-term projects. Such adaptability ensures that quests or tasks can be tailored to accommodate diverse objectives and the unique needs of players or users.

## How to Configure Time Bound Quests Using CMS

1. Head to your Application on the [Producer Site](https://cf-blast.livelikecdn.com/producer/)
2. Select **"Quests"** from the sidebar menu
3. Click on the **"New Quest"** Button
4. Set the Quest name, Description, and add at least one subtask.  
   Note: When creating a subtask, you may link a reward action for automating quest task progress
5. Select Time duration from the below given options

   1. No Time Duration Quest

      <Image align="center" border={false} src="https://files.readme.io/31022fa-Screenshot_2024-04-05_at_11.45.06_AM.png" />
   2. Schedule Start/End Quest

      <Image border={false} src="https://files.readme.io/ffcca50-Screenshot_2024-04-05_at_12.13.55_PM.png" />
   3. User Specific Timer Quest

      <Image border={false} src="https://files.readme.io/450ac44-Screenshot_2024-04-05_at_12.14.08_PM.png" />
6. Click on the **"Create"** Button to create the quest

## Link to API doc

If you intend to generate time-bound quests programmatically through the API, please consult the provided technical [documentation](https://docs.livelike.com/reference/create-quests) for comprehensive guidance on the process.

<br />
