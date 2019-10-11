#设备控制

#基础信息1

```Objective-C
 typedef NS_ENUM(UInt16, WHOCallBackCode) {
    WHOCallBackOK = 0x0000,             // 控制（获取/添加/删除倒计时）成功
    WHOCallBackTimeout = 0x0001,        // 控制（获取/添加/删除倒计时）超时
    WHOCallBackFail = 0x0002,           // 控制（获取/添加/删除倒计时）失败
 };

/*
 例子：WHONOTIFY
 type 为 refresh 时，可能返回
 device, wisdom, timing;
 device：设备变更
 wisdom：智能变更
 timing: 定时变更
 type 为 upgrade ，value = 1 表示成功，value ：0表示失败
 例子：
 {
    "type":"refresh",
    "value":"wisdom"，
    "id":"298"，
 }
 */

 typedef NS_ENUM(UInt16, WHOActionType) {
    WHOGET = 0x0001,                    // 获取设备详情
    WHOINFORM = 0x0002,                 // 设备详情上报
    WHOLOGIN = 0x0003,                  // 设备登录
    WHODISCONN = 0x0004,                // 设备离线
    WHODIFFLOGIN = 0x0005,              // 用户下线
    WHONOTIFY = 0x0006,                 // 消息通知
 };

 typedef void(^DataInteractionCallBack)(WHOCallBackCode Code,NSDictionary *dict);      //设备信息获取回调

 typedef void(^ReciveDataInteractionCallBack)(WHOActionType type,NSString *deviceId,NSDictionary *dict);  //监听设备上报状态
```



#设备交互操作（方式1）

```Objective-C   
/** SYWHODataInteractionManager
 *  公有接口方法(获取设备状态，控制设备状态，添加倒计时接口)
 *  @param dps               参照设备模型文档，组包控制
 *  @param actionType        执行操作的名称（获取设备状态:@"get",控制设备状态:@"control"）
 *  actionType:@"control" 控制设备
 *  NSDictionary *dps = [NSDictionary dictionaryWithObjectsAndKeys:[NSString stringWithFormat:@"%d",status],@"onoff",nil];
 *  NSDictionary *dps = [NSDictionary dictionaryWithObjectsAndKeys:[NSString stringWithFormat:@"%d",status],@"onoff1",nil];
 *  NSDictionary *dps = [NSDictionary dictionaryWithObjectsAndKeys:[NSString stringWithFormat:@"%d",status],@"onoff2",nil];
 *  NSDictionary *dps = [NSDictionary dictionaryWithObjectsAndKeys:[NSString stringWithFormat:@"%ld",brightness],@"set_brightness",nil];
 *  NSDictionary *dps = [NSDictionary dictionaryWithObjectsAndKeys:[NSString stringWithFormat:@"%ld",brightness],@"set_brightness_night",nil];
 *  NSDictionary *dps = [NSDictionary dictionaryWithObjectsAndKeys:[NSString stringWithFormat:@"%d",cct],@"set_cct",nil];
 *  NSDictionary *dps = [NSDictionary dictionaryWithObjectsAndKeys:[NSString stringWithFormat:@"%d",mode],@"set_mode",nil];
 *  actionType:@"get"     获取设备
 *  NSDictionary *dps = [NSDictionary dictionaryWithObject:@"all" forKey:@"attrTarget"];
 *  @param deviceId          设备did
 *  @param blockHandling     结果回调      (结果:WHOCallBackCode,参数:dict)

 get 回包，根据code == 1，获取存储在attrMaps字典里状态数据
 {
    attrMaps = {
                    brightness = 10;
                    cct = 0;
                    mode = 0;
                    status = 0;
                    status1 = 0;
                    status2 = 0;
                    "timing_period" = 2700;
                    "timing_period_remain" = 2700;
              };
    code = 1;
 }

 倒计时
 *  添加倒计时 actionType == @"addObject"
 *  action = @{@"onoff":@"1"};   //执行动作
 *  NSDictionary * taskDic =[[NSDictionary alloc] initWithObjectsAndKeys: @([deviceId integerValue]),@"id",@{@"hour":@(hour),@"min":@(min),@"sec":@(0)},@"time",action,@"trigger",nil];
 *  NSDictionary  * dps = [[NSDictionary alloc] initWithObjectsAndKeys: @"cd",@"role",taskDic,@"obj",@(0),@"updateNum",nil];
 *  删除倒计时 actionType == @"deleteObject"
 *  NSDictionary  * dps = [[NSDictionary alloc] initWithObjectsAndKeys: @"cd",@"role",@{@"id":@([deviceId integerValue])},@"obj",nil];

 *  查询倒计时 actionType == @"queryObject"
 *  NSDictionary  * dps = [[NSDictionary alloc] initWithObjectsAndKeys: @"cd",@"role",nil];
 查询倒计时回包
 body == {
             code = 1;                     //状态，code=1时解析倒计时。
             obj =  {
                        id = 19381;           //设备did
                        time = {
                                hour = 1;             //小时
                                min = 0;              //分钟
                                sec = 51;             //秒
                                };
                        trigger = {
                                onoff = 1;            //执行动作
                                };
                    };
             role = cd;                    //倒计时字段 @“cd”
 }
 
 *  查询设备MCU actionType == @"getMcuInfo"
 *  NSDictionary  * dps = @{};
 */
+ (void)publishDps:(NSDictionary *)dps actionType:(NSString *)actionType deviceId:(NSString *)deviceId callback:(DataInteractionCallBack)blockHandling;
```
#监听所有设备方法
```Objective-C 

/**
 *  监听所有设备方法
 *  @param blockHandling     结果回调
 *  WHOActionType type       消息类型
 *  NSString *deviceId,      消息来源
 *  NSDictionary *dict       消息明细（设备状态上报，设备上下线，账号离线，设备变更，定时变更，智能变更）
 */
+ (void)reciveDataInteractionCallback:(ReciveDataInteractionCallBack)blockHandling;
```
#监听设备状态
```Objective-C 
/**
 *  监听设备状态
 *  @param deviceId          设备Id
 *  @param blockHandling     结果回调
 *  WHOActionType type       消息类型
 *  NSDictionary *dict       消息明细 （设备状态上报，设备上下线）
 */
+ (void)reciveDataInteractionDeviceId:(NSString *)deviceId Callback:(ReciveDataInteractionCallBack)blockHandling;
```
#手机连接路由器时，开始发送心跳包和重连TCP
```Objective-C 

/**
 *  手机连接路由器时，开始发送心跳包和重连TCP
 */
+ (void)startConnectTCPAndKeepActive;
```
#手机断开路由器，停止发送心跳包和重连TCP
```Objective-C 
/**
 *  手机断开路由器，停止发送心跳包和重连TCP
 */
+ (void)stopConnectTcp;
```
#断开MQTT连接 （用户退出时，调用此方法）取消topics订阅
```Objective-C 

/**
 *  断开MQTT连接 （用户退出时，调用此方法）取消topics订阅
 */
+ (void)stopMQTTConnect;

```
#基础信息1
```Objective-C
 typedef NS_ENUM(UInt16, ControlCallBackCode) {
    ControlCallBackOK = 0x0000,             // 控制（获取/添加/删除倒计时）成功
    ControlCallBackTimeout = 0x0001,        // 控制（获取/添加/删除倒计时）超时
    ControlCallBackFail = 0x0002,           // 控制（获取/添加/删除倒计时）失败
 };
 typedef NS_ENUM(UInt16, WHOActionOneType) {
    WHOOneGET = 0x0001,                    // 获取设备详情
    WHOOneINFORM = 0x0002,                 // 设备详情上报
    WHOOneLOGIN = 0x0003,                  // 设备登录
    WHOOneDISCONN = 0x0004,                // 设备离线
    WHOOneDIFFLOGIN = 0x0005,              // 用户下线
    WHOOneNOTIFY = 0x0006,                 // 消息通知
 };
 typedef void(^ControlCallBack)(ControlCallBackCode controlCode);      //设备操作回调
 typedef void(^GETDeviceStatusCallBack)(ControlCallBackCode controlCode,DeviceModel *device);//设备信息获取回调
 typedef void(^DeviceStatusReceiveCallBack)(WHOActionOneType type,DeviceModel *device,NSDictionary *dict);//设备信息获取回调
 typedef void(^QueryCountDownCallBack)(ControlCallBackCode code,NSDictionary *body);            //查询定时回调
```

#设备交互操作（方式2）

```Objective-C
BaseControlModel
/**
 *  设备开关(公有控制方法)
 *  @param status            要执行的动作（开或关）
 *  @param deviceId          设备did
 *  @param blockHandling     控制结果回调(直接刷新设备模型onOff属性，SDK已更新)
 */
+ (void)setAllOnOrOFF:(BOOL)status deviceId:(NSString *)deviceId callback:(ControlCallBack)blockHandling;
```

#获取所有设备信息（方式2）

```Objective-C

/**
 *  获取所有设备信息
 *  @param blockHandling     获取结果回调(直接刷新设备模型onOff属性，SDK已更新)
 */
+ (void)getAllDevicesStatusCallback:(GETDeviceStatusCallBack)blockHandling;
```

#监听所有设备信息上报（系统消息）（方式2）

```Objective-C
/**
 *  监听所有设备信息上报（系统消息）
 *  @param blockHandling     获取结果回调(设备上线，离线，信息上报状态会调用此接口，直接刷新设备模型deviceStatus， onOff属性，SDK已更新)
 *  根据WHOActionOneType来判断上报信息类型，做对应的处理，如设备状态上报，设备上下线，账号离线，设备变更，定时变更，智能变更等
 */
+ (void)receiveAllDevicesStatusCallback:(DeviceStatusReceiveCallBack)blockHandling;
```

#添加倒计时（一个设备只会有一个倒计时）（方式2）

```Objective-C
/**
 *  添加倒计时（一个设备只会有一个倒计时）
 *  @param hour              倒计时：小时
 *  @param min               倒计时：分钟
 *  @param action            倒计时动作{"onoff":"1"}
 *  @param deviceId          设备did
 *  @param blockHandling     添加结果回调
 */
+ (void)addCountDownHour:(int)hour min:(int)min action:(NSDictionary *)action deviceId:(NSString *)deviceId callback:(ControlCallBack)blockHandling;
```

#删除倒计时（方式2）

```Objective-C
/**
 *  删除倒计时
 *  @param deviceId          设备did
 *  @param blockHandling     删除结果回调
 */
+ (void)deleteCountDownDeviceId:(NSString *)deviceId  callback:(ControlCallBack)blockHandling;
```

#查找倒计时（方式2）

```Objective-C
/**
 *  查找倒计时
 *  @param deviceId          设备did
 *  @param blockHandling     查询结果回调

 22000+sub错误码
 sub错误码    说明
 通用错误码（0~100）
 1          报文内容不正确，解析失败
 2          内存空间溢出
 固件更新错误码（100~130）
 100        固件更新host不正确
 101        固件更新用户名或密码不正确
 102        固件更新固件不存在
 103        固件更新下载超时
 104        固件更新进行中
 105        当前固件版本号不低于升级的版本号
 智能操作错误码固件更新错误码（130~160)
 131        智能已存在
 132        智能不存在
 body == {
            code = 1;                     //状态，code=1时解析倒计时。
            obj =  {
                    id = 19381;           //设备did
                    time = {
                            hour = 1;     //小时
                            min = 0;      //分钟
                            sec = 51;     //秒
                            };
                    trigger = {
                            onoff = 1;        //执行动作
                            };
                  };
            role = cd;                    //倒计时字段 @“cd”
        }
 */
+ (void)queryCountDownDeviceId:(NSString *)deviceId  callback:(QueryCountDownCallBack)blockHandling;
```

#手机连接路由器时，开始发送心跳包和重连TCP（方式2）

```Objective-C
/**
 *  手机连接路由器时，开始发送心跳包和重连TCP
 */
+ (void)startConnectTCPAndKeepActive;
```

#手机断开路由器，停止发送心跳包和重连TCP（方式2）

```Objective-C
/**
 *  手机断开路由器，停止发送心跳包和重连TCP
 */
+ (void)stopConnectTcp;
```

#断开MQTT连接 （用户退出时，调用此方法）取消topics订阅（方式2）

```Objective-C
/**
 *  断开MQTT连接 （用户退出时，调用此方法）取消topics订阅
 */
+ (void)stopMQTTConnect;
```
#设备交互操作具体模型控制（方式2）
```Objective-C 
 ToshibaCeilingLightModel
 typedef void(^receiveCeilingLightCallBack)(WHOActionOneType type,ToshibaCeilingLightModel *ceilingModel,NSDictionary *dict);
 typedef void(^GETToshibaCeilingLightStatusCallBack)(ControlCallBackCode controlCode,ToshibaCeilingLightModel *ceilingModel);//设备信息获取回调
 //@property (nonatomic,assign)BOOL status;//主灯、夜灯互斥，总开关开只打开主、夜灯的记忆状态
 @property (nonatomic,assign)BOOL status1;                  /**<主灯*/
 @property (nonatomic,assign)BOOL status2;                  /**<夜灯*/
 @property (nonatomic,assign)NSInteger brightness;          /**<主灯的亮度值*/
 @property (nonatomic,assign)NSInteger cct;                 /**<主灯的色温值*/
 @property (nonatomic,assign)NSInteger brightness_night;    /**<夜灯的亮度值*/
 @property (nonatomic,assign)NSInteger mode;                /**<灯的情景模式*/
 @property (nonatomic,assign)NSInteger cd_time;             /**
                                                                0~0xFF,
                                                                0 无倒计时或倒计时结束
                                                                ...
                                                                0x3C 还有 60 分钟(显示“60 分钟后消灯”)
                                                                0xFF 无效值
                                                            */
```
#监听设备上报状态数据（设备信息）（方式2）
```Objective-C 
/**
 *  监听设备上报状态数据（设备信息）
 *  @param deviceId          设备did
 *  @param blockHandling     控制结果回调
 */
+ (void)receiveToshibaCeilingLightWithDeviceId:(NSString *)deviceId callback:(receiveCeilingLightCallBack)blockHandling;
```
#查询设备上报状态数据（设备信息）（方式2）
```Objective-C 
/**
 *  查询设备上报状态数据
 *  @param deviceId          设备did
 *  @param blockHandling     控制结果回调
 */
+(void)getDeviceToshibaCeilingLightWithDeviceId:(NSString *)deviceId callback:(GETToshibaCeilingLightStatusCallBack)blockHandling;
```
#主灯开关（方式2）
```Objective-C 
/**
 *  主灯开关
 *  @param status            要执行的动作（开或关） 
 *  @param deviceId          设备did
 *  @param blockHandling     控制结果回调
 */
+ (void)setStatus1OnOrOFF:(BOOL)status deviceId:(NSString *)deviceId callback:(ControlCallBack)blockHandling;
```
#夜灯开关（方式2）
```Objective-C 
/**
 *  夜灯开关
 *  @param status            要执行的动作（开或关）
 *  @param deviceId          设备did
 *  @param blockHandling     控制结果回调
 */
+ (void)setStatus2OnOrOFF:(BOOL)status deviceId:(NSString *)deviceId callback:(ControlCallBack)blockHandling;
```
#设置主灯亮度值（方式2）
```Objective-C 
/**
 *  设置主灯亮度值
 *  @param brightness        要设置的主灯亮度
 *  @param deviceId          设备did
 *  @param blockHandling     控制结果回调
 */
+ (void)setBrightness:(NSInteger)brightness deviceId:(NSString *)deviceId callback:(ControlCallBack)blockHandling;
```
#设置夜灯亮度值（方式2）
```Objective-C 
/**
 *  设置夜灯亮度值
 *  @param brightness        要设置的夜灯亮度
 *  @param deviceId          设备did
 *  @param blockHandling     控制结果回调
 */
+ (void)setBrightnessNight:(NSInteger)brightness deviceId:(NSString *)deviceId callback:(ControlCallBack)blockHandling;
```
#设置主灯的色温值（方式2）
```Objective-C 
/**
 *  设置主灯的色温值
 *  @param cct               要设置主灯的色温值
 *  @param deviceId          设备did
 *  @param blockHandling     控制结果回调
 */
+ (void)setCCT:(int)cct deviceId:(NSString *)deviceId callback:(ControlCallBack)blockHandling;
```
#设置灯的情景模式（方式2）
```Objective-C
/**
 *  设置灯的情景模式
 *  @param mode              要设置主灯的情景模式
 *  @param deviceId          设备did
 *  @param blockHandling     控制结果回调
 */
+ (void)setMode:(int)mode deviceId:(NSString *)deviceId callback:(ControlCallBack)blockHandling;
```


#DeviceModel数据模型
| 字段名称            | 类型   | 字段说明                    |
|-----------------|------|-------------------------|
| userId          | 数字   | 用户id                    |
| homeId          | 数字   | 家庭id                    |
| roomId          | 数字   | 房间id                    |
| deviceId        | 数字   | 房间数量                    |
| createTime      | 数字   | 创建时间                    |
| roomName        | 字符串  | 房间名称                    |
| deviceMac       | 字符串  | 设备mac                   |
| deviceName      | 字符串  | 设备名称                    |
| deviceIcon      | 字符串  | 设备图片                    |
| deviceIp        | 字符串串 | 设备ip                    |
| classification  | 数字   | 网络类型                    |
| productId       | 字符串  | 产品id                    |
| localDid        | 数字   | 本地id                    |
| deviceVersion   | 字符串  | 设备版本                    |
| deviceWifiSSID  | 字符串  | 设备所连WiFi                |
| deviceStatus    | 数字   | 设备状态 0初始化 1在线 9离线       |
| userRole        | 数字   | 设备角色 1主人 2被分享者          |
| mainDeviceId    | 数字   | 网关id                    |
| isLocalDevice   | 布尔   | 是否本地设备                  |
| isIllegalDevice | 布尔   | 是否非法设备                  |
| isDaily           | 数字   | 是否常用设备 0不是 1是           |
| localStatus     | 数字   | 是否本地在线 0离线 1在线          |
