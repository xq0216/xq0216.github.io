---
layout: post
title: native app调用webview中的js方法获取返回值
categories: []
tags: [javascript]
published: True

---

融合app中，js与native方法之间的相互调用很常见。Android系统默认提供了这种支持，实现起来比较简单。iOS上实现就稍微复杂一点，所以我在iOS上直接使用了已经封装好的开源库[EasyJSWebView](https://github.com/dukeland/EasyJSWebView)。

在android上，js调用java方法一切安好，但java调用直接js方法无法取得返回值，这个设计比较搞笑。于是只好曲线救国，通过一点小技巧来实现java调用js获得返回值，思路如下：

使用alert传值，js方法将返回值alert出来，java测通过覆写webview的onJsAlert来捕获alert信息，取得返回值。

*js代码示例如下：*

	//android使用alert传值
	android && alert(JSON.stringify(result));
	//iOS正常返回
    return JSON.stringify(result);

*java代码示例：*

	@Override
        public boolean onJsAlert(WebView view, String url, String message, JsResult result) {
            String result ＝ message;
            //此处的message就是我们想要的返回值
        }

这种方法的缺点是只能返回字符串类型，如果想要返回更复杂的信息，可以使用json字符串来包装。