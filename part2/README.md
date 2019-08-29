#用户登录

```Objective-C
/**
*  登录
*  @param countryCode        登录的区域编码  (中国86)
*  @param email              账号
*  @param password           密码
*  @param progress           进度
*  @param success            请求成功后的回调
*  @param failure            请求失败后的回调
*/
+(void)login:(NSString *)countryCode email:(NSString *)email pwd:(NSString *)password progress:(void (^)(NSProgress *uploadProgress))progress success:(void (^)(SYResponeHCUserResult *result))success failure:(void (^)(NSError *error))failure;
```

#用户注册

```Objective-C
/**
*  注册
*  @param countryCode        注册的区域编码  (中国86)
*  @param email              账号
*  @param password           密码
*  @param code               验证码
*  @param progress           进度
*  @param success            请求成功后的回调
*  @param failure            请求失败后的回调
*/
+(void)registerByEmail:(NSString *)countryCode email:(NSString *)email pwd:(NSString *)password code:(NSString *)code progress:(void (^)(NSProgress *uploadProgress))progress success:(void (^)(SYResponeHCUserResult *result))success failure:(void (^)(NSError *error))failure;
```

#获取注册验证码

```Objective-C
/**
*  获取验证码
*  @param email              账号
*  @param type               类型，@(1)注册账号时获取 @(2)忘记密码时获取 @(3)验证码登录
*  @param progress           进度
*  @param success            请求成功后的回调
*  @param failure            请求失败后的回调
*/
+(void)sendVerifyCodeByRegisterEmail:(NSString *)email type:(NSInteger)type progress:(void (^)(NSProgress *uploadProgress))progress success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
```

#重置密码

```Objective-C
/**
*  忘记密码
*  @param email              账号
*  @param password           密码
*  @param code               验证码
*  @param progress           进度
*  @param success            请求成功后的回调  "hRA": "1" 请求成功
*  @param failure            请求失败后的回调
*/
+ (void)resetPasswordByEmail:(NSString *)email pwd:(NSString *)password code:(NSString *)code progress:(void (^)(NSProgress *uploadProgress))progress success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
```

#退出登录

```Objective-C
/**
*  退出登录
*  @param success            请求成功后的回调
*  @param failure            请求失败后的回调
*/
+(void)loginOut:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
```

#更新用户名称

```Objective-C
/**
*  修改名称
*  @param nickname           修改后的名称
*  @param success            请求成功后的回调
*  @param failure            请求失败后的回调
*/
+ (void)updateNickname:(NSString *)nickname success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
```

#更新用户头像
##获取文件的token

```Objective-C
/**
*  获取文件的token             上传头像图片时需获取。
*  @param success            请求成功后的回调
*  @param failure            请求失败后的回调
*/
+ (void)getHeadImageToken:(void (^)(SYResponeHCDictionaryResult *result))success failure:(void (^)(NSError *error))failure
```
##上传图像

```Objective-C
/**
*  上传图像
*  @param objectKey          iconURL
*  @param progress           进度
*  @param success            请求成功后的回调
*  @param failure            请求失败后的回调
*/
+ (void)addHeadImage:(NSString*)objectKey progress:(void (^)(NSProgress *uploadProgress))progress success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
```


#更新用户密码

```Objective-C
/**
*  修改密码
*  @param newPassword        新密码
*  @param password           原密码
*  @param progress           进度
*  @param success            请求成功后的回调  "hRA": "1" 请求成功
*  @param failure            请求失败后的回调
*/
+ (void)resetNewPasswordByEmail:(NSString *)newPassword pwd:(NSString *)password progress:(void (^)(NSProgress *uploadProgress))progress success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
```

#提交用户意见反馈

```Objective-C
/**
*  意见反馈
*  @param contact            联系方式
*  @param feedbackContent    内容描述
*  @param feedbackPicture    图片链接
*  @param success            请求成功后的回调
*  @param failure            请求失败后的回调
*/
+ (void)addFeedback:(NSString *)contact feedbackContent:(NSString*)feedbackContent feedbackPicture:(NSString *)feedbackPicture  progress:(void (^)(NSProgress *uploadProgress))progress success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
```

#获取用户意见反馈

```Objective-C
/**
*  意见列表
*  @param success            请求成功后的回调
*  @param failure            请求失败后的回调
*/
+ (void)getFeedbackList:(void (^)(SYResponeHCFeedbackListResult *result))success failure:(void (^)(NSError *error))failure;
```

#User数据模型
| 字段名称          | 类型  | 字段说明   |
|---------------|-----|--------|
| userId        | 数字  | 用户id   |
| email         | 字符串 | 邮箱     |
| userName      | 字符串 | 用户名称   |
| createTime    | 数字  | 创建时间   |
| iconUrl       | 字符串 | 用户头像地址 |
| phone         | 字符串 | 手机号码   |
| hasCreateHome | 数字  | 是否创建家庭 |

#SYMyFeedback数据反馈模型
| 字段名称            | 类型  | 字段说明                   |
|-----------------|-----|------------------------|
| feedbacId       | 数字  | 反馈ID                   |
| createTime      | 数字  | 添加时间                   |
| feedbackStatus  | 数字  | 反馈状态；0：未处理，1：已处理，2：处理中 |
| feedbackContent | 字符串 | 反馈内容                   |
| systemReply     | 字符串 | 系统反馈                   |
