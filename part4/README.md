#创建家庭

```Objective-C
/**
 *  添加家庭
 *  @param name  添加的家庭名称
 *  @param homeLocation  家庭位置
 *  @param roomArr 房间集合
 *  @param progress  进度
 *  @param success 请求成功后的回调
 *  @param failure 请求失败后的回调
 *  请求成功回调后，可获取以下数据
 *  获取家庭数据    [UserManager shareInstance].home
 *  获取网络房间数据 [UserManager shareInstance].rooms
 *  获取网络设备数据 [UserManager shareInstance].devices
 *  获取所有房间数据（包含缓存+网络数据）  [UserManager shareInstance].roomsArray
 *  获取所有设备数据（包含缓存+网络数据）  [UserManager shareInstance].devicesArray
 {
    "homeLocation": "深圳",
    "name": "凉yi",
    "room": [{"roomName":"客厅","roomIcon":"asa.png"}]
 }
*/
+ (void)addHome:(NSString*)name homeLocation:(NSString *)homeLocation roomArr:(NSArray *)roomArr progress:(void (^)(NSProgress *uploadProgress))progress success:(void (^)(SYResponeHCHomeInfoResult *result))success failure:(void (^)(NSError *error))failure;
```

#得到用户家庭数据

```Objective-C
/**
 *  获取家庭房间及设备信息
 *  @param success              请求成功后的回调
 *  @param failure              请求失败后的回调
 *  请求成功回调后，可获取以下数据
 *  获取家庭数据    [UserManager shareInstance].home
 *  获取网络房间数据 [UserManager shareInstance].rooms
 *  获取网络设备数据 [UserManager shareInstance].devices
 *  获取所有房间数据（包含缓存+网络数据）  [UserManager shareInstance].roomsArray
 *  获取所有设备数据（包含缓存+网络数据）  [UserManager shareInstance].devicesArray
 example:
 [SYNetWorkManager homeList:^(SYResponeHCHomeInfoListResult * _Nonnull result) {
 if (result.hRA == 1) {
    NSLog(@"%@", [UserManager shareInstance].user.userId);
    NSLog(@"%@",[UserManager shareInstance].devicesArray);
    NSLog(@"%@",[UserManager shareInstance].home);
    NSLog(@"%@",[UserManager shareInstance].roomsArray);
    NSLog(@"%@",[UserManager shareInstance].defaultRoomId);
    }
 } failure:^(NSError * _Nonnull error) {

 }];
 */
+ (void)homeList:(void (^)(SYResponeHCHomeInfoListResult *result))success failure:(void (^)(NSError *error))failure;
```

#更新家庭信息

```Objective-C
/**
 *  修改家庭名称和家庭位置
 *  @param homeId               家庭id
 *  @param homeLocation         家庭位置(有就传值，没有就传空)
 *  @param name                 家庭名字
 *  @param success              请求成功后的回调
 *  @param failure              请求失败后的回调
 example:
 [SYNetWorkManager updateHomeWithHomeId:[UserManager shareInstance].home.hid homeLocation:@"" name:@"紫禁之巅" success:^(SYResponeHCStringResult * _Nonnull result) {
    if (result.hRA == 1) {

    }
 } failure:^(NSError * _Nonnull error) {

 }];
 */
+ (void)updateHomeWithHomeId:(int)homeId homeLocation:(NSString *)homeLocation name:(NSString *)name success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
```

#获取更新家庭mesh信息 (用户登录后需获取)
```Objective-C
/**
*  获取mesh文件信息 （用户登录后，获取本地群组数据，判断群组是否含有本地数据，如果有，就同步一下）
*  @param success              请求成功后的回调
*  @param failure              请求失败后的回调
*/
+ (void)getHomeMeshDetail:(void (^)(SYResponeHCDictionaryResult *result))success failure:(void (^)(NSError *error))failure;
```
