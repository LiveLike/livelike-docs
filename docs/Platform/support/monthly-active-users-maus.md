---
title: Monthly Active Users (MAUs)
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
Monthly Active Users (MAUs) are the primary factor when calculating costs for using the Engagement platform. As an integrator it is important that you manage when and how the platform tracks unique users.

## How are MAUs counted?

By default, the Engagement SDK will generate a new user upon first initialization. The uuid of this new user is stored in local data and will be reused in future SDK initializations. Since the uuid is only stored in local data, it may be deleted if the user updates or uninstalls the application and won't persist across devices. This may results in higher than expected MAU count so it is highly recommend that you override this default behavior and manage user UUID persistence in your own database.

Recommendations

* Initialize the Engagement SDK as late as possible. If you have any login or pay walls in your application that block access to the Engagement platform features then you should initialize the SDK after the user passes those walls.
* Override where the generated user UUIDs are stored for a more accurate count.
