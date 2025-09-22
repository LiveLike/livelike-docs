---
title: Creating and Scheduling Widgets
deprecated: false
hidden: false
metadata:
  robots: index
---
# Overview

The first step in a Widget's lifecycle is creation. To create a widget you will need to provide the content of the Widget as well as other data such as the Program it belongs to. Each widget has distinct content properties that must be provided but some properties are common between all Widgets.

After creating the Widget it is time to publish it or schedule it to be published later. When a widget is published it will be pushed out to users to be interacted with.

And then you're done!
The widget will remain available for users to see and interact with. If you'd like to delete a widget see below.

> **Note:** You can also create **VOD (Video on Demand) Widgets** to schedule interactions at specific playback moments. [Learn more about VOD Widget](https://docs.livelike.com/v1_doc_rewire_vk/update/docs/video-on-demand-widget#/)

## Permissions

To create, publish a widget with an application profile you should be a producer or have the permissions mentioned in the below table.

| Widget     | Create Widget Permission | Publish Widget Permission |
| :--------- | :----------------------- | :------------------------ |
| Text Poll  | create_text_poll         | publish_text_poll         |
| Image Poll | create_image_poll        | publish_image_poll        |
| Alert      | create_alert             | publish_alert             |

<br />

# Create a Widget

Every widget has some common properties that are provided upon creation which can alter the behavior and uses of the widget.

| Property                   | Description                                                                         | Required |
| :------------------------- | :---------------------------------------------------------------------------------- | :------- |
| Program ID                 | The ID of the Program this Widget belongs to                                        | Yes      |
| Timeout                    | A hint for how long this Widget should be displayed for                             | No       |
| Custom Data                | A string of custom data used for custom use cases                                   | No       |
| Interactive Until          | A date on which the widget can no longer be interacted with                         | No       |
| Playback Time Milliseconds | A hint in milliseconds for when this Widget should be displayed during VOD playback | No       |
| Widget Attributes          | A set of custom key-value pairs used for custom use cases                           | No       |
| Sponsor Ids                | List of sponsor Ids to add to a widget                                              | No       |

<br />

## Alerts

| Property   | Description                      | Required |
| :--------- | :------------------------------- | :------- |
| Title      | An alert title                   | No       |
| Text       | The text of the alert            | Yes      |
| Image URL  | The image of the alert           | No       |
| Link Label | The label of a link to the alert | No       |
| Link URL   | The link to the alert            | No       |

<details>
  <summary>Create Alert Widget</summary>

  ```javascript Web
  LiveLike.createAlertWidget({
    programId: '<program-id>',
    text: '<alert text>',
    title: '<alert title>',
    imageUrl: '<imag-url>',
    linkLabel: '<link-label>',
    linkUrl: '<link-url>',
    customData: '<stringified-custom-data-object>',
    widgetAttributes: [{ key: '<attribute-key>', value: '<atribute-value>' }],
    programDateTime: '<date-time-for-syncing-widget-with-video-timestamp>',
    // video playback time for showing video on demand widget
    playbackTimeMs: 2000,
    // UI interactive timeout value
    timeout: 'P0DT0H0M30S',
    interactiveUntil: '<date-time>',
  }).then((res) => console.log(res));
  ```
  ```swift
  let livelike: LiveLike

  livelike.widgetClient.createAlertWidget(
    options: CreateAlertRequestOptions(
      common: CommonCreateWidgetOptions(
        programID: <program - id>
      ),
      title: "<title>",
      text: "<text>",
      imageURL: <image - url>,
      linkLabel: "<link-label>",
      linkURL: <link - url>
    ),
    completion: {
      result
      switch result {
      case .success(let widget):
        break
      case .failure(let error):
        break
      }
    }
  )

  ```
  ```kotlin
  val liveLikeWidgetClient = sdk.widget()
  liveLikeWidgetClient.createAlert(
      request = CreateAlertRequest(
                 programId = request.program_id!!,
                 timeout = request.timeout!!,
                 title = request.title,
                 text = request.text,
                 imageURL = request.image_url,
                 linkLabel = request.link_label,
                 linkURL = request.link_url,
      ), { result,error -> })
  ```
</details>

<br />

## Polls

| Property | Description              | Required |
| :------- | :----------------------- | :------- |
| Question | The question of the poll | Yes      |
| Options  | The options of the poll  | Yes      |

### Option

| Property  | Description                        | Required                  |
| :-------- | :--------------------------------- | :------------------------ |
| Text      | The text description of the option | Yes                       |
| Image URL | The image of the option            | Yes (For Image Poll Only) |

<details>
  <summary>Create TextPoll Widget</summary>

  ```javascript Web
  LiveLike.createTextPollWidget({
    question: '<poll question>',
    programId: '<program-id>',
    options: [
      { description: '<option-description-1>' },
      { description: '<option-description-2>' },
    ],
    customData: '<stringified-custom-data-object>',
    widgetAttributes: [{ key: '<attribute-key>', value: '<atribute-value>' }],
    programDateTime: '<date-time-for-syncing-widget-with-video-timestamp>',
    // video playback time for showing video on demand widget
    playbackTimeMs: 2000,
    // UI interactive timeout value
    timeout: 'P0DT0H0M30S',
    interactiveUntil: '<date-time>',
  }).then((res) => console.log(res));

  // create image poll widget
  LiveLike.createImagePollWidget({
    question: '<poll question>',
    programId: '<program-id>',
    options: [
      { 
        description: '<option-description-1>',
        imageUrl: '<option-image-url>',
      },
      { 
        description: '<option-description-2>',
        imageUrl: '<option-image-url>',
      },
    ],
    customData: '<stringified-custom-data-object>',
    widgetAttributes: [{ key: '<attribute-key>', value: '<atribute-value>' }],
    programDateTime: '<date-time-for-syncing-widget-with-video-timestamp>',
    // video playback time for showing video on demand widget
    playbackTimeMs: 2000,
    // UI interactive timeout value
    timeout: 'P0DT0H0M30S',
    interactiveUntil: '<date-time>',
  }).then((res) => console.log(res));


  ```
  ```swift
  let livelike: LiveLike

  livelike.widgetClient.createTextPollWidget(
    options: CreateTextPollRequestOptions(
      common: CommonCreateWidgetOptions(
        programID: <program - id>
      ),
      question: "<question>",
      options: [
        .init(text: "<option-text>"),
        .init(text: "<option-text>"),
      ]
    ),
    completion: {
      result
      switch result {
      case .success(let widget):
        break
      case .failure(let error):
        break
      }
    }
  )

  livelike.widgetClient.createImagePollWidget(
    options: CreateImagePollRequestOptions(
      common: CommonCreateWidgetOptions(
        programID: <program - id>,
        timeoutSeconds: 1000
      ),
      question: "<question>",
      options: [
        .init(text: "<option-text>", imageURL: <image - url>),
        .init(text: "<option-text>", imageURL: <image - url>),
      ]
    ),
    completion: {
      result
      switch result {
      case .success(let widget):
        break
      case .failure(let error):
        break
      }
    }
  )

  ```
  ```kotlin
  val liveLikeWidgetClient = sdk.widget()
  liveLikeWidgetClient.createTextPoll(
        request = CreateTextPollRequest(
           	 options = "<options>",
             programId = "<program-id>",
           	 question = "<question>",
          	 timeout = "<timeout>",
        ).run { copy(options = txtPoll.options.map { this.Option(it.description) }) },
    { result,error -> })

  liveLikeWidgetClient.createImagePoll(
        request = CreateImagePollRequest(
           	 options = "<options>",
             programId = "<program-id>",
           	 question = "<question>",
          	 timeout = "<timeout>",
        ).run { copy(options = imgPoll.options.map {this.Option(it.description, it.image_url!!)}) },
    { result,error -> })

  ```
</details>

<br />

## Prediction

| Property             | Description                                          | Required |
| :------------------- | :--------------------------------------------------- | :------- |
| Question             | The question of the prediction                       | Yes      |
| Options              | The options for the prediction                       | Yes      |
| Confirmation Message | Message to show when user submitted their prediction | No       |

### Option

| Property  | Description                        | Required                        |
| :-------- | :--------------------------------- | :------------------------------ |
| Text      | The text description of the option | Yes                             |
| Image URL | The image of the option            | Yes (For Image Prediction Only) |

<details>
  <summary>Create Text Prediction Widget</summary>

  ```javascript Web
  LiveLike.createTextPredictionWidget({
    question: '<prediction question>',
    programId: '<program-id>',
    options: [
      { description: '<option-description-1>' },
      { description: '<option-description-2>' },
    ],
    customData: '<stringified-custom-data-object>',
    widgetAttributes: [{ key: '<attribute-key>', value: '<atribute-value>' }],
    programDateTime: '<date-time-for-syncing-widget-with-video-timestamp>',
    // video playback time for showing video on demand widget
    playbackTimeMs: 2000,
    // UI interactive timeout value
    timeout: 'P0DT0H0M30S',
    interactiveUntil: '<date-time>',
    confirmationMessage: '<your-confirmation-message>',
  }).then((res) => console.log(res));

  // create image prediction widget
  LiveLike.createImagePredictionWidget({
    question: '<prediction question>',
    programId: '<program-id>',
    options: [
      { 
        description: '<option-description-1>',
        imageUrl: '<option-image-url>'
      },
      { 
        description: '<option-description-2>',
        imageUrl: '<option-image-url>'
      },
    ],
    customData: '<stringified-custom-data-object>',
    widgetAttributes: [{ key: '<attribute-key>', value: '<atribute-value>' }],
    programDateTime: '<date-time-for-syncing-widget-with-video-timestamp>',
    // video playback time for showing video on demand widget
    playbackTimeMs: 2000,
    // UI interactive timeout value
    timeout: 'P0DT0H0M30S',
    interactiveUntil: '<date-time>',
    confirmationMessage: '<your-confirmation-message>',
  }).then((res) => console.log(res));
  ```
  ```swift
  let livelike: LiveLike

  livelike.widgetClient.createTextPredictionWidget(
    options: CreateTextPollRequestOptions(
      common: CommonCreateWidgetOptions(
        programID: <program - id>
      ),
      question: "<question>",
      options: [
        .init(text: "<option-text>"),
        .init(text: "<option-text>"),
      ]
    ),
    completion: {
      result
      switch result {
      case .success(let widget):
        break
      case .failure(let error):
        break
      }
    }
  )

  livelike.widgetClient.createImagePredictionWidget(
    options: CreateImagePollRequestOptions(
      common: CommonCreateWidgetOptions(
        programID: <program - id>,
        timeoutSeconds: 1000
      ),
      question: "<question>",
      options: [
        .init(text: "<option-text>", imageURL: <image - url>),
        .init(text: "<option-text>", imageURL: <image - url>),
      ]
    ),
    completion: {
      result
      switch result {
      case .success(let widget):
        break
      case .failure(let error):
        break
      }
    }
  )

  ```
  ```kotlin
  val liveLikeWidgetClient = sdk.widget()
  liveLikeWidgetClient.createTextPrediction(
        request = CreateTextPredictionRequest(
            options = "<options>",
            programId = "<program-id>",
            question = "<question>",
           	timeout = "<timeout>",
            confirmationMessage = "Thanks"
        ).run { copy(options = options!!.map {this.Option(it.description)})},
    { result,error -> })

  liveLikeWidgetClient.createImagePrediction(
        request =  CreateImagePredictionRequest(
             options = "<options>",
             programId = "<program-id>",
           	 question = "<question>",
          	 timeout = "<timeout>",
             confirmationMessage = "Thanks"
        ).run { copy(options = options!!.map { this.Option(it.description, it.image_url!!) })},
    { result,error -> })

  ```
</details>

<br />

### Prediction Result

For publishing a prediction result, you can either create a follow-up widget with the correct option ID or update a prediction widget option to declare which option is correct. Once the option(s) are updated, you may then publish a prediction follow-up widget that shows the prediction result to your users.

#### Approach 1: Create a Follow-Up Widget

<details>
  <summary>Create Prediction Follow Up Widget</summary>

  ```javascript Web
  LiveLike.createPredictionFollowUpWidget({
      widgetId: "<widget-id>",
    	// this could be LiveLike.WidgetKind.TEXT_PREDICTION or LiveLike.WidgetKind.IMAGE_PREDICTION 
      widgetKind: LiveLike.WidgetKind.TEXT_PREDICTION,
      correctOptionId: "<option-id>",
      sponsorIds: ["sponsor-id"]
  }).then(res => console.log(res))
  ```
  ```kotlin
  val liveLikeWidgetClient = sdk.widget()
  liveLikeWidgetClient.createPredictionFollowUpWidget(
                  CreatePredictionFollowUpWidgetRequest(
                      widgetId, widgetType, correctOptionId
                  )
              ) { result, error ->          
  						
  							}

  ```
</details>

#### Approach 2: Update Prediction Option

<details>
  <summary>Update Prediction option</summary>

  ```javascript Web
  // for updating text prediction option
  LiveLike.updateTextPredictionWidgetOption({
    widgetId: "ec55d288-5e7d-43ce-83fb-768f98c6d8af",
    optionId: "742abe83-0bb8-4825-9b93-bc26fadb48f9",
    isCorrect: true,
    // optional rewardItemId in case there an need to add reward
    rewardItemId: "<reward-id>",
    // optional rewardItemAmount in case there an need to add reward
  	rewardItemAmount: 30
  }).then(res => console.log(res))

  // for updating image prediction option
  LiveLike.updateTextPredictionWidgetOption({
    widgetId: "ec55d288-5e7d-43ce-83fb-768f98c6d8af",
    optionId: "742abe83-0bb8-4825-9b93-bc26fadb48f9",
    isCorrect: true,
    // optional if image url needs to be updated
    imageUrl: "<updated-image-url>"
    // optional rewardItemId in case there an need to add reward
    rewardItemId: "<reward-id>",
    // optional rewardItemAmount in case there an need to add reward
  	rewardItemAmount: 30
  }).then(res => console.log(res))
  ```
  ```kotlin
  val liveLikeWidgetClient = sdk.widget()
  liveLikeWidgetClient.updateTextPredictionOption(
                  UpdateTextPredictionOptions(
                      textPrediction.id, textPredictionOptionId, null,isCorrect = true, null
                  )
              ) { result, error ->          
  						
  							}

  liveLikeWidgetClient.updateImagePredictionOption(
                  UpdateImagePredictionOptions(
                      imagePrediction.id, imagePredictionOptionsId, null,isCorrect= true, null
                  )
              ) { result, error ->
                  
              }
  ```
  ```swift Swift
  // Updating text prediction follow up option
  livelike.widgetClient.updateTextPredictionFollowUpWidgetOption(
  	options: UpdateTextPredictionFollowUpRequestOptions(
  		predictionID: "prediction-id",
  		optionID: "prediction-option-id",
  		isCorrect: true
  	)
  ) { result in
  	...
  }

  // Updating image prediction follow up option
  livelike.widgetClient.updateImagePredictionFollowUpWidgetOption(
  	options: UpdateImagePredictionFollowUpRequestOptions(
  		predictionID: "prediction-id",
  		optionID: "prediction-option-id",
      isCorrect: true
  	)
  ) { result in
  	...
  }
  ```
</details>

### Publish Prediction FollowUp

Whenever a prediction widget is created, the backend service automatically creates a corresponding follow-up widget. You can get the follow-up widget ID and kind from the prediction widget resource.

<details>
  <summary>Get Prediction Widget Resource</summary>

  ```javascript Web
  // get prediction widget resource
  LiveLike.getWidget({
    id: "<widget-id>",
    kind: LiveLike.WidgetKind.TEXT_PREDICTION
  }).then(widget => {
    const {follow_ups} = widget;
    const followupWidget = follow_ups[0];
    // publish prediction followup widget
    return LiveLike.publishWidget({
  		widgetId: followupWidget.id
      widgetKind: followupWidget.kind
    })
  }).then(res => console.log(res))
  ```
</details>

<br />

## Number Prediction

| Property             | Description                                          | Required |
| :------------------- | :--------------------------------------------------- | :------- |
| Question             | The question of the number prediction                | Yes      |
| Options              | The options for the number prediction                | Yes      |
| Confirmation Message | Message to show when user submitted their prediction | No       |

### Option

| Property  | Description                        | Required |
| :-------- | :--------------------------------- | :------- |
| Text      | The text description of the option | Yes      |
| Image URL | The image of the option            | Yes      |

<details>
  <summary>Create Image Number Prediction Widget</summary>

  ```javascript Web
  LiveLike.createImageNumberPredictionWidget({
    question: '<prediction question>',
    programId: '<program-id>',
    options: [
      { 
        description: '<option-description-1>',
        imageUrl: '<option-image-url>'
      },
      { 
        description: '<option-description-2>',
        imageUrl: '<option-image-url>'
      },
    ],
    customData: '<stringified-custom-data-object>',
    widgetAttributes: [{ key: '<attribute-key>', value: '<atribute-value>' }],
    programDateTime: '<date-time-for-syncing-widget-with-video-timestamp>',
    // video playback time for showing video on demand widget
    playbackTimeMs: 2000,
    // UI interactive timeout value
    timeout: 'P0DT0H0M30S',
    interactiveUntil: '<date-time>',
    confirmationMessage: '<your-confirmation-message>',
  }).then((res) => console.log(res));
  ```
  ```kotlin
  val liveLikeWidgetClient = sdk.widget()
  liveLikeWidgetClient.createImageNumberPrediction(
                  CreateImageNumberPredictionRequest(
                      question = "Test Image Number Prediction",
                      timeout = "P0DT00H00M20S",
                      programId = programId,
                      options = listOf(
                          CreateImageNumberPredictionRequest.Option(
                              1,
                              "https://livelike.com/wp-content/uploads/2019/07/Mike-Moloksher.jpg",
                              "Option 1"
                          ), CreateImageNumberPredictionRequest.Option(
                              1,
                              "https://livelike.com/wp-content/uploads/2019/07/Mike-Moloksher.jpg",
                              "Option 2"
                          )
                      ),
                      confirmationMessage = "Thanks",
                      sponsorIds = sponsorIds
                  )
              ) { result, error ->
                 
              }
  ```
  ```swift
  self.livelike.widgetClient.createNumberPredictionWidget(
  	options: CreateNumberPredictionWidgetOptions(
  		common: CommonCreateWidgetOptions(programID: "program-id"),
  		question: "question",
      options: [
        .init(text: "sample-text-a", imageURL: <image-url>),
        .init(text: "sample-text-b", imageURL: <image-url>)
      ]
    )
  ) { result in
    ...
  }
  ```
</details>

### Number Prediction Result

For publishing a number prediction result, you can update each prediction widget option with the correct number. Once options are updated, you may then publish a prediction follow-up widget that shows the prediction result to your users.

<details>
  <summary>Update Number Prediction Option</summary>

  ```javascript Web
  LiveLike.updateImageNumberPredictionWidgetOption({
    widgetId: "ec55d288-5e7d-43ce-83fb-768f98c6d8af",
    optionId: "742abe83-0bb8-4825-9b93-bc26fadb48f9",
    correctNumber: 10,
    // optional if image url needs to be updated
    imageUrl: "<updated-image-url>"
    // optional rewardItemId in case there an need to add reward
    rewardItemId: "<reward-id>",
    // optional rewardItemAmount in case there an need to add reward
    rewardItemAmount: 30
  }).then(res => console.log(res))
  ```
  ```kotlin
  liveLikeWidgetClient.updateImageNumberPredictionOption(
                  UpdateImageNumberPredictionOptionRequest(
                      prediction.id, predictionOptionId, 12, null, null
                  )
              ) { result, error ->
                  
              
  ```
  ```swift
  self.livelike.widgetClient.updateNumberPredictionFollowUpOption(
    options: UpdateNumberPredictionFollowUpOption(
      predictionID: "prediction-id",
      optionID: "prediction-option-id",
      correctNumber: 10,
      text: "new text",
      imageUrl: <new-image-url>
    )
  ) { result in
    ...
  }
  ```
</details>

### Publish Number Prediction Follow-Up

Whenever a number prediction widget is created, the backend service automatically creates a corresponding follow-up widget. You can get the follow-up widget ID and kind from the number prediction widget resource.

<details>
  <summary>Get Number Prediction Widget Resource</summary>

  ```javascript Web
  // get number prediction widget resource
  LiveLike.getWidget({
    id: "<widget-id>",
    kind: LiveLike.WidgetKind.IMAGE_NUMBER_PREDICTION
  }).then(widget => {
    const {follow_ups} = widget;
    const followupWidget = follow_ups[0];
    // publish prediction followup widget
    return LiveLike.publishWidget({
  		widgetId: followupWidget.id
      widgetKind: followupWidget.kind
    })
  }).then(res => console.log(res))
  ```
  ```kotlin
  liveLikeWidgetClient.createImageNumberPredictionFollowUp(
                  CreateImageNumberPredictionFollowUpRequest(imageNumberPredictionWidget.id, null
                  )
  						) { result, error ->
                  result?.let {
                  		liveLikeWidgetClient.publishWidget(
  								        	 request = PublishWidgetRequest(
                						 type = liveLikeWidget.getWidgetType()!!,
                 						 id = liveLikeWidget.id,
                 						 publishDelay = "P0DT00H00M00S",
                						 programDateTime = null),
    									{ result, error -> })
                  }
              }
  ```
</details>

<br />

## Quiz

| Property | Description              | Required |
| :------- | :----------------------- | :------- |
| Question | The question of the Quiz | Yes      |
| Choices  | The choices for the Quiz | Yes      |

### Option

| Property       | Description                        | Required                  |
| :------------- | :--------------------------------- | :------------------------ |
| Text           | The text description of the Option | Yes                       |
| Image URL      | The image of the option            | Yes (For Image Quiz Only) |
| Correct Option | The correct option of the Quiz     | Yes                       |

<details>
  <summary>Create Text Quiz Widget</summary>

  ```javascript Web
  // create text quiz widget
  LiveLike.createTextQuizWidget({
    question: '<quiz question>',
    programId: '<program-id>',
    choices: [
      { description: '<choice-description-1>', isCorrect: true },
      { description: '<choice-description-2>' },
    ],
    customData: '<stringified-custom-data-object>',
    widgetAttributes: [{ key: '<attribute-key>', value: '<atribute-value>' }],
    programDateTime: '<date-time-for-syncing-widget-with-video-timestamp>',
    // video playback time for showing video on demand widget
    playbackTimeMs: 2000,
    // UI interactive timeout value
    timeout: 'P0DT0H0M30S',
    interactiveUntil: '<date-time>',
    confirmationMessage: '<your-confirmation-message on submit>',
  }).then((res) => console.log(res));

  ```
  ```kotlin
  val liveLikeWidgetClient = sdk.widget()
  liveLikeWidgetClient.createTextQuiz(
        request = CreateTextQuizRequest(
           choices = listOf(Choice("<description>","<is_correct>")),
           programId = "<program-id>",
           question = "<question>",
           timeout = "<timeout>"
        ),
    { result,error -> })

  ```
  ```swift
  let livelike: LiveLike
  livelike.widgetClient.createTextQuizWidget(
    options: CreateTextQuizWidgetOptions(
      common: CommonCreateWidgetOptions(
        programID: self.config.programID
      ),
      question: "<question>",
      choices: [
        .init(text: "option 1", isCorrect: true),
        .init(text: "option 2", isCorrect: false),
      ]
    )
  ) { result in
    switch result {
    case .failure(let error):
      break
    case .success(let model):
      break
    }
  }

  ```
</details>

<details>
  <summary>Create Image Quiz Widget</summary>

  ```javascript Web
  // create image quiz widget
  LiveLike.createImageQuizWidget({
    question: '<quiz question>',
    programId: '<program-id>',
    choices: [
      { 
        description: '<choice-description-1>',
        imageUrl: '<choice-image-url>'
      },
      { 
        description: '<option-description-2>',
        imageUrl: '<option-image-url>',
        isCorrect: true
      },
    ],
    customData: '<stringified-custom-data-object>',
    widgetAttributes: [{ key: '<attribute-key>', value: '<atribute-value>' }],
    programDateTime: '<date-time-for-syncing-widget-with-video-timestamp>',
    // video playback time for showing video on demand widget
    playbackTimeMs: 2000,
    // UI interactive timeout value
    timeout: 'P0DT0H0M30S',
    interactiveUntil: '<date-time>',
    confirmationMessage: '<your-confirmation-message on submit>',
  }).then((res) => console.log(res));

  ```
  ```kotlin
  liveLikeWidgetClient.createImageQuiz(
        request = CreateImageQuizRequest(
           choices = listOf(Choice("<description>","<is_correct>","<image_url>")),
           programId = "<program-id>",
           question = "<question>",
           timeout = "<timeout>"
        ),
    { result,error -> })

  ```
  ```swift
  let livelike: LiveLike
  livelike.widgetClient.createImageQuizWidget(
    options: CreateImageQuizWidgetOptions(
      common: CommonCreateWidgetOptions(
        programID: self.config.programID
      ),
      question: "<question>",
      choices: [
        .init(text: "option 1", imageURL: URL(string: "<image-url>"), isCorrect: true),
        .init(text: "option 2", imageURL: URL(string: "<image-url>"), isCorrect: false),
      ]
    )
  ) { result in
    switch result {
    case .failure(let error):
      break
    case .success(let model):
      break
    }
  }

  ```
</details>

<br />

## Text Ask

| Property | Description                      | Required |
| :------- | :------------------------------- | :------- |
| Title    | The title of the text ask widget | Yes      |
| Prompt   | The prompt question              | Yes      |

<details>
  <summary>Create Text Ask Widget</summary>

  ```javascript Web
  LiveLike.createTextAskWidget({
    programId: '<program-id>',
    prompt: "< your question prompt>", 
    title: "<your title>",
    customData: '<stringified-custom-data-object>',
    widgetAttributes: [{ key: '<attribute-key>', value: '<atribute-value>' }],
    programDateTime: '<date-time-for-syncing-widget-with-video-timestamp>',
    // video playback time for showing video on demand widget
    playbackTimeMs: 2000,
    // UI interactive timeout value
    timeout: 'P0DT0H0M30S',
    interactiveUntil: '<date-time>',
    confirmationMessage: '<your-confirmation-message on submit>',
  }).then((res) => console.log(res));
  ```
  ```kotlin
  val liveLikeWidgetClient = sdk.widget()
  liveLikeWidgetClient.createTextAsk(
        request = CreateTextAskRequest(
           prompt = "<prompt>",
           programId = "<program-id>",
           title = "<title>",
           timeout = "<timeout>",
           confirmationMessage = "Thanks for submission"
        ),
    { result,error -> })
  ```
  ```swift
  let livelike: LiveLike

  livelike.widgetClient.createTextAskWidget(
    options: CreateTextAskWidgetOptions(
      common: CommonCreateWidgetOptions(
        programID: config.programID
      ),
      title: "<title>",
      prompt: "<prompt>",
      confirmationMessage: "<confirmation-message>"
    ),
    completion: {
      result
      switch result {
      case .success(let widget):
        break
      case .failure(let error):
        break
      }
    }
  )
  ```
</details>

<br />

<br />

# Publish a Widget

| Property          | Description                                                 | Required |
| :---------------- | :---------------------------------------------------------- | :------- |
| Widget ID         | The ID of the widget to publish                             | Yes      |
| Widget Kind       | The kind of widget to publish                               | Yes      |
| Publish Delay     | The duration at which the widget will be delayed to publish | No       |
| Program Date Time | A hint for live video synchronization                       | No       |

<details>
  <summary>Publish Widget</summary>

  ```javascript Web
  LiveLike.publishWidget({
    widgetId: '<widget-id>',
    widgetKind: '<widget-kind>',
    programDateTime: 'date-time-in-ISO-string-format'
  }).then((res) => console.log(res));
  ```
  ```swift
  let livelike: LiveLike

  livelike.widgetClient.publishWidget(
    options: PublishWidgetRequestOptions(
      kind: <widget-kind>,
      id: "<widget-id>",
      publishDelaySeconds: <publish-delay-seconds>
    )
  ) { result
  	switch result {
    case .success(let widget):
      break
    case .failure(let error):
      break
    }
  }
  ```
  ```kotlin
  val liveLikeWidgetClient = sdk.widget()
  liveLikeWidgetClient.publishWidget(
          request = PublishWidgetRequest(
                 type = liveLikeWidget.getWidgetType()!!,
                 id = liveLikeWidget.id,
                 publishDelay = "P0DT00H00M00S",
                 programDateTime = null),
    			{ result, error -> })
  ```
</details>

<br />

Delete Widget



| Property    | Description                    | Required |
| :---------- | :----------------------------- | :------- |
| Widget ID   | The id of the widget to delete | Yes      |
| Widget Kind | The kind of widget to delete   | Yes      |

```javascript Web
LiveLike.deleteWidget({
  widgetId: '<widget-id>',
  widgetKind: '<widget-kind>',
}).then((res) => console.log(res));

```
```swift
let livelike: LiveLike

livelike.widgetClient.deleteWidget(
  options: DeleteWidgetRequestOptions(
    kind: <widget-kind>,
    id: "<widget-id>"
  )
) { result
	switch result {
  case .success(let widget):
    break
  case .failure(let error):
    break
  }
}
```
```kotlin
val liveLikeWidgetClient = sdk.widget()
liveLikeWidgetClient.deleteWidget(
        request = DeleteWidgetRequest(
               type = liveLikeWidget.getWidgetType()!!,
               id = liveLikeWidget.id),
  			{ result, error -> })
```
