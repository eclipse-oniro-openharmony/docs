# 应用侧调用前端页面函数


应用侧可以通过[runJavaScript()](../reference/apis/js-apis-webview.md#runjavascript)方法调用前端页面的JavaScript相关函数。


在下面的示例中，点击应用侧的“runJavaScript”按钮时，来触发前端页面的htmlTest()方法。


- 前端页面有参。
  
  ```html
  <!-- index.html -->
  <!DOCTYPE html>
  <html>
  <body>
  <script>
      var param = "JavaScript Hello World!";
      function htmlTest(param) {
          console.log(param);
      }
  </script>
  </body>
  </html>
  ```

- 前端页面无参。
  
  ```html
  <!-- index.html -->
  <!DOCTYPE html>
  <html>
  <body>
  <script>
      function htmlTest() {
          console.info('JavaScript Hello World! ');
      }
  </script>
  </body>
  </html>
  ```


- 应用侧代码。
  
  ```ts
  // xxx.ets
  import web_webview from '@ohos.web.webview';
  
  @Entry
  @Component
  struct WebComponent {
    webviewController: web_webview.WebviewController = new web_webview.WebviewController();
  
    aboutToAppear() {
      // 配置Web开启调试模式
      web_webview.WebviewController.setWebDebuggingAccess(true);
    }

    build() {
      Column() {
        Button('runJavaScript')
          .onClick(() => {
            // 前端页面函数无参时，将param删除。
            this.webviewController.runJavaScript('htmlTest(param)');
          })
        Web({ src: $rawfile('index.html'), controller: this.webviewController})
      }
    }
  }
  ```

## 相关实例

针对Web组件开发，有以下相关实例可供参考：

- [JS注入与执行（ArkTS）（Full SDK）（API9）](https://gitee.com/openharmony/applications_app_samples/tree/master/code/BasicFeature/Web/RunJsInWeb)