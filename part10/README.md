
#设备分享


##获取某个设备被分享的用户列表
```Objective-C
/**
*  获取某个设备被分享的用户列表
*  @param deviceId             设备ID
*  @param success              请求成功后的回调
*  @param failure              请求失败后的回调
*/
+ (void)getShareDeviceListWithDeviceId:(NSInteger)deviceId success:(void (^)(SYResponeHCUserShareListResult *result))success failure:(void (^)(NSError *error))failure;
```

##分享一个设备给某个用户
```Objective-C
/**
*  用户添加设备分享
*  @param deviceId             设备Id
*  @param userId               用户账号（手机号或者邮箱）
*  @param success              请求成功后的回调
*  @param failure              请求失败后的回调
*/
+ (void)shareDeviceWithDeviceId:(NSInteger)deviceId userId:(NSString *)userId success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
```

##移除分享
```Objective-C
/**
*  用户取消设备分享
*  @param userId               用户id
*  @param nudId                分享者记录ID
*  @param success              请求成功后的回调
*  @param failure              请求失败后的回调
*/

+ (void)deleteShareDeviceWithUserId:(NSInteger)userId nudId:(NSInteger)nudId success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;

```


##更新分享设备名字和设备图标
```Objective-C
/**
*  更新分享设备名字和设备图标
*  @param deviceId             设备ID
*  @param deviceName           设备注释名
*  @param deviceIcon           图片地址
*  @param success              请求成功后的回调
*  @param failure              请求失败后的回调
*/
+ (void)updateShareDeviceWithDeviceId:(NSInteger)deviceId deviceName:(NSString *)deviceName deviceIcon:(NSString *)deviceIcon success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
```

##更新分享设备所在房间
```Objective-C
/**
*  更新分享设备所在房间
*  @param deviceId             设备ID
*  @param roomId               房间ID
*  @param success              请求成功后的回调
*  @param failure              请求失败后的回调
*/
+ (void)updateShareDeviceRoomWithDeviceId:(NSInteger)deviceId roomId:(NSInteger)roomId success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;

```

#ShareItemBean 数据模型

| 字段名称              | 字段说明   | 类型  | 备注        |
|-------------------|--------|-----|-----------|
| userId            | 用户id   | 数字  | \-        |
| nudId             | 用户设备Id | 数字  | \-        |
| userName          | 用户名    | 字符串 | \-        |
| userAccountNumber | 用户账号   | 字符串 | 分为：手机号和邮箱 |
| iconUrl           | 用户头像地址 | 字符串 | \-        |

