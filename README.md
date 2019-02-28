### 埋点SDK集成说明

1. gradle添加依赖(后续上传maven仓库)

   ```
   implementation project(':lib_tracker')
   ```

2. application下初始化SDK

   ```
           val configuration = Configuration()
                   .setChannel("zhebao")
                   //SDK给一个用户分配一个ID
                   .setAppId("kls008956321") 
                   //.setDuration(60) 可配置上传时间
                   //.setTraceAllFragment(true) 是否自动收集fragment页面事件
                   //.setTraceView(true) 是否自动收集view事件
                   //.setTestMode(true) 测试模式-立即上传埋点
   	            //.setSupportMultiProcess(true) 是否收集其他进程埋点
           TrackerManager.instance.init(this, configuration)
   ```

### 埋点事件与收集维度

* 页面事件

  - page:页面

  - timestamp:打开页面时间戳
  - fromPage:上一个页面
  - duration:停留时长
  - network:网络情况

  ```
  {"page":"com.zbcm.demo.tracker.activity.MainActivity","timestamp":1550631267339,"fromPage":"com.zbcm.demo.tracker.activity.MainActivity","duration":27341,"network":"WIFI"}
  ```

* 基础事件

  * imei
  * androidId
  * language:语言
  * operator:运营商
  * appVersion:应用版本号
  * appName:应用名
  * channel:渠道
  * screenWidth:屏幕宽度
  * screenHeight:屏幕高度
  * model:系统版本
  * brand:设备名

  ```
  {"imei":"862756040681755","androidId":"7c22ce4ecbbe3c50","language":"zh","operator":"中国联通","appVersion":"1.0","appName":"APP统计","channel":"zhebao","screenWidth":1080,"screenHeight":2028}
  ```

* 定位

  * accuracy:定位精度
  * latitude:纬度
  * longitude:经度
  * countryCode:国家代号
  * countryName:国家名
  * adminArea:省/直辖市名
  * locality:城市名
  * subLocality:二级城市名/区
  * featureName:位置信息

  ```
  {"accuracy":2521.852,"latitude":31.205674,"longitude":121.60122199999999,"countryName":"中国","countryCode":"CN","adminArea":"上海市","locality":"上海市","subLocality":"浦东新区","featureName":"张江高科技园区亮景路上海浦东软件园(哈雷路)"}
  ```

* 点击事件

  * page:当前页面(子页面用分号间隔)
  * path:点击的控件所在路径
  * text:控件文本

  ```
  {"page":"com.zbcm.demo.tracker.activity.LoginActivity|com.zbcm.demo.tracker.fragment.LoginFragment","path":"ContentFrameLayout\/ConstraintLayout[0]\/FrameLayout[0]\/ConstraintLayout[0]\/AppCompatButton[0]#btLogin","text":"登    录","type":"Button"}
  ```
  
* 错误崩溃事件

  * reason:错误栈
  
  ```
  {"reason":"java.lang.ArithmeticException: divide by zero\n\tat com.zbcm.demo.tracker.activity.MainActivity$onCreate$9.onClick(MainActivity.kt:75)\n\tat android.view.View.performClick(View.java:6614)\n\tat android.view.View.performClickInternal(View.java:6591)\n\tat android.view.View.access$3100(View.java:786)\n\tat android.view.View$PerformClick.run(View.java:25948)\n\tat android.os.Handler.handleCallback(Handler.java:873)\n\tat android.os.Handler.dispatchMessage(Handler.java:99)\n\tat android.os.Looper.loop(Looper.java:201)\n\tat android.app.ActivityThread.main(ActivityThread.java:6806)\n\tat java.lang.reflect.Method.invoke(Native Method)\n\tat com.android.internal.os.RuntimeInit$MethodAndArgsCaller.run(RuntimeInit.java:547)\n\tat com.android.internal.os.ZygoteInit.main(ZygoteInit.java:873)\n"}
  ```
  
* App进入前台

  * time:事件时间
  
  ```
  {"time":1551323207274}
  ```

* App进入后台

  * time:事件时间
  * duration:留存时间
  
   ```
   {"time":1551323144808,"duration":22200}
   ```

* 手动埋点事件

  * name:事件名
  * variable:参数信息

  ```
  {"name":"click","variable":"{page=MainActivity, type=围棋}"}
  ```

  

  

  

  