title: Android系统WebView使用
date: 2015-10-28 11:27:56
category: 技术
tags:  WebView使用
description: Android开发时要经常用到webview，本文总结了一些WebView在使用中的技巧

---
##webView开启下载功能

有时候我们在App的webView中需要下载文件，当点击网页的下载链接发现没反应，其实是因为Android自带的Webview控件没有开启Download接口，在webView添加下面代码就可以了。

	  webView.setDownloadListener(new MDownLoadListener());
 	
      private class MDownLoadListener implements DownloadListener {

        @Override
        public void onDownloadStart(String url, String userAgent, String contentDisposition, String mimetype,
                                    long contentLength) {
            Uri uri = Uri.parse(url);
            Intent intent = new Intent(Intent.ACTION_VIEW, uri);
            startActivity(intent);
        }
    }


##为webview Http 请求添加 header

	Webview webview=new WebView(getActivity())
	Map<String, String> headers = new HashMap<>();
	headers.put("params", "this is params");	
	webView.loadUrl(getIntent().getStringExtra(WEBURL), headers);