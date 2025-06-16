---
title: Building a Social Embed Widget
excerpt: ''
deprecated: false
hidden: false
metadata:
  title: Building a Social Embed Widget | Android SDK | LiveLike
  description: >-
    This is a guide on building a Social Embed Widget for Android applications.
    Check out the Social Embed Widget Model to learn more.
  robots: index
next:
  description: ''
---
[block:callout]
{
  "type": "info",
  "title": "Minimum SDK version",
  "body": "2.29"
}
[/block]
This is a guide on building a custom Social Embed Widget. For an overview of the Custom Widget UI system see [Custom Widget UI](doc:custom-widget-ui). 
[block:api-header]
{
  "title": "Social Embed Widget Model"
}
[/block]
***Social Embed Data(object of LiveLikeWidget class)***
The Social Embed Data provides data about the Social Embed Widget such as the oembed provider url, provider name, html and many more.


The model also provides metadata about the widget such as the Date that it was created or the timeout duration set by the Producer.
[block:api-header]
{
  "title": "Sample Social Embed Widget"
}
[/block]

[block:code]
{
  "codes": [
    {
      "code": "class CustomSocialEmbed: ConstraintLayout {\n    var socialEmbedWidgetModel: SocialEmbedWidgetModel? = null\n    private lateinit var binding: CustomSocialEmbedBinding\n\n    constructor(context: Context) : super(context) {\n        init()\n    }\n\n    constructor(context: Context, attrs: AttributeSet) : super(context, attrs) {\n        init()\n    }\n\n    constructor(context: Context, attrs: AttributeSet, defStyle: Int) : super(\n        context,\n        attrs,\n        defStyle\n    ) {\n        init()\n    }\n\n    private fun init() {\n        binding = CustomSocialEmbedBinding.inflate(LayoutInflater.from(context), this@CustomSocialEmbed, true)\n    }\n\n\n    @SuppressLint(\"SetJavaScriptEnabled\")\n    override fun onAttachedToWindow() {\n        super.onAttachedToWindow()\n        socialEmbedWidgetModel?.widgetData?.let { liveLikeWidget ->\n            liveLikeWidget.socialEmbedItems?.get(0)?.let { oembed ->\n                binding.webView.settings.javaScriptEnabled = true\n                binding.webView.settings.domStorageEnabled = true\n\n\n                binding.webView.loadDataWithBaseURL(\n                    oembed.oEmbed.providerUrl,\n                    oembed.oEmbed.html, \"text/html\", \"utf-8\", \"\"\n                )\n\n                binding.webView.webViewClient = object : WebViewClient() {\n\n                    override fun onPageFinished(view: WebView?, url: String?) {\n                        super.onPageFinished(view, url)\n\n                    }\n\n                    override fun onPageCommitVisible(view: WebView?, url: String?) {\n                        super.onPageCommitVisible(view, url)\n                    }\n\n                    override fun onLoadResource(view: WebView?, url: String?) {\n                        super.onLoadResource(view, url)\n                    }\n\n                    override fun shouldInterceptRequest(\n                        view: WebView?,\n                        request: WebResourceRequest?\n                    ): WebResourceResponse? {\n                        return super.shouldInterceptRequest(view, request)\n                    }\n\n                    override fun shouldOverrideUrlLoading(\n                        view: WebView?,\n                        request: WebResourceRequest?\n                    ): Boolean {\n                        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) {\n                            request?.url?.let { url ->\n                                    val universalLinkIntent =\n                                        Intent(Intent.ACTION_VIEW, Uri.parse(url.toString())).setFlags(\n                                            Intent.FLAG_ACTIVITY_NEW_TASK)\n                                    if (universalLinkIntent.resolveActivity(context.packageManager) != null) {\n                                        ContextCompat.startActivity(context, universalLinkIntent, Bundle.EMPTY)\n                                    }\n\n                            }\n                        }\n                        return true\n                    }\n                }\n            }\n        }\n    }\n}",
      "language": "kotlin"
    }
  ]
}
[/block]