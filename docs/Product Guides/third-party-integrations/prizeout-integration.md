---
title: Prizeout
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: >-
    You will successfully integrate Prizeout with LiveLike after completing all
    the above steps. The next step is to set up Prizeout for monetization
    feature in a reward item. Please read this documentation to set up Prizeout
    in rewards.
  pages:
    - type: basic
      slug: prizeout-for-rewards
      title: Prizeout for Rewards
---
Integrating Prizeout with LiveLike CMS enables the points redemption feature in your platform to engage your customers with an exciting gamification experience. to know more about this feature please check <a href="https://docs.livelike.com/docs/prizeout-for-rewards" target="_blank">here</a> this out.

## How to connect Prizeout to LiveLike?

> 🚧 Make sure you have an account with Prizeout
>
> Make sure you have an account with Prizeout and have access to their partner dashboard. If you don't have one please create one from <a href="https://partners.prizeout.com/#/register" target="_blank">here</a>.

We have made enabling this feature very easy for you and please follow the below steps in LiveLike CMS for integration.

1. Navigate to **Integrations** then look for Prizeout and click **Connect** button to start integrating.

![1440](https://files.readme.io/0798e4c-PO-integration.png "PO-integration.png")

2. Enter Prizeout **Partner ID, API Key, API Secret Key,** and **HTTP Security Token** in respective input fields

![1440](https://files.readme.io/d733492-PO-keys.png "PO-keys.png")

To get all the required fields, Go to Prizeout dashboard and navigate **Prizeout Dashboard** > **Account Settings**

3. Click **Connect** button to complete integration.

4. Once the integration is successful then you will see an **Active** switch is on.

![1440](https://files.readme.io/a463ed0-PO-active.png "PO-active.png")

## Callback APIs

Prizeout calls a series of HTTP callbacks provided by LiveLike to trigger some actions like verifying user balance. Following are the APIs which you need to paste in your **Prizeout Dashboard** > **Account Settings** with each relevant label.

<Table align={["left","left","left"]}>
  <thead>
    <tr>
      <th>
        Label
      </th>

      <th>
        Description
      </th>

      <th>
        API Endpoint
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        Balance Check
      </td>

      <td>
        Used to verify the user's balance
      </td>

      <td>
        [https://cf-blast.livelikecdn.com/api/v1/applications/\{client\_id}/prizeout-callback-balance/](https://cf-blast.livelikecdn.com/api/v1/applications/\{client_id}/prizeout-callback-balance/)
      </td>
    </tr>

    <tr>
      <td>
        Cashout Success
      </td>

      <td>
        Executed when a cash out request is completed and successful.
      </td>

      <td>
        [https://cf-blast.livelikecdn.com/api/v1/applications/\{client\_id}/prizeout-callback-success/](https://cf-blast.livelikecdn.com/api/v1/applications/\{client_id}/prizeout-callback-success/)
      </td>
    </tr>

    <tr>
      <td>
        Cashout Fail
      </td>

      <td>
        Executed when a cash out request fails.
      </td>

      <td>
        [https://cf-blast.livelikecdn.com/api/v1/applications/\{client\_id}/prizeout-callback-failure/](https://cf-blast.livelikecdn.com/api/v1/applications/\{client_id}/prizeout-callback-failure/)
      </td>
    </tr>

    <tr>
      <td>
        Session
      </td>

      <td>
        Prizeout will ask at various stages if the session\_id you passed us is valid.
      </td>

      <td>
        [https://cf-blast.livelikecdn.com/api/v1/applications/\{client\_id}/prizeout-callback-session/](https://cf-blast.livelikecdn.com/api/v1/applications/\{client_id}/prizeout-callback-session/)
      </td>
    </tr>
  </tbody>
</Table>
