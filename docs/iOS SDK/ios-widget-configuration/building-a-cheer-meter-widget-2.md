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
[block:callout]
{
  "type": "info",
  "title": "Minimum SDK Version",
  "body": "2.11"
}
[/block]
This is a guide on building a custom Cheer Meter Widget. For an overview of the Custom Widget UI system see [Custom Widget UI](doc:custom-widget-ui). 
[block:callout]
{
  "type": "info",
  "title": "Considerations for WidgetPopupViewController",
  "body": "If you plan on using your Custom Widget UI with the WidgetPopupViewController see [Using Custom Widget UI with the WidgetPopupViewController](doc:using-custom-widget-ui-with-the-widgetviewcontroller)"
}
[/block]

[block:api-header]
{
  "title": "The Cheer Meter Model"
}
[/block]
The Cheer Meter Model is a reflection of a Cheer Meter as it is on the server.

[API Reference](http://livelike-docs.s3-website-us-east-1.amazonaws.com/ios/api-reference/Classes/CheerMeterWidgetModel.html)

**Initialize UI With Cheer Meter Data**
The Cheer Meter Model provides data about the Cheer Meter such as the title text and the Cheer Meter options.
The model also provides metadata about the widget such as the Date that it was created or the timeout duration set by the Producer.
[block:code]
{
  "codes": [
    {
      "code": "class CustomCheerMeter: UIViewController {\n    let titleLabel: UILabel = UILabel()\n    var optionButtons: [UIButton] = []\n\n    let model: CheerMeterWidgetModel\n\n    init(model: CheerMeterWidgetModel) {\n        self.model = model\n        super.init(nibName: nil, bundle: nil)\n    }\n\n    required init?(coder: NSCoder) {\n        fatalError(\"init(coder:) has not been implemented\")\n    }\n\n    override func viewDidLoad() {\n        super.viewDidLoad()\n\n        // Initializing UI elements with Model data\n        titleLabel.text = model.title\n        model.options.enumerated().forEach { index, option in\n            let optionButton = UIButton()\n            optionButton.setTitle(\"\\(option.voteCount)\", for: .normal)\n            do {\n                let imageData = try Data(contentsOf: option.imageURL)\n                let image = UIImage(data: imageData)\n                optionButton.setImage(image, for: .normal)\n            } catch {\n                print(error)\n            }\n            optionButtons.append(optionButton)\n        }\n    }\n}",
      "language": "swift"
    }
  ]
}
[/block]
**Submitting a vote**
Due to the high volume of votes expected on a Cheer Meter the SDK will batch the votes puts a 1 second throttle on the vote request.

To submit a vote take the id of the option and call `submitVote(optionID:)`
[block:code]
{
  "codes": [
    {
      "code": "class CustomCheerMeter: UIViewController {\n    ...\n    override func viewDidLoad() {\n        ...\n        model.options.enumerated().forEach { index, option in\n            ...\n            optionButton.tag = index // Will be used to lookup option id later\n            optionButton.addTarget(self, action: #selector(optionButtonHandler), for: .touchUpInside)\n            ...\n        }\n    }\n\n    // Get the option id by index and submit vote\n    @objc private func optionButtonHandler(sender: UIButton) {\n        guard model.options.count > sender.tag else { return }\n        model.submitVote(optionID: model.options[sender.tag].id)\n    }\n}",
      "language": "swift",
      "name": ""
    }
  ]
}
[/block]
**Listening for Updates on the Cheer Meter**
The CheerMeterModelDelegate gives you access to updates on the Cheer Meter. This includes an event for when the vote count changes on the server and also an event for when the user's batched vote requests are completed.
[block:code]
{
  "codes": [
    {
      "code": "class CustomCheerMeter: UIViewController {\n    ...\n    override func viewDidLoad() {\n        ...\n        model.delegate = self\n    }\n    ...\n}\n\nextension CustomCheerMeter: CheerMeterWidgetModelDelegate {\n    func cheerMeterWidgetModel(\n        _ model: CheerMeterWidgetModel,\n        voteCountDidChange voteCount: Int,\n        forOption optionID: String\n    ) {\n        // This method is not guaranteed to be called on the Main thread\n        DispatchQueue.main.async {\n            guard let optionIndex = model.options.firstIndex(where: { $0.id == optionID }) else { return }\n            guard self.optionButtons.count > optionIndex else { return }\n            self.optionButtons[optionIndex].setTitle(\"\\(voteCount)\", for: .normal)\n        }\n\n    }\n\n    func cheerMeterWidgetModel(\n        _ model: CheerMeterWidgetModel,\n        voteRequest: CheerMeterWidgetModel.VoteRequest,\n        didComplete result: Result<CheerMeterWidgetModel.Vote, Error>\n    ) {\n        // To make your UI more responsive\n        // You may want to optimistically update your UI when the user votes\n        // While the throttled network request is being made\n        // You can use this method to validate your UI in case the request fails\n    }\n}",
      "language": "swift"
    }
  ]
}
[/block]

[block:api-header]
{
  "title": "Full CustomCheerMeter Sample"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "class CustomCheerMeter: UIViewController {\n    let stackView: UIStackView = {\n        let stackView = UIStackView()\n        stackView.translatesAutoresizingMaskIntoConstraints = false\n        stackView.axis = .vertical\n        stackView.distribution = .fillEqually\n        stackView.alignment = .leading\n        return stackView\n    }()\n\n    let titleLabel: UILabel = {\n        let label = UILabel()\n        label.translatesAutoresizingMaskIntoConstraints = false\n        label.numberOfLines = 0\n        return label\n    }()\n\n    var optionButtons: [UIButton] = []\n\n    let model: CheerMeterWidgetModel\n\n    init(model: CheerMeterWidgetModel) {\n        self.model = model\n        super.init(nibName: nil, bundle: nil)\n    }\n\n    required init?(coder: NSCoder) {\n        fatalError(\"init(coder:) has not been implemented\")\n    }\n\n    override func loadView() {\n        view = stackView\n    }\n\n    override func viewDidLoad() {\n        super.viewDidLoad()\n\n        stackView.addArrangedSubview(titleLabel)\n\n        // Initializing UI elements with Model data\n        titleLabel.text = model.title\n        model.options.enumerated().forEach { index, option in\n            let optionButton = UIButton()\n            optionButton.translatesAutoresizingMaskIntoConstraints = false\n            optionButton.tag = index // Will be used to lookup option id later\n            optionButton.setTitle(\"\\(option.voteCount)\", for: .normal)\n            do {\n                let imageData = try Data(contentsOf: option.imageURL)\n                let image = UIImage(data: imageData)\n                optionButton.setBackgroundImage(image, for: .normal)\n            } catch {\n                print(error)\n            }\n            optionButton.addTarget(self, action: #selector(optionButtonHandler), for: .touchUpInside)\n            optionButtons.append(optionButton)\n            stackView.addArrangedSubview(optionButton)\n        }\n\n        model.delegate = self\n    }\n\n    @objc private func optionButtonHandler(sender: UIButton) {\n        guard model.options.count > sender.tag else { return }\n        model.submitVote(optionID: model.options[sender.tag].id)\n    }\n}\n\nextension CustomCheerMeter: CheerMeterWidgetModelDelegate {\n    func cheerMeterWidgetModel(\n        _ model: CheerMeterWidgetModel,\n        voteCountDidChange voteCount: Int,\n        forOption optionID: String\n    ) {\n        // This method is not guaranteed to be called on the Main thread\n        DispatchQueue.main.async {\n            guard let optionIndex = model.options.firstIndex(where: { $0.id == optionID }) else { return }\n            guard self.optionButtons.count > optionIndex else { return }\n            self.optionButtons[optionIndex].setTitle(\"\\(voteCount)\", for: .normal)\n        }\n    }\n\n    func cheerMeterWidgetModel(\n        _ model: CheerMeterWidgetModel,\n        voteRequest: CheerMeterWidgetModel.VoteRequest,\n        didComplete result: Result<CheerMeterWidgetModel.Vote, Error>\n    ) {\n        // To make your UI more responsive\n        // You may want to optimistically update your UI when the user votes\n        // While the throttled network request is being made\n        // You can use this method to validate your UI in case the request fails\n    }\n}",
      "language": "swift"
    }
  ]
}
[/block]