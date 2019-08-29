#倒计时模块

##获取当前设备倒计时，查询设备获取，null代表当前设备无倒计时

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

##添加倒计时
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

##停止倒计时
```Objective-C
/**
 *  删除倒计时
 *  @param deviceId          设备did
 *  @param blockHandling     删除结果回调
 */
+ (void)deleteCountDownDeviceId:(NSString *)deviceId  callback:(ControlCallBack)blockHandling;
```



##设备端可能返回的错误码

| 错误码  | 说明              |
|----------------------|--------------
| 0                   | 通用错误               |
| 22131                    | 智能-倒计时CD已存在    |
| 22132                    | 智能-倒计时不存在      |
| 22133                    | 智能-倒计时不需要更新   |

