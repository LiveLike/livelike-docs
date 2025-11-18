---
title: Points Redemption
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# Reward Store

LiveLike now powers a complete end-to-end rewards economy — enabling your users to **earn** points through LiveLike experiences and **burn** those points by redeeming rewards directly inside your product. With this expansion, LiveLike provides everything you need to build a flexible, scalable loyalty ecosystem.

Alongside long-standing earning features like **Quests**, **Widgets**, **User Actions** (internal & external), and **Mini Games**, you can now offer two primary redemption options:

1. **LiveLike Reward Store** — Fully owned & configurable product redemption experience.
2. **Prizeout Integration** — Cash-out and gift-card redemption

## Overview

The LiveLike Reward Store lets you curate a catalog of redeemable items — digital or physical — and define custom redemption rules for different user segments. Whether you're building a loyalty marketplace, a simple perk catalog, or a gated tiered shop, the Reward Store gives you full control over what users can redeem and when.

It is fully integrated with the LiveLike economy, ensuring:

* Automatic point deduction on redemption
* Order creation and management
* Tier and level-based product access
* Configurable eligibility and visibility rules
* Full tracking and analytics

## Capabilities

The LiveLike Reward Store supports a wide range of features to help you build the ideal redemption experience:

### **Catalog & Product Management**

* Create, edit, and categorize reward products
* Add product attributes, images, and descriptions
* Configure stock and availability rules (optional)
* Specify point cost and tier/level restrictions

### **User Personalization & Access Control**

* Gate products by **user tier**
* Feature specific products to highlight them in your storefront
* Combine with quests or user actions to unlock exclusive items

### **Redemption Experience**

* Users can redeem eligible items with a single API call
* Automatic validation of balance, tier, and visibility rules
* Order creation and order-status tracking
* Customizable confirmation, fulfillment, and post-redemption flows

### **Order History & Tracking**

* Track active and past user orders
* Store metadata for fulfillment or digital delivery workflows
* Support for custom order status and fulfillment states

### **API-First Architecture**

* Use LiveLike’s fully documented APIs to build any front-end experience — web, mobile, embedded, or hybrid
* Fetch product list, product details, and user order history
* Initiate redemptions and manage workflows programmatically

## Store UI Examples

Use the examples below to understand how the Reward Store may appear in a typical implementation.

### **Catalog Page**

> <Image align="center" border={false} src="https://files.readme.io/0b3cd36e64a7902638fa2a3e5c05c62562ed4047c94840d24f37f3a291ca6e49-Screenshot_2025-11-18_at_12.55.58_PM.png" />

A product listing view showcasing available rewards, featuring:

* Product image thumbnail
* Point cost
* Tier/level restrictions
* Featured product sections

### **Product Details Page**

> <Image align="center" border={false} src="https://files.readme.io/98be40d79d0b59f51b367a8a76e6dbc99b962c5924dbdd8cc166a12373122c78-Screenshot_2025-11-18_at_12.56.19_PM.png" />

A dedicated view for each reward item, typically including:

* Large product image
* Detailed description
* Cost and eligibility requirements
* Redeem button and confirmation flow

### **Order History Page**

> <Image align="center" border={false} src="https://files.readme.io/6914e55ce8b9bfe7496710efa78f0f58dafa7361894bbd035a37ccac6dc184b1-Screenshot_2025-11-18_at_12.55.50_PM.png" />

A history view that helps users track past and ongoing redemptions.

## Reward Store Front APIs

LiveLike provides a complete set of APIs to build your own fully customized storefront. These include:

* **Products and product details**
* **Categories and category details**
* **User order history and order details**
* **Product redemption**
* **Reward items and reward item details**
* **Tiers and tier details**
* **Refunds and refund details**

You can find the full Reward Store API documentation here: [LINK](https://docs.livelike.com/reference/reward-store-api-documentation#/)

***

# Prizeout Integration

LiveLike enables point redemption by integrating Prizeout with CMS. Prizeout is an innovative withdrawal platform that gives users more purchasing power in the form of digital gift cards with bonus offers. Those who choose Prizeout withdrawals usually receive their gift cards via e-mail within minutes and can redeem them at mainstream retailers such as Airbnb, Apple, GameStop, Lowe’s, and more.

Imaging your platform can reward points to your customers for doing actions such as registering on the platform, watching videos, inviting a friend, subscribing, completing a quest, answering a poll, and a lot more. then your customers can redeem their earned points as gift cards and claim them in a variety of brands. It will help your business retain customers, convert prospective customers into loyal customers, and more. Now all of these are possible with the LiveLike point redemption feature.

<Image alt="4112" border={false} src="https://files.readme.io/f9b7965-Infographic_v2.png" title="Infographic v2.png" />

<br />

## How using Prizeout can benefit your brand?

It will benefit your customers by having the power of redeeming points in different types of options such as real gift cards. Partners have had a 25%+ cumulative increase in user retention, 95% of brands on the Prizeout platform offer a potential bonus value of up to 25%, and Withdrawal is a no-cost payments service.

## How to get started?

To start using this feature, first should complete Prizeout integration with LiveLike CMS and follow the steps from below to create a reward item with a monetization feature and use that item to reward for certain actions of a user.

> 🚧 The first step to start using this feature
>
> Make sure you have successfully integrated Prizeout with LiveLike to start using this feature If not, please check this <a href="https://docs.livelike.com/docs/prizeout-integration" target="_blank">documentation</a> for the complete guide.

## Create a monetization-enabled reward item

Let’s see how to create a reward item with Prizeout for monetization feature.

1. Navigate to **Rewards** > **New Reward Item** to start creating a new reward item.

<Image alt="1440" border={false} src="https://files.readme.io/240c67f-Reward_Items.png" title="Reward Items.png" />

2. Add an image or symbol for the item and enter a name for the reward item in the **Name** input field.

<Image alt="1440" border={false} src="https://files.readme.io/ca981c0-New_Reward_Item_-_Set_PrizeOut_Point.png" title="New Reward Item - Set PrizeOut Point.png" />

3. Turn on the **Prizeout Points** switch.

<Image alt="1440" border={false} src="https://files.readme.io/4c56c50-set-conversion.png" title="set-conversion.png" />

4. To set the conversion rate, Enter the **Reward Item Amount** and the **Prizout Points** equal to that Reward Item.

> 📘 1 Prizeout Point = 1 cent that you are rewarding to a customer.

<Image alt="1440" border={false} src="https://files.readme.io/a98f489-New_Reward_Item_-_Set_PrizeOut_Point_1.png" title="New Reward Item - Set PrizeOut Point (1).png" />

5. Click **Create** to submit all inputs.

## Using monetization-enabled reward item for an action

Now you have successfully created a new reward item with the Prizeout feature and now let’s see how to use that.

1. Navigate to **Rewards** > **Tables**. Then Create a new reward table or click on an existing table.

<Image alt="1440" border={false} src="https://files.readme.io/54f2191-Reward_table.png" title="Reward table.png" />

2. Click **New Entry** to create a reward for an action.

<Image alt="1440" border={false} src="https://files.readme.io/403ae96-Reward_table_entries.png" title="Reward table entries.png" />

3. Select an action from the **Reward Action** Dropdown.
4. Select an item from the **Reward Item** dropdown for which you added the conversion rate in the reward item creation step.
5. Enter an amount in the **Reward Amount** input field and that amount will be received by the users.

<Image alt="1440" border={false} src="https://files.readme.io/4edd928-Reward_table_entries_-_New.png" title="Reward table entries - New.png" />

For example, as you can see above that once a customer performs a “Vote on a poll” action, he will receive 500 “LiveLike Points” which is equal to "5 Prizeout Points“.

7. Click **Create** to submit all inputs.

After all of these steps, you have successfully created a reward item with prizeout feature. Now, you can move forward with client side integration to let your users earn prizeout points each time when they earn this item and redeem gift cards.

## Client Side Integration

Before loading the Prizeout marketplace widget on the client side, you will need to create Prizeout User Session using the [API Endpoint](https://docs.livelike.com/reference/prizeout-user-session) provided by LiveLike.  
Use the `session_id` to initialise the Prizeout SDK.

Refer [Prizeout API documentation](https://partners.prizeout.com/#/api) for more details.

Below is an example of how you can integrate prizeout and let users redeem gift cards with their prizeout points. Follow the steps mentioned above and fill in all the required keys in the config.js file.

<Embed url="https://stackblitz.com/edit/js-yznhaz?file=index.html,config.js,index.js,style.css" iframe="true" href="https://stackblitz.com/edit/js-yznhaz?file=index.html,config.js,index.js,style.css" />
