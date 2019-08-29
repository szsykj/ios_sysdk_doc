#添加智能

```Objective-C
/**
 *  新添加智能
 *  @param wisdom               智能（SYWisdom）模型 （参数解释相见模型）
 *  @param success              请求成功后的回调
 *  @param failure              请求失败后的回调
 example:
 - (void)addWisdom{
    DeviceModel *device = [UserManager shareInstance].devicesArray[0];
    SYWisdom * wisdom = [[SYWisdom alloc] init];
    SYResponeWisdom *resWisdom = [[SYResponeWisdom alloc] init];
    resWisdom.andOr = @"1";//执行条件 1 一起执行，2 满足其中一个就执行 默认@“1”
    resWisdom.hid = [NSString stringWithFormat:@"%ld",[UserManager shareInstance].home.hid]; //家庭ID
    resWisdom.wisdomName = @"你想取的智能名字，注意有长度要求1";
    resWisdom.supportHomePage = @"0";//是否在首页显示
    resWisdom.wisdomType = @"1";//智能类型 @"1":点击执行，@"2":设备联动执行，@"3":定时智能智能
    wisdom.wisdom = resWisdom;
    wisdom.wisdomConditions = [[NSMutableArray alloc] init];
    wisdom.wisdomImplements = [[NSMutableArray alloc] init];
    SYIntellingCondition *con1 =  [[WHO_PIDManager shareInstance]sy_intellingConditionWithDeviceModel:device][0];
    SYResponeWisdomConditions *condition = [[SYResponeWisdomConditions alloc] init];
    condition.appointment =  con1.mode;
    condition.conditionName = con1.name;
    condition.conditionType = con1.num;
//    condition.conditionValue = @"1";
    condition.did = device.deviceId;
    [wisdom.wisdomConditions addObject:condition];
    SYIntellingImplement *imp =[[WHO_PIDManager shareInstance]sy_intellingImplementWithDeviceModel:device][0];
    SYResponeWisdomImplements *implement = [[SYResponeWisdomImplements alloc] init];
    implement.implementType = @"2";
    implement.implementName = imp.cmdName;
    implement.implementValue = imp.cmdId;
    implement.did = device.deviceId;
    [wisdom.wisdomImplements addObject:implement];
    [SYNetWorkManager addNewSceneWithWisdom:wisdom success:^(SYResponeHCWisdomResult * _Nonnull result) {
        if (result.hRA == 1) {

        }
    } failure:^(NSError * _Nonnull error) {

    }];
 }
 */
+ (void)addNewSceneWithWisdom:(SYWisdom *)wisdom success:(void (^)(SYResponeHCWisdomResult *result))success failure:(void (^)(NSError *error))failure;
```

#删除智能

```Objective-C
/**
 *  删除智能
 *  @param wid                  智能Id
 *  @param success              请求成功后的回调
 *  @param failure              请求失败后的回调
 */
+ (void)deleteSceneWithWisdomId:(NSInteger)wid success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
```

#获取智能数据集合

```Objective-C
/**
 *  用户查看智能列表
 *  @param sceneType            获取智能的类型 0:首页不显示 1:首页显示 2:全部返回
 *  @param success              请求成功后的回调
 *  @param failure              请求失败后的回调
 */
+ (void)sceneListWithType:(int)sceneType success:(void (^)(SYResponeHCWisdomListResult *result))success failure:(void (^)(NSError *error))failure;
```


#开关智能

```Objective-C
/**
 *  智能操作
 *  @param wid                  智能Id
 *  @param status               状态,L(1~2) 1：打开， 0：关闭
 *  @param success              请求成功后的回调
 *  @param failure              请求失败后的回调
 */
+ (void)sceneOnOffWithWisdomId:(NSInteger)wid status:(int)status success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
```

#修改智能

```Objective-C
/**
 *  修改智能
 *  @param wisdom               智能（SYWisdom）模型 （参数解释相见模型）
 *  @param success              请求成功后的回调
 *  @param failure              请求失败后的回调
 - (void)updateWisdom:(SYWisdom *)wisdom{
    wisdom.wisdom.wisdomName = @"大黑山住在大黑山上" ;
    wisdom.wisdom.supportHomePage = @"1";
    SYResponeWisdomConditions *condition = wisdom.wisdomConditions[0];//需要修改的条件
    DeviceModel *device = [[UserManager shareInstance]selectUIDeviceDataFromDeviceId:condition.did];
    SYIntellingCondition *con1 =  [[WHO_PIDManager shareInstance]sy_intellingConditionWithDeviceModel:device][1];//选中的条件
    condition.appointment =  con1.mode;
    condition.conditionName = con1.name;
    SYResponeWisdomImplements *implement = wisdom.wisdomImplements[0];//需要修改的执行
    DeviceModel *device1 = [[UserManager shareInstance]selectUIDeviceDataFromDeviceId:implement.did];
    SYIntellingImplement *imp =[[WHO_PIDManager shareInstance]sy_intellingImplementWithDeviceModel:device1][1]; //选中的执行
    implement.implementName = imp.cmdName;
    implement.implementValue = imp.cmdId;
    NSLog(@"wisdom == %@",wisdom.mj_keyValues);
    [SYNetWorkManager updateSceneWithWisdom:wisdom success:^(SYResponeHCWisdomResult * _Nonnull result) {
        if (result.hRA == 1) {

        }
    } failure:^(NSError * _Nonnull error) {

    }];
 }
 */
+ (void)updateSceneWithWisdom:(SYWisdom *)wisdom success:(void (^)(SYResponeHCWisdomResult *result))success failure:(void (^)(NSError *error))failure;
```

#手动执行智能

```Objective-C  WHOIntelligentManager
/**
 * 手动执行智能
 * @param wid 智能id
 */
- (void)click:(NSInteger)wid;
```


