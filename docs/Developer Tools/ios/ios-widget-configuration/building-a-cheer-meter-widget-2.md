---
title: Building a Cheer Meter Widget
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Cheer Meter Widget | React Native SDK | LiveLike Developer Hub
  description: >-
    Cheer meters provide allow users to engage with your platform and share
    their opinions. Learn more about React Native SDK Cheer Meters.
  robots: index
next:
  description: ''
  pages:
    - type: basic
      slug: using-custom-widget-ui-with-the-widgetviewcontroller
      title: Using Custom Widget UI with the WidgetViewController
    - type: basic
      slug: building-an-alert-widget
      title: Building an Alert Widget
---
> 📘 Minimum SDK Version
>
> 2.11

This is a guide on building a custom Cheer Meter Widget. For an overview of the Custom Widget UI system see [Custom Widget UI](doc:custom-widget-ui). 

> 📘 Considerations for WidgetPopupViewController
>
> If you plan on using your Custom Widget UI with the WidgetPopupViewController see [Using Custom Widget UI with the WidgetPopupViewController](doc:using-custom-widget-ui-with-the-widgetviewcontroller)

## The Cheer Meter Model

The Cheer Meter Model is a reflection of a Cheer Meter as it is on the server.

[API Reference](http://livelike-docs.s3-website-us-east-1.amazonaws.com/ios/api-reference/Classes/CheerMeterWidgetModel.html)

**Initialize UI With Cheer Meter Data**\
The Cheer Meter Model provides data about the Cheer Meter such as the title text and the Cheer Meter options.\
The model also provides metadata about the widget such as the Date that it was created or the timeout duration set by the Producer.

```swift
class CustomCheerMeter: UIViewController {
    let titleLabel: UILabel = UILabel()
    var optionButtons: [UIButton] = []

    let model: CheerMeterWidgetModel

    init(model: CheerMeterWidgetModel) {
        self.model = model
        super.init(nibName: nil, bundle: nil)
    }

    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }

    override func viewDidLoad() {
        super.viewDidLoad()

        // Initializing UI elements with Model data
        titleLabel.text = model.title
        model.options.enumerated().forEach { index, option in
            let optionButton = UIButton()
            optionButton.setTitle("\(option.voteCount)", for: .normal)
            do {
                let imageData = try Data(contentsOf: option.imageURL)
                let image = UIImage(data: imageData)
                optionButton.setImage(image, for: .normal)
            } catch {
                print(error)
            }
            optionButtons.append(optionButton)
        }
    }
}
```

**Submitting a vote**\
Due to the high volume of votes expected on a Cheer Meter the SDK will batch the votes puts a 1 second throttle on the vote request.

To submit a vote take the id of the option and call `submitVote(optionID:)`

```swift
class CustomCheerMeter: UIViewController {
    ...
    override func viewDidLoad() {
        ...
        model.options.enumerated().forEach { index, option in
            ...
            optionButton.tag = index // Will be used to lookup option id later
            optionButton.addTarget(self, action: #selector(optionButtonHandler), for: .touchUpInside)
            ...
        }
    }

    // Get the option id by index and submit vote
    @objc private func optionButtonHandler(sender: UIButton) {
        guard model.options.count > sender.tag else { return }
        model.submitVote(optionID: model.options[sender.tag].id)
    }
}
```

**Listening for Updates on the Cheer Meter**\
The CheerMeterModelDelegate gives you access to updates on the Cheer Meter. This includes an event for when the vote count changes on the server and also an event for when the user's batched vote requests are completed.

```swift
class CustomCheerMeter: UIViewController {
    ...
    override func viewDidLoad() {
        ...
        model.delegate = self
    }
    ...
}

extension CustomCheerMeter: CheerMeterWidgetModelDelegate {
    func cheerMeterWidgetModel(
        _ model: CheerMeterWidgetModel,
        voteCountDidChange voteCount: Int,
        forOption optionID: String
    ) {
        // This method is not guaranteed to be called on the Main thread
        DispatchQueue.main.async {
            guard let optionIndex = model.options.firstIndex(where: { $0.id == optionID }) else { return }
            guard self.optionButtons.count > optionIndex else { return }
            self.optionButtons[optionIndex].setTitle("\(voteCount)", for: .normal)
        }

    }

    func cheerMeterWidgetModel(
        _ model: CheerMeterWidgetModel,
        voteRequest: CheerMeterWidgetModel.VoteRequest,
        didComplete result: Result<CheerMeterWidgetModel.Vote, Error>
    ) {
        // To make your UI more responsive
        // You may want to optimistically update your UI when the user votes
        // While the throttled network request is being made
        // You can use this method to validate your UI in case the request fails
    }
}
```

## Full CustomCheerMeter Sample

```swift
class CustomCheerMeter: UIViewController {
    let stackView: UIStackView = {
        let stackView = UIStackView()
        stackView.translatesAutoresizingMaskIntoConstraints = false
        stackView.axis = .vertical
        stackView.distribution = .fillEqually
        stackView.alignment = .leading
        return stackView
    }()

    let titleLabel: UILabel = {
        let label = UILabel()
        label.translatesAutoresizingMaskIntoConstraints = false
        label.numberOfLines = 0
        return label
    }()

    var optionButtons: [UIButton] = []

    let model: CheerMeterWidgetModel

    init(model: CheerMeterWidgetModel) {
        self.model = model
        super.init(nibName: nil, bundle: nil)
    }

    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }

    override func loadView() {
        view = stackView
    }

    override func viewDidLoad() {
        super.viewDidLoad()

        stackView.addArrangedSubview(titleLabel)

        // Initializing UI elements with Model data
        titleLabel.text = model.title
        model.options.enumerated().forEach { index, option in
            let optionButton = UIButton()
            optionButton.translatesAutoresizingMaskIntoConstraints = false
            optionButton.tag = index // Will be used to lookup option id later
            optionButton.setTitle("\(option.voteCount)", for: .normal)
            do {
                let imageData = try Data(contentsOf: option.imageURL)
                let image = UIImage(data: imageData)
                optionButton.setBackgroundImage(image, for: .normal)
            } catch {
                print(error)
            }
            optionButton.addTarget(self, action: #selector(optionButtonHandler), for: .touchUpInside)
            optionButtons.append(optionButton)
            stackView.addArrangedSubview(optionButton)
        }

        model.delegate = self
    }

    @objc private func optionButtonHandler(sender: UIButton) {
        guard model.options.count > sender.tag else { return }
        model.submitVote(optionID: model.options[sender.tag].id)
    }
}

extension CustomCheerMeter: CheerMeterWidgetModelDelegate {
    func cheerMeterWidgetModel(
        _ model: CheerMeterWidgetModel,
        voteCountDidChange voteCount: Int,
        forOption optionID: String
    ) {
        // This method is not guaranteed to be called on the Main thread
        DispatchQueue.main.async {
            guard let optionIndex = model.options.firstIndex(where: { $0.id == optionID }) else { return }
            guard self.optionButtons.count > optionIndex else { return }
            self.optionButtons[optionIndex].setTitle("\(voteCount)", for: .normal)
        }
    }

    func cheerMeterWidgetModel(
        _ model: CheerMeterWidgetModel,
        voteRequest: CheerMeterWidgetModel.VoteRequest,
        didComplete result: Result<CheerMeterWidgetModel.Vote, Error>
    ) {
        // To make your UI more responsive
        // You may want to optimistically update your UI when the user votes
        // While the throttled network request is being made
        // You can use this method to validate your UI in case the request fails
    }
}
```
