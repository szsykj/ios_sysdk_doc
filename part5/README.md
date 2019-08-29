#添加房间

```Objective-C
/**
 *  添加房间
 *  @param roomName             房间名称
 *  @param roomIcon             房间图片（本地基础图片名字）
 *  @param success              请求成功后的回调（返回房间ID：hRC）
 *  @param failure              请求失败后的回调
 example:
 [SYNetWorkManager addRoomName:@"黑山12222222" roomIcon:@"123452222.png" success:^(SYResponeHCIntegerResult * _Nonnull result) {
    if (result.hRA == 1) {

    }
 } failure:^(NSError * _Nonnull error) {

 }];
 */
+ (void)addRoomName:(NSString *)roomName roomIcon:(NSString *)roomIcon success:(void (^)(SYResponeHCIntegerResult *result))success failure:(void (^)(NSError *error))failure;
```


#更新房间信息

```Objective-C
/**
 *  修改房间
 *  @param roomName             房间名称
 *  @param roomIcon             房间图片（本地基础图片名字）
 *  @param roomId               需要修改的房间ID
 *  @param success              请求成功后的回调
 *  @param failure              请求失败后的回调
 example:
 [SYNetWorkManager updateRoomName:@"大黑山大山" roomIcon:@"12345.png" roomId:123 success:^(SYResponeHCStringResult * _Nonnull result) {
    if (result.hRA == 1) {

    }
 } failure:^(NSError * _Nonnull error) {

 }];
 */
+ (void)updateRoomName:(NSString *)roomName roomIcon:(NSString *)roomIcon  roomId:(NSInteger)roomId success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
```

#更新设备所属的房间

```Objective-C
/**
 *  房间添加设备
 *  @param roomId               房间Id
 *  @param devicesArr           设备DeviceModel集合
 *  @param success              请求成功后的回调（判断回调 code：1 ，全部成功，code：2 部分成功 需解析 外部直接调用数据库数据）
 *  @param failure              请求失败后的回调
 example:
 [SYNetWorkManager addDevicesToRoomWithRoomId:67671 devices:[UserManager shareInstance].devicesArray success:^(SYResponeHCDictionaryResult * _Nonnull result) {
    if (result.hRA == 1) {

    }
 } failure:^(NSError * _Nonnull error) {

 }];
 */
+ (void)addDevicesToRoomWithRoomId:(NSInteger)roomId devices:(NSArray<DeviceModel*>*)devicesArr success:(void (^)(SYResponeHCDictionaryResult *result))success failure:(void (^)(NSError *error))failure;
```

#删除房间

```Objective-C
/**
 *  删除房间
 *  @param roomId               房间Id
 *  @param success              请求成功后的回调（返回房间ID：hRC）
 *  @param failure              请求失败后的回调
 example:
 [SYNetWorkManager deleteRoomWithRoomId:6145 success:^(SYResponeHCIntegerResult * _Nonnull result) {
    if (result.hRA == 1) {

    }
 } failure:^(NSError * _Nonnull error) {

 }];
 */
+ (void)deleteRoomWithRoomId:(NSInteger)roomId success:(void (^)(SYResponeHCIntegerResult *result))success failure:(void (^)(NSError *error))failure;
```


#RoomListModel数据模型
| 字段名称       | 类型  | 字段说明            |
|------------|-----|-----------------|
| userId     | 数字  | 用户id            |
| hid     | 数字  | 家庭id            |
| roomId     | 数字  | 房间id            |
| roomName   | 字符串 | 房间名称            |
| roomIcon   | 字符串 | 设备数量            |
| roomType   | 数字  | 房间类型（1：默认 2：新增） |
| createTime | 数字  | 创建时间            |
| isReflish | 数字  | 是否刷新            |
