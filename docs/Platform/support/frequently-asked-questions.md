---
title: Frequently Asked Questions
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: FAQs | LiveLike Developer Hub | Audience Engagement Suite
  description: >-
    We want to give you all the support you need to have a successful
    integration with LiveLike! Check out this list of FAQs to learn more.
  robots: index
next:
  description: ''
---
## General

### Can I use chat rooms without widgets and programs, or vice versa?

Yes, you can. Chat rooms and programs are independent of each other, and can be combined in various ways to achieve different results. For example, you could be a part of many group chats, the members of which may be watching different videos and interacting with different widgets than you are.

### Which platforms are supported?

For a current list of supported platforms, check the [supported platforms](doc:supported-platforms) page.

### How big are the SDKs?

<Table align={["left","left"]}>
  <thead>
    <tr>
      <th>
        Version
      </th>

      <th>
        Size
      </th>
    </tr>
  </thead>

  <tbody>
    <tr>
      <td>
        iOS
      </td>

      <td>
        3.5 MB
      </td>
    </tr>

    <tr>
      <td>
        Android
      </td>

      <td>
        2.1 MB
      </td>
    </tr>

    <tr>
      <td>
        Web (Production Build)
      </td>

      <td>
        430 KB
      </td>
    </tr>

    <tr>
      <td>
        Web (Development Build)
      </td>

      <td>
        3 MB
      </td>
    </tr>
  </tbody>
</Table>

### Where can I find sample integration code?

We have sample applications that can be browsed and downloaded by developers to see the SDKs used in action.

* [iOS Sample App](https://github.com/LiveLike/engagement-sample-app)
* [Android Sample App](https://github.com/LiveLike/SampleAndroidApp)
* [Web Sample App](https://github.com/LiveLike/Web-SDK-HTML-Demo)

## Users

### How do I integrate with my existing user logins and accounts?

You should store the access tokens associated with LiveLike profiles on your own user records if you already have them. See the [Integrating with Logins](doc:using-profiles-with-logins) guide for a how-to and example use cases.

## Chat

### How do I set the chat nickname?

Chat nicknames are controlled by the nickname stored on the [Profiles](doc:user-profiles). When the profile nickname is changed, the chat nickname will change too for all future messages sent.

* [User Profiles on iOS](doc:ios-user-profiles) 
* [User Profiles on Web](doc:web-user-profile-integration)

### Can I control who can send chat messages?

Yes, the ability to control who can and cannot send messages in chat allows creating curated experiences like Influencer Chat where only users who match your criteria may send messages. Everybody else can follow along and add their reactions, but they can't send messages. Read more about [Customizing Chat Input](doc:custom-chat-input).

### Can I customize the stickers and reactions being used in chat?

Yes. Log in to the CMS and navigate to the Stickers or Reactions section to customize your assets. We also provide [Chat Asset Guidelines](doc:chat-sticker-guidelines) for teams creating their own assets.

## Data Integrations

### Can the unique ID's for profiles, programs, chat rooms, etc. be chosen or customized by my integration?

Those identifiers are assigned by the LiveLike server, and so they cannot be chosen or changed. It is recommended that you store those identifiers alongside your own records when doing an integration.

In the case of programs, the LiveLike-assigned ID's cannot be replaced, but a secondary [Custom ID](doc:custom-program-ids) can be assigned.

### How do I share LiveLike profile data across all of my products?

Configuring your products to use the same LiveLike Client ID (aka application ID) will allow LiveLike profile data to persist across all of your products. That includes the same product on multiple platforms, as well as independent or complementary products on the same platform. You should only create a new LiveLike app when you want to keep the end-user experience independent.

## Video

### Can features like chat and widgets be used without video?

Yes those features can be used without video.

### Do the Program Date Time values in HLS streams need to be close to the present wall-clock time for spoiler prevention to work?

No, they do not. The timestamps in the streams will be compared to the timestamps on the widget without comparing to the wall clock time on the device. That means the timestamps can be current, or arbitrarily far into the past or future. The timestamps on widgets and streams only have to have a correspondence.

### Can I use a device's time to prevent spoilers if I'm using a custom sync strategy?

No, we strongly advise against this. Preventing spoilers is dramatically more reliable when everyone in the audience is referencing time source they have in a common, like the one coming from inside the stream they are all watching. Those common timestamps are usually inside of the stream in the form of Program Date Time directives or custom ID3 tags.

Using times from a user's device is unreliable because no two devices have perfectly synced clocks, and it's fairly common that any two independent clocks are significantly divergent. Times from those clocks also have no information about where in a stream a user actually is at a given instant, so even perfectly synchronized clocks are not useful for preventing spoilers.

### Do I have to use the same HLS video stream in the CMS as I do in my app?

No you do not, as long as both streams are using the same time source for the Program Date Time directives in the manifest, and those timestamps correspond to the same action in the video.

## Content and Design

### How big should my images in poll, quiz, and prediction widgets be?

Images in options for polls, quizzes, and predictions will be scaled to 80 pixels wide cropped 80 pixels tall. For more details see the [Widget Asset Guidelines section](doc:widget-asset-guidelines#section-polls-quizzes-and-predictions). Try to use images close to those dimensions.
