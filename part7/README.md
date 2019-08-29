#设备定时模块

##获取设备的所有定时任务
```Objective-C
/**
 *  获取定时
 *  @param device               获取的定时设备
 *  @param success              请求成功后的回调
 *  @param failure              请求失败后的回调
 example:
 DeviceModel *device = [UserManager shareInstance].devicesArray[0];
 [SYNetWorkManager getTimingListWithDevice:device success:^(SYResponeHCTimerInfoResult * _Nonnull result) {
    if (result.hRA == 1) {
     }
 } failure:^(NSError * _Nonnull error) {
 }];
 */
+ (void)getTimingListWithDevice:(DeviceModel *)device success:(void (^)(SYResponeHCTimerInfoResult *result))success failure:(void (^)(NSError *error))failure;
```

##添加一个定时

```Objective-C
/**
 *  添加定时
 *  @param device               添加定时的设备
 *  @param name                 定时的名称
 *  @param repeat               循环次数
 *                                      对于 mode 为自定义时，每一位代表一周中的一天。
 *                                      最右边的位为低位，代表周一，最左边的位为高位，代表周日。
 *                                      0：标识该天不需要执行定时。
 *                                      1：标识该天需要执行定时。
 *                                      例如，自定义为周二、周四、周五需要执行定时，则可定义为：0011010
 *  @param action               执行的动作 如 {"onoff":1,"mode":2}
 *  @param year                 年
 *  @param month                月
 *  @param day                  日
 *  @param hour                 时
 *  @param min                  分
 *  @param success              请求成功后的回调
 *  @param failure              请求失败后的回调
 example:
 DeviceModel *device = [UserManager shareInstance].devicesArray[0];
 NSDictionary *dict = [NSDictionary dictionaryWithObjectsAndKeys:@"1",@"onoff",@"2",@"mode", nil];
 [SYNetWorkManager addTimingWithDevice:device name:@"定时4" repeat:@"1110000" action:dict year:2019 month:9 day:2 hour:8 min:55 success:^(SYResponeHCIntegerResult * _Nonnull result) {
    if (result.hRA == 1) {

    }
 } failure:^(NSError * _Nonnull error) {

 }];
 */
+ (void)addTimingWithDevice:(DeviceModel *)device name:(NSString *)name repeat:(NSString *)repeat  action:(NSDictionary *)action year:(int)year month:(int)month day:(int)day hour:(int)hour min:(int)min  success:(void (^)(SYResponeHCIntegerResult *result))success failure:(void (^)(NSError *error))failure;
```

##更新设备的定时任务

```Objective-C
/**
 *  编辑定时
 *  @param device               添加定时的设备
 *  @param timerId              需要修改的定时id
 *  @param name                 定时的名称
 *  @param repeat               循环次数
 *                              对于 mode 为自定义时，每一位代表一周中的一天。
 *                              最右边的位为低位，代表周一，最左边的位为高位，代表周日。
 *                              0：标识该天不需要执行定时。
 *                              1：标识该天需要执行定时。
 *                              例如，自定义为周二、周四、周五需要执行定时，则可定义为：0011010
 *  @param action               执行的动作 如 {"onoff":1,"mode":2}
 *  @param year                 年
 *  @param month                月
 *  @param day                  日
 *  @param hour                 时
 *  @param min                  分
 *  @param success              请求成功后的回调
 *  @param failure              请求失败后的回调
 example:
 DeviceModel *device = [UserManager shareInstance].devicesArray[0];
 NSDictionary *dict = [NSDictionary dictionaryWithObjectsAndKeys:@"1",@"onoff",@"2",@"mode", nil];
 [SYNetWorkManager updateTimingWithDevice:device timerId:890 name:@"定时炸弹" repeat:@"0000000" action:dict year:2019 month:10 day:10 hour:10 min:10 success:^(SYResponeHCIntegerResult * _Nonnull result) {
    if (result.hRA == 1) {

    }
 } failure:^(NSError * _Nonnull error) {

 }];
 */
+ (void)updateTimingWithDevice:(DeviceModel *)device timerId:(NSInteger)timerId name:(NSString *)name repeat:(NSString *)repeat  action:(NSDictionary *)action year:(int)year month:(int)month day:(int)day hour:(int)hour min:(int)min  success:(void (^)(SYResponeHCIntegerResult *result))success failure:(void (^)(NSError *error))failure;
```

##删除设备的某个定时任务


```Objective-C
/**
 *  删除设备定时
 *  @param timerId              定时id
 *  @param success              请求成功后的回调
 *  @param failure              请求失败后的回调
 example:
 [SYNetWorkManager deleteTimingWithTimerId:890 success:^(SYResponeHCStringResult * _Nonnull result) {
    if (result.hRA == 1) {

    }
 } failure:^(NSError * _Nonnull error) {

 }];
 */
+ (void)deleteTimingWithTimerId:(NSInteger)timerId success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
```

##更新设备的某个定时任务开启和关闭状态


```Objective-C
/**
 *  设置设备定时状态
 *  @param timerId              定时id
 *  @param status               需要设置的状态 （ 1：打开， 0：关闭）
 *  @param success              请求成功后的回调
 *  @param failure              请求失败后的回调
 example:
 [SYNetWorkManager controlTimingStatusWithTimerId:891 status:0 success:^(SYResponeHCIntegerResult * _Nonnull result) {
    if (result.hRA == 1) {
    }
 } failure:^(NSError * _Nonnull error) {

 }];
 */
+ (void)controlTimingStatusWithTimerId:(NSInteger)timerId status:(int)status success:(void (^)(SYResponeHCIntegerResult *result))success failure:(void (^)(NSError *error))failure;
```

##SYResponeTimerModel数据模型类
=======
#SYResponeTimerModel数据模型


| 字段名称       | 字段说明    | 类型  | 备注                                                                                       |
|------------|---------|-----|------------------------------------------------------------------------------------------|
| dtId       | 定时任务的ID | 数字  | \-                                                                                       |
| startInfo  | 启动的信息   | 文本  | \{"time":\{"year":2018,"month":7,"date":8,"hour":12,"min":48\},"trigger":\{"onoff":"0"\} |
| endInfo    | 结束的信息   | 文本  | \{"time":\{"year":2018,"month":7,"date":8,"hour":12,"min":48\},"trigger":\{"onoff":"0"\} |
| dtMode     | 模型      | 字符串 |  模型 once：一次性执行 every：每天 week：工作日 reset：周末 self：自定义                                       |
| dtDays     | 执行日期    | 字符串 |  对于 mode 为自定义时，每一位代表一周中的一天。<br> 最右边的位为低位，代表周一，最左边的位为高位，代表周日。 <br> 0：标识该天不需要执行定时。 <br> 1：标识该天需要执行定时。<br> 例如，自定义为周二、周四、周五需要执行定时，则为：0011010                                                                                    |
| createTime | 创建的时间   | 数字  | \-                                                                                       |
| userId     | 用户ID    | 数字  | \-                                                                                       |
| deviceId   | 设备ID    | 数字  | \-                                                                                       |
| dtStatus   | 任务的状态   | 数字  | 状态 1：打开， 0：关闭                                                                   |

