# 实验四

## 实验内容
一、自定义WebView验证隐式Intent的使用
1、新建一个工程用来获取URL地址并启动Intent
2、新建一个工程使用WebView来加载URL

## 实验步骤

### 一、自定义WebView验证隐式Intent的使用

1、新建一个工程用来获取URL地址并启动Intent
首先编辑界面用于输入网址和按钮事件

```
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".MainActivity">

    <EditText
        android:id="@+id/url"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="输入网址格式为http://......"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintTop_toTopOf="parent" />
    <Button
        android:onClick="toweb"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="浏览该网页"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        app:layout_constraintTop_toBottomOf="@id/url"/>

</androidx.constraintlayout.widget.ConstraintLayout>
```

MainActivity.java
代码：

```
package com.example.webview;


import android.content.ComponentName;
import android.content.Intent;
import android.net.Uri;
import android.os.Bundle;
import android.view.View;
import android.widget.EditText;

import androidx.appcompat.app.AppCompatActivity;

public class MainActivity extends AppCompatActivity {
    private EditText url;
    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        url= (EditText) findViewById(R.id.url);

    }
    public void toweb(View source){
        Intent intent=new Intent();
        //跳一个系统的视图
        intent.setAction(Intent.ACTION_VIEW);
        intent.setData(Uri.parse(url.getText().toString()));
        Intent choose=Intent.createChooser(intent,"选择浏览器");
        startActivity(choose);
    }
}
```

实验结果截图：



[![TnVgRH.png](https://s4.ax1x.com/2021/12/20/TnVgRH.png)](https://imgtu.com/i/TnVgRH)



[![TnVWQA.png](https://s4.ax1x.com/2021/12/20/TnVWQA.png)](https://imgtu.com/i/TnVWQA)



[![TnVfsI.png](https://s4.ax1x.com/2021/12/20/TnVfsI.png)](https://imgtu.com/i/TnVfsI)



2、新建一个工程使用WebView来加载URL
webview.java


```
package com.example.webview;

import android.os.Bundle;
import android.webkit.WebSettings;
import android.webkit.WebView;
import android.webkit.WebViewClient;

import androidx.appcompat.app.AppCompatActivity;

public class webview extends AppCompatActivity {

    private WebView web;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_webview);
        web = (WebView) findViewById(R.id.web);
        //接收main页面界面传递过来的数据（网址)
        String url=getIntent().getDataString();

        WebSettings webSettings=web.getSettings();
        webSettings.setJavaScriptEnabled(true);
        webSettings.setSupportZoom(true);
        webSettings.setAllowFileAccess(true);
        webSettings.setAllowContentAccess(true);

        //让web加载网址
        web.loadUrl(url);

        //使用自己的web客户端打开网址
        web.setWebViewClient(new WebViewClient(){
            @Override
            public boolean shouldOverrideUrlLoading(WebView view, String url) {
                web.loadUrl(url);
                return true;
            }
        });
    }
}
```

实验结果截图：


[![TnV2zd.png](https://s4.ax1x.com/2021/12/20/TnV2zd.png)](https://imgtu.com/i/TnV2zd)
