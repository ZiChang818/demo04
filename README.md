实验四_Intent



Button按钮setonclicklistenter监听点击事件触发隐式intent

定义WebView接收隐式intent加载URL



布局文件（activity_main.xml）

```
  <LinearLayout
        android:id="@+id/linearLayout"
        android:layout_width="251dp"
        android:layout_height="102dp"
        android:layout_marginStart="80dp"
        android:layout_marginTop="144dp"
        android:orientation="horizontal"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent"
        tools:context="com.lindroid.edittext.MainActivity"
        tools:ignore="MissingConstraints">

        <TextView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="URL：" />

        <EditText
            android:id="@+id/URL_content"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:hint="请输入待访问的网址！" />
    </LinearLayout>

    <Button
        android:id="@+id/browse_button"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="浏览该网址"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintHorizontal_bias="0.498"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toBottomOf="@+id/linearLayout"
        app:layout_constraintVertical_bias="0.183"
        tools:ignore="NotSibling" />

```

效果图示意：
![imag](https://github.com/ZiChang818/demo04/blob/master/demo%20photo/ui%E8%AE%BE%E8%AE%A1%E5%9B%BE.png)

![imag](https://github.com/ZiChang818/demo04/blob/master/demo%20photo/%E9%A1%B9%E7%9B%AEui%E6%9C%80%E7%BB%88%E5%AE%9E%E7%8E%B0%E5%9B%BE.png)


创建intent对象

```
        url = findViewById(R.id.URL_content);
        Button browse_bt = findViewById(R.id.browse_button);
        browse_bt.setOnClickListener(new View.OnClickListener() {
            public void onClick(View v) {
                // Code here executes on main thread after user presses button
                Intent intent = new Intent();
                intent.setAction(Intent.ACTION_VIEW);

                String link = url.getText().toString();
                if (!link.startsWith("https://")) {
                    link = "https://" + link;
                }
                Uri uri = Uri.parse(link);
                intent.setData(uri);
                startActivity(intent);
            }
        });
```





打开网页信息：

```
    public void OpenURL(View V) {
        Intent intent = new Intent();
        intent.setAction(Intent.ACTION_VIEW);

        String link = url.getText().toString();
        if (!link.startsWith("https://")) {
            link = "https://" + link;
        }
        Uri uri = Uri.parse(link);
        intent.setData(uri);
        startActivity(intent);
    }
```



创建webview对象来接受：

```
  webView = findViewById(R.id.webView);
        webView.setWebViewClient(new WebViewClient());
        webView.setWebChromeClient(new WebChromeClient());
```



接受intent：

```
    @Override
    public void onWindowFocusChanged(boolean hasFocus) {
        super.onWindowFocusChanged(hasFocus);
        webView.loadUrl(Objects.requireNonNull(getIntent().getData()).toString());
    }
```



项目实现图片：
![imag](https://github.com/ZiChang818/demo04/blob/master/demo%20photo/%E9%80%89%E6%8B%A9intent%E7%9A%84%E6%B5%8F%E8%A7%88%E5%99%A8.png)

![imag](https://github.com/ZiChang818/demo04/blob/master/demo%20photo/%E9%A1%B9%E7%9B%AE%E6%88%90%E5%8A%9F%E5%AE%9E%E7%8E%B0.png)
