title: Android 系统 WebView 使用
date: 2015-10-28 11:27:56
category: Android
tags:  WebView使用
description: Android开发时要经常用到webview，本文总结了一些WebView在使用中的技巧

---
### webView开启下载功能

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


### 为webview Http 请求添加 header

	Webview webview=new WebView(getActivity())
	Map<String, String> headers = new HashMap<>();
	headers.put("params", "this is params");	
	webView.loadUrl(getIntent().getStringExtra(WEBURL), headers);

### loaddata乱码问题

	webView.getSettings().setDefaultTextEncodingName("UTF -8");//设置默认为utf-8
    webView.loadData(data, "text/html; charset=UTF-8", null);//这种写法可以正确解码
	//webView.loadData(data, "text/html", "UTF -8");//API提供的标准用法，无法解决乱码问题
