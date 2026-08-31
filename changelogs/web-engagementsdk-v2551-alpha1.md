---
title: Web engagementsdk v2.55.1-alpha.1
author: ReadMe API
hidden: false
published_at: '2024-04-16T13:46:19.043Z'
---
### Fixes:

* fix sorting issue in `livelike-chat` messages caused by spoiler prevention with messages sent at the same program\_date\_time, ensuring correct order by converting variables to milliseconds for comparison in the `programDateTimeSort` function.