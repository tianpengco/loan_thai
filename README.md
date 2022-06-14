# 泰国项目整体流程说明
   本文档旨在说明泰国项目整体流程，包括需求介绍，接口文档，开发要求等。
   
   ## 开发需求
   开发需求为APP Android端项目开发，可以任意语言框架，包大小尽量不要超过40M，不然会影响推广，不要求提交市场上架，只需要完成功能开发自测，并通过我方的整体流程测试即可，需要移交代码完成交易。项目业务主要是针对泰国市场的金融借贷业务，业务不复杂，我方提供UI以及接口文档。
   
   ## UI地址
   [暂无（之后会提供蓝湖UI地址）](https://www.lanhu.com)
   
   ## 接口文档地址
   [接口swagger文档地址](http://www.speedcash.ltd/api-market/swagger-ui.html#/)
   
   ## 合作说明
   开发期为1-2个月，以签署合同开始，项目提交测试版本计算周期。提交测试版本之后支付百分之五十费用，测试完成移交代码支付剩余百分之五十费用。
   
   
   ## 需求说明：
   
   ### 需要对接SDK
   1.[OCR以及活体识别SDK--GuardianLivenessDetectionSDK]([https://www.lanhu.com](https://in.advance.ai/login))，对接简单，里面有详细的说明。OCR是走API的方式，可以参考接口文档，活体识别需要上报回调的活体照片。（登录需要账号，合同签署之后提供）
   2.[AppsFlyer SDK](https://www.appsflyer.com/cn/?utm_source=baidu&utm_medium=cpc&utm_campaign=pc-brandzone-title&utm_term=title) ,这是一个数据埋点，数据分析sdk，通过api上报各个节点，上报方案下面会有详细说明。（我方会提供apikey）
   3.需要通过AdvertisingIdClient获取googleId,然后在上报设备信息的时候上报该值,具体参考接口文档.
      依赖库:implementation 'androidx.ads:ads-identifier:1.0.0-alpha04'
   
   ### 需要权限说明
   ```Java
    <uses-permission
        android:name="android.permission.INTERNET" />
    <uses-permission
        android:name="android.permission.GET_ACCOUNTS" />
    <uses-permission
        android:name="android.permission.ACCESS_WIFI_STATE" />
    <uses-permission
        android:name="android.permission.READ_CONTACTS" />
    <uses-permission
        android:name="android.permission.ACCESS_COARSE_LOCATION" />
    <uses-permission
        android:name="android.permission.CAMERA" />
    <uses-permission
        android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission
        android:name="android.permission.READ_PHONE_STATE" />
    <uses-permission
        android:name="android.permission.ACCESS_NETWORK_STATE" />
    <uses-permission android:name="android.permission.RECEIVE_BOOT_COMPLETED" />
    <uses-permission
        android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    <uses-permission
        android:name="android.permission.READ_EXTERNAL_STORAGE" />
    <uses-permission
        android:name="android.permission.READ_SMS" />
    <uses-feature
        android:name="android.hardware.camera" />
    <uses-feature
        android:name="android.hardware.camera.autofocus" />
    <uses-permission
        android:name="android.permission.WAKE_LOCK" />
    <uses-permission
        android:name="com.google.android.finsky.permission.BIND_GET_INSTALL_REFERRER_SERVICE" />
    <uses-permission
        android:name="com.google.android.c2dm.permission.RECEIVE" />
    <!--上传图片-->
    <uses-permission android:name="android.permission.ACCESS_MEDIA_LOCATION"/>
    <uses-feature android:name="android.hardware.camera.autofocus" />
    <uses-feature android:name="android.hardware.camera" />
    <uses-permission android:name="android.permission.VIBRATE" />
    <uses-permission android:name="android.permission.FOREGROUND_SERVICE" />

   ```
   以上权限都需要，其中读取短信权限是为了读取用户所有短信记录并上报，有可能还会需要上报通话记录，这个需求待定。
   动态权限需要在用户第一次进入就全部一起申请一次，后面按需求再动态申请，初次申请样式大概如下：
   ![NO00 916](https://user-images.githubusercontent.com/14327254/173614554-e41269d3-30af-49fc-bb9d-d1cb35910006.jpg)

   
   ### 上报用户信息说明
   风控需求，要上报用户手机上的数据，包括用户的所有已安装APP信息，设备信息，通讯录，短信记录，定位信息，并且五分钟上报一次定位信息，包括当前网络环境，ip，经纬度（该定时器需要写在service里面）。还需要上报用户相册中照片的属性信息，包括拍摄时间，经纬度之类的，具体可以参考接口文档。
   
   ### 本地化说明
   因为运营地为泰国，所以需要语言为泰语，开发期间需要中文包测试，所以需要做多语言，上架需要泰语。语言的所有文案直接体现在ui
   里面，如果没有的话后期会单独提供。
   
   ### 埋点上报说明
   待补充
   
   ### 接口说明
   为了规避代码重复率审查以及破解安全，对接口路径进行加密处理，用项目名进行统一md5加密。然后将加密的项目名通过appCode字段放入请求头中统一传给后台，请求头中同时还需要添加source字段
   ，这个字段为会增加在后台大部分返回的接口键值中，为source__key样式，具体可以私下沟通。同时若已登录则在请求头中携带token字段。
   
   
   
