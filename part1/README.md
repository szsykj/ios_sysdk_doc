
#快速集成
本章介绍如何集成SDK,请使用Xcode来开发（部分新增接口未及时跟新，请参考SDK里接口注视说明）

#创建工程
在Xcode中建立你的工程，直接把SYSDK.framework和SYSDK.bundle拉进项目。

# 第三方pod支持
在Podfile文件中添加以下内容：

```Objective-C
pod 'YYModel'
pod 'SAMKeychain'    
pod 'MQTTClient'
pod 'MJExtension'
pod 'AliyunOSSiOS'
pod 'Realm'
pod 'AFNetworking', '~> 4.0'
pod 'CocoaAsyncSocket'
pod 'Reachability'
pod 'EspTouch', '~> 5.3.2'
```
然后在项目根目录下执行pod update/install命令，集成第三方库。

# Xcode 配置
在iOS 12以后不能直接获取手机Wi-Fi信息，需要在Xcode配置 ：项目Target -> Capabilities -> Access WiFi Information -> on
从 iOS 13 开始，如果没有开启地理位置权限，手机将获取不到正确的 SSID （在第已开启 Wi-Fi 权限的前提下）, 在此情况下，系统会默认返回 WLAN or Wi-Fi，以下是 Apple 的官方邮件说明
```Objective-C
As we announced at WWDC19, we're making changes to further protect user privacy and prevent unauthorized location tracking. Starting with iOS 13, the CNCopyCurrentNetworkInfo API will no longer return valid Wi-Fi SSID and BSSID information. Instead, the information returned by default will be: 

SSID: “Wi-Fi” or “WLAN” (“WLAN" will be returned for the China SKU)
BSSID: "00:00:00:00:00:00"
```
1.确认 app 已开启地理位置权限

2.确认通过系统方法获取的 BSSID 为 00:00:00:00:00:00 则认为是系统的默认返回，该结果不可用，需要开发者另外处理，比如手动输入 Wi-Fi 名称


# SDK初始化
在AppDelegate中初始化sdk。

```Objective-C
- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    [SYSDKConfig defaultConfig].server =  Toshiba_SERVER;//设置SDK服务器
    [SYSDKConfig defaultConfig].saveLog = NO;            //是否保存log
    [SYSDKConfig defaultConfig].languageCode = @"en";    //设置SDK配置语言
    [SYSDKConfig defaultConfig].hasMesh = YES;           //是否包含mesh
    [SYSDKConfig defaultConfig].verson = @"v2";         //设置服务器版本，默认设置为@"v1"
    [SYWHOUDPManager shareInstance].deviceType = 1;    //0:测试版设备  1:正式版本设备  2:全部
    [SYSDKConfig defaultConfig].hasVendors = YES;      //是否支持多厂商设备配网
    [SYSDKConfig defaultConfig].AppId = APPID;          //App在后台注册时产生的key，
    
    
    return YES;
}
```
# PID管理初始化
根据设备的数据模型文档，外部配置对应的PID，以日本东芝吸顶灯数据模型（Data Model）为例：
##日本东芝吸顶灯数据模型ToshibaCeilingLight创建
ToshibaCeilingLight模型继承BaseDeviceModel，
```Objective-C
//ToshibaCeilingLight.h
#import "BaseDeviceModel.h"
NS_ASSUME_NONNULL_BEGIN
@interface ToshibaCeilingLight : BaseDeviceModel
- (instancetype)init;
@end
```
```Objective-C
//  ToshibaCeilingLight.m
#import "ToshibaCeilingLight.h"
#import "NSBundle+SYSDK.h"

@implementation ToshibaCeilingLight
- (instancetype)init{
if (self = [super init]) {
[self initConfig];
[self initAutoIntelling];
}
return self;
}
- (void)initConfig{
self.deviceConfig                    = [[DeviceConfig alloc] init];
self.deviceConfig.pid                = @"00010104000D01";
self.deviceConfig.name               = [NSBundle sy_localizedStringForKey:@"00010104000D01_name"];
self.deviceConfig.controlVC          = [NSBundle sy_localizedStringForKey:@"00010104000D01_controlVC"];;
self.deviceConfig.childModel         = @"ToshibaCeilingLightModel";
self.deviceConfig.deviceOn           = [NSBundle sy_localizedStringForKey:@"00010104000D01_deviceOn"];
self.deviceConfig.deviceOff          = [NSBundle sy_localizedStringForKey:@"00010104000D01_deviceOff"];
self.deviceConfig.device_icon        = [NSBundle sy_localizedStringForKey:@"00010104000D01_device_icon"];
self.deviceConfig.deviceOn_icon      = [NSBundle sy_localizedStringForKey:@"00010104000D01_deviceOn_icon"];
self.deviceConfig.deviceOff_icon     = [NSBundle sy_localizedStringForKey:@"00010104000D01_deviceOff_icon"];
self.deviceConfig.deviceAuto_icon    = [NSBundle sy_localizedStringForKey:@"00010104000D01_deviceAuto_icon"];
self.deviceConfig.isHaveOnOff        = YES;
self.deviceConfig.isHaveMCU          = YES;
self.deviceConfig.isAutoCondition    = YES;
self.deviceConfig.isAutoImplement    = YES;
}
- (void)initAutoIntelling{
//联动条件
self.intelling = [[SYIntellingModel alloc] init];
[self.intelling addIntellingConditionUI:[NSBundle sy_localizedStringForKey:@"00010104000D01_status_redge_1"] name:@"status" mode:@"redge" num:@"1"];
[self.intelling addIntellingConditionUI:[NSBundle sy_localizedStringForKey:@"00010104000D01_status_fedge_0"] name:@"status" mode:@"fedge" num:@"0"];
[self.intelling addIntellingConditionUI:[NSBundle sy_localizedStringForKey:@"00010104000D01_status1_redge_1"] name:@"status1" mode:@"redge" num:@"1"];
[self.intelling addIntellingConditionUI:[NSBundle sy_localizedStringForKey:@"00010104000D01_status2_redge_1"] name:@"status2" mode:@"redge" num:@"1"];
//联动执行
[self.intelling addIntellingImplementUI:[NSBundle sy_localizedStringForKey:@"00010104000D01_onoff_1"] cmdName:@"onoff" cmdId:@"1"];
[self.intelling addIntellingImplementUI:[NSBundle sy_localizedStringForKey:@"00010104000D01_onoff_0"] cmdName:@"onoff" cmdId:@"0"];
[self.intelling addIntellingImplementUI:[NSBundle sy_localizedStringForKey:@"00010104000D01_onoff1_1"] cmdName:@"onoff1" cmdId:@"1"];
[self.intelling addIntellingImplementUI:[NSBundle sy_localizedStringForKey:@"00010104000D01_onoff2_1"] cmdName:@"onoff2" cmdId:@"1"];
}
@end
```
##日本东芝吸顶灯数据模型ToshibaCeilingLight初始化
```Objective-C
- (void)addPID{
ToshibaCeilingLight *light = [[ToshibaCeilingLight alloc] init];
[[WHO_PIDManager shareInstance]addPIDManagerWithPID:@"00010104000D01" baseDeviceModel:light];
}
```

# SYSDK.bundle 配置及作用说明

SDK里设备配置多语言
SYSDK.bundle 键值对是根据设备的设备模型来设置
```Objective-C
"pid_name" = "东芝吸顶灯";                       /**<设备名字            外部主页面UI显示时使用。       */
"pid_controlVC" = "00010104000D01Controller";  /**<控制页面控制器VC名称  外部主页面进入设备详情页面时使用 */
"pid_deviceOn" = "打开";                        /**<设备打开描述         外部主页面UI显示时使用。       */
"pid_deviceOff" = "关闭";                       /**<设备关闭描述         外部主页面UI显示时使用。       */
"pid_device_icon" = "device_icon";             /**<设备默认图标         外部主页面UI显示时使用。       */
"pid_deviceOn_icon" = "deviceOn_icon";         /**<设备打开图标         外部主页面UI显示时使用。       */
"pid_deviceOff_icon" = "deviceOff_icon";       /**<设备关闭图标         外部主页面UI显示时使用。       */
"pid_deviceAuto_icon" = "deviceAuto_icon";     /**<设备智能图标         外部智能详情面UI显示时使用。    */

"pid_status_redge_1" = "开灯";                  /**<联动条件UI          外部智能UI显示时使用。         */
"pid_status_fedge_0" = "关灯";                  /**<联动条件UI          外部智能UI显示时使用。         */
"pid_status1_redge_1" = "主灯开";               /**<联动条件UI          外部智能UI显示时使用。         */
"pid_status2_redge_1" = "夜灯开";               /**<联动条件UI          外部智能UI显示时使用。         */

"pid_onoff_1" = "开灯";                         /**<联动执行UI          外部智能UI显示时使用。         */
"pid_onoff_0" = "关灯";                         /**<联动执行UI          外部智能UI显示时使用。         */
"pid_onoff1_1" = "开主灯";                      /**<联动执行UI          外部智能UI显示时使用。         */
"pid_onoff2_1" = "开夜灯";                      /**<联动执行UI          外部智能UI显示时使用。         */
```

