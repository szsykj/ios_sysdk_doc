#集成SDK
本章介绍如何集成SDK,请使用Xcode来开发


#创建工程
在Xcode中建立你的工程，直接把SYSDK.framework拉进项目。


# 第三方pod支持

```Objective-C
pod 'MQTTClient'
pod 'MJExtension'
pod 'AliyunOSSiOS'
pod 'Bugly'
pod 'Realm'
pod 'AFNetworking', '~> 3.0'
pod 'CocoaAsyncSocket'
```

# Xcode 配置
在iOS 12以后不能直接获取手机Wi-Fi信息，需要在Xcode配置 ：项目Target -> Capabilities -> Access WiFi Information -> on

#SDK初始化

在AppDelegate中初始化sdk。

```Objective-C
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [SYSDKConfig defaultConfig].saveLog = NO;
    [SYSDKConfig defaultConfig].languageCode = @"en";
    [UserManager shareInstance];
    [EVONetStates shareInstance];
    return YES;
}
```

# SYSDK.bundle 配置及作用说明

SDK里设备配置多语言
```Objective-C
"pid_name" = "东芝吸顶灯";                 /**<设备名字*/
"pid_controlVC" = "00010104000D01Controller"; /**<控制页面控制器VC名称*/
"pid_deviceOn" = "打开";                  /**<设备打开描述*/
"pid_deviceOff" = "关闭";                 /**<设备关闭描述*/
"pid_device_icon" = "device_icon";                  /**<设备默认图标*/
"pid_deviceOn_icon" = "deviceOn_icon";                /**<设备打开图标*/
"pid_deviceOff_icon" = "deviceOff_icon";               /**<设备关闭图标*/
"pid_deviceAuto_icon" = "deviceAuto_icon";              /**<设备智能图标*/

"pid_status_redge_1" = "开灯";            /**<联动条件UI*/
"pid_status_fedge_0" = "关灯";            /**<联动条件UI*/
"pid_status1_redge_1" = "主灯开";         /**<联动条件UI*/
"pid_status2_redge_1" = "夜灯开";         /**<联动条件UI*/

"pid_onoff_1" = "开灯";                   /**<联动执行UI*/
"pid_onoff_0" = "关灯";                   /**<联动执行UI*/
"pid_onoff1_1" = "开主灯";                /**<联动执行UI*/
"pid_onoff2_1" = "开夜灯";                /**<联动执行UI*/

```
