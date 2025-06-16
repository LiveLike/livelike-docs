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
> 📘 Minimum SDK version
>
> 2.29

This is a guide on building a custom Social Embed Widget. For an overview of the Custom Widget UI system see [Custom Widget UI](doc:custom-widget-ui). 

## Social Embed Widget Model

***Social Embed Data(object of LiveLikeWidget class)***\
The Social Embed Data provides data about the Social Embed Widget such as the oembed provider url, provider name, html and many more.

The model also provides metadata about the widget such as the Date that it was created or the timeout duration set by the Producer.

## Sample Social Embed Widget

```kotlin
class CustomSocialEmbed: ConstraintLayout {
    var socialEmbedWidgetModel: SocialEmbedWidgetModel? = null
    private lateinit var binding: CustomSocialEmbedBinding

    constructor(context: Context) : super(context) {
        init()
    }

    constructor(context: Context, attrs: AttributeSet) : super(context, attrs) {
        init()
    }

    constructor(context: Context, attrs: AttributeSet, defStyle: Int) : super(
        context,
        attrs,
        defStyle
    ) {
        init()
    }

    private fun init() {
        binding = CustomSocialEmbedBinding.inflate(LayoutInflater.from(context), this@CustomSocialEmbed, true)
    }


    @SuppressLint("SetJavaScriptEnabled")
    override fun onAttachedToWindow() {
        super.onAttachedToWindow()
        socialEmbedWidgetModel?.widgetData?.let { liveLikeWidget ->
            liveLikeWidget.socialEmbedItems?.get(0)?.let { oembed ->
                binding.webView.settings.javaScriptEnabled = true
                binding.webView.settings.domStorageEnabled = true


                binding.webView.loadDataWithBaseURL(
                    oembed.oEmbed.providerUrl,
                    oembed.oEmbed.html, "text/html", "utf-8", ""
                )

                binding.webView.webViewClient = object : WebViewClient() {

                    override fun onPageFinished(view: WebView?, url: String?) {
                        super.onPageFinished(view, url)

                    }

                    override fun onPageCommitVisible(view: WebView?, url: String?) {
                        super.onPageCommitVisible(view, url)
                    }

                    override fun onLoadResource(view: WebView?, url: String?) {
                        super.onLoadResource(view, url)
                    }

                    override fun shouldInterceptRequest(
                        view: WebView?,
                        request: WebResourceRequest?
                    ): WebResourceResponse? {
                        return super.shouldInterceptRequest(view, request)
                    }

                    override fun shouldOverrideUrlLoading(
                        view: WebView?,
                        request: WebResourceRequest?
                    ): Boolean {
                        if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.LOLLIPOP) {
                            request?.url?.let { url ->
                                    val universalLinkIntent =
                                        Intent(Intent.ACTION_VIEW, Uri.parse(url.toString())).setFlags(
                                            Intent.FLAG_ACTIVITY_NEW_TASK)
                                    if (universalLinkIntent.resolveActivity(context.packageManager) != null) {
                                        ContextCompat.startActivity(context, universalLinkIntent, Bundle.EMPTY)
                                    }

                            }
                        }
                        return true
                    }
                }
            }
        }
    }
}
```
