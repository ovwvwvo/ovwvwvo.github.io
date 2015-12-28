title: 给WebView添加Header
date: 2015-10-28 11:27:56
category: 技术
tags:  代码范例
description: 为 webview 的请求添加 header
---

为webview Http 请求添加 header

	Webview webview=new WebView(getActivity())
	Map<String, String> headers = new HashMap<>();
	headers.put("params", "this is params");	
	webView.loadUrl(getIntent().getStringExtra(WEBURL), headers);