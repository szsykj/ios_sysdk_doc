#集成SDK
本章介绍如何集成SDK,请使用Android studio编辑器来开发


#创建工程
在Android Studio中建立你的工程，并在libs文件夹中添加SykjSmartSdk_v1.0.0.aar文件。


# build.gradle 配置
build.gradle 文件里添加集成准备中下载的dependencies 依赖库。  
```java
implementation (name:'SykjSmartSdk_v1.0.0, ext:'aar')

implementation 'com.squareup.retrofit2:retrofit:2.4.0'
implementation 'com.squareup.okhttp3:logging-interceptor:3.11.0'
implementation 'org.eclipse.paho:org.eclipse.paho.client.mqttv3:1.2.0'
implementation 'org.eclipse.paho:org.eclipse.paho.android.service:1.1.1'
implementation 'com.tencent:mmkv:1.0.10'
implementation 'org.greenrobot:eventbus:3.1.1'
implementation 'com.google.code.gson:gson:2.8.3'
implementation 'org.litepal.android:java:3.0.0'
implementation 'com.aliyun.dpa:oss-android-sdk:+'

```

# AndroidManifest.xml 配置
在Androidmanifest中添加以下权限及服务
```java
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.ACCESS_NETWORK_STATE" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.FLASHLIGHT" />

<service android:name="org.eclipse.paho.android.service.MqttService" />
```
#SDK初始化

在application中初始化sdk后，使用sdk中对外提供的接口(具体接口使用参考demo实例)

```java
public class SykjApplication extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
        SYSdk.init(this);
    }
}
```

