# SYSDK

### 简介  
#### SDK配置
1.直接把Demo里的SYSDK.framework进项目。
2.第三方pod支持：
pod 'MQTTClient'
pod 'MJExtension'
pod 'AliyunOSSiOS'
pod 'Bugly'
pod 'Realm'
pod 'AFNetworking', '~> 3.0'
pod 'CocoaAsyncSocket'
##### 1. SYSDKConfig.h 
@property (copy, nonatomic, nullable) NSString *languageCode; SDK语言设置，外部调用是设置语言，默认英语:en   中文：zh  日语：ja
@property (nonatomic, assign)BOOL saveLog;是否保存log信息到本地，yes表示保存，no表示不保存，默认为no。
##### 2.UserManager.h
外部使用数据
@property (nonatomic,strong)User *user;   当前用户
@property (nonatomic,strong)HomeListModel *home;  当前家庭。
@property (nonatomic,strong)NSMutableArray<RoomListModel *> *roomsArray; 当前房间数据集合
@property (nonatomic,strong)NSMutableArray<DeviceModel *> *devicesArray;   当前设备数据集合
/**
*  刷新数据库和数据缓存
*/
- (void)reflishDataBase;
/**
*  刷新家庭（增，改）
*/
- (void) updateHome:(HomeListModel *)home;

/**
*  刷新房间数据库和房间数据缓存（增，改）
*/
- (void) reflishUIRoomData:(RoomListModel *)room;
/**
*  删除房间数据库和房间数据缓存（删除）
*/
- (void) deleteRoomDataWithRoomId:(NSInteger)roomId;
/**
*  刷新设备数据库和设备数据缓存（增，改）
*/
- (void)reflishUIDevicesData:(DeviceModel *)device;

/**
*  刷新设备数据库和设备数据缓存（增）
*/
- (void) addUIDevicesData:(AddDeviceDTOList*)addDevice;

/**
*  根据房间ID获取房间model
*/
- (RoomListModel*) selectUIRoomDataFromRoomId:(NSString *)roomId;
/**
*  根据设备ID获取设备model
*/
- (DeviceModel*) selectUIDeviceDataFromDeviceId:(NSString *)deviceId;
/**
*  根据房间ID获取设备Array
*/
- (NSArray<DeviceModel*>*) selectUIDeviceDataFromRoomId:(NSString *)roomId;

##### 3.User.h
@property (nonatomic,copy)NSString *userId;
@property (nonatomic,copy)NSString *loginToken;     登录token
@property (nonatomic,copy)NSString *email;
@property (nonatomic,copy)NSString *password;
@property (nonatomic,copy)NSString *createTime;
@property (nonatomic,copy)NSString *mqttAddress;
@property (nonatomic,copy)NSString *mqttPort;
@property (nonatomic,copy)NSString *mqttUsername;
@property (nonatomic,copy)NSString *mqttPassword;
@property (nonatomic,copy)NSString *userName;
@property (nonatomic,copy)NSString *iconUrl;
@property (nonatomic,copy)NSString *cellIphone;
@property (nonatomic,assign)BOOL hasCreateHome;       /**<是否创建家庭*/

##### 4.SYNetWorkManager.h 

/**
*  登录
*  @param countryCode   登录的区域编码  (中国86)
*  @param email   账号
*  @param password  密码
*  @param progress  进度
*  @param success 请求成功后的回调
*  @param failure 请求失败后的回调
*/
+(void)login:(NSString *)countryCode email:(NSString *)email pwd:(NSString *)password progress:(void (^)(NSProgress *uploadProgress))progress success:(void (^)(SYResponeHCUserResult *result))success failure:(void (^)(NSError *error))failure;
/**
*  注册
*  @param countryCode   注册的区域编码  (中国86)
*  @param email   账号
*  @param password  密码
*  @param code      验证码
*  @param progress  进度
*  @param success 请求成功后的回调
*  @param failure 请求失败后的回调
*/
+(void)registerByEmail:(NSString *)countryCode email:(NSString *)email pwd:(NSString *)password code:(NSString *)code progress:(void (^)(NSProgress *uploadProgress))progress success:(void (^)(SYResponeHCUserResult *result))success failure:(void (^)(NSError *error))failure;

/**
*  获取验证码
*  @param email   账号
*  @param type      类型，@(1)注册账号时获取 @(2)忘记密码时获取 @(3)验证码登录
*  @param progress  进度
*  @param success 请求成功后的回调
*  @param failure 请求失败后的回调
*/
+(void)sendVerifyCodeByRegisterEmail:(NSString *)email type:(NSInteger)type progress:(void (^)(NSProgress *uploadProgress))progress success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
/**
*  忘记密码
*  @param email   账号
*  @param password  密码
*  @param code      验证码
*  @param progress  进度
*  @param success 请求成功后的回调  "hRA": "1" 请求成功
*  @param failure 请求失败后的回调
*/
+ (void)resetPasswordByEmail:(NSString *)email pwd:(NSString *)password code:(NSString *)code progress:(void (^)(NSProgress *uploadProgress))progress success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
/**
*  修改密码
*  @param newPassword   新密码
*  @param password  原密码
*  @param progress  进度
*  @param success 请求成功后的回调  "hRA": "1" 请求成功
*  @param failure 请求失败后的回调
*/
+ (void)resetNewPasswordByEmail:(NSString *)newPassword pwd:(NSString *)password progress:(void (^)(NSProgress *uploadProgress))progress success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
/**
*  账号是否可用（是否注册）
*  @param account   账号
*  @param progress  进度
*  @param success 请求成功后的回调  "hRA": "1" 请求成功   "hRC": "1" 账户存在  "hRC": "0" 账户不存在
*  @param failure 请求失败后的回调
*/
+(void)checkAccount:(NSString *)account progress:(void (^)(NSProgress *uploadProgress))progress success:(void (^)(SYResponeHCBOOLResult *result))success failure:(void (^)(NSError *error))failure;
/**
*  退出登录
*  @param success 请求成功后的回调
*  @param failure 请求失败后的回调
*/
+(void)loginOut:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;

/**
*  修改名称
*  @param nickname  修改后的名称
*  @param success 请求成功后的回调
*  @param failure 请求失败后的回调
*/
+ (void)updateNickname:(NSString *)nickname success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
/**
*  意见反馈
*  @param contact  联系方式
*  @param feedbackContent  内容描述
*  @param feedbackPicture  图片链接
*  @param success 请求成功后的回调
*  @param failure 请求失败后的回调
*/
+ (void)addFeedback:(NSString *)contact feedbackContent:(NSString*)feedbackContent feedbackPicture:(NSString *)feedbackPicture  progress:(void (^)(NSProgress *uploadProgress))progress success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
/**
*  意见列表
*  @param success 请求成功后的回调
*  @param failure 请求失败后的回调
*/
+ (void)getFeedbackList:(void (^)(SYResponeHCFeedbackListResult *result))success failure:(void (^)(NSError *error))failure;
/**
*  获取文件的token 上传头像图片时需获取。
*  @param success 请求成功后的回调
*  @param failure 请求失败后的回调
*/
+ (void)getHeadImageToken:(void (^)(SYResponeHCDictionaryResult *result))success failure:(void (^)(NSError *error))failure;
/**
*  上传图像
*  @param objectKey  iconURL
*  @param progress  进度
*  @param success 请求成功后的回调
*  @param failure 请求失败后的回调
*/
+ (void)addHeadImage:(NSString*)objectKey progress:(void (^)(NSProgress *uploadProgress))progress success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
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
/**
*  获取家庭房间及设备信息
*  @param success 请求成功后的回调
*  @param failure 请求失败后的回调
*  请求成功回调后，可获取以下数据
*  获取家庭数据    [UserManager shareInstance].home
*  获取网络房间数据 [UserManager shareInstance].rooms
*  获取网络设备数据 [UserManager shareInstance].devices
*  获取所有房间数据（包含缓存+网络数据）  [UserManager shareInstance].roomsArray
*  获取所有设备数据（包含缓存+网络数据）  [UserManager shareInstance].devicesArray
*/
+ (void)homeList:(void (^)(SYResponeHCHomeInfoListResult *result))success failure:(void (^)(NSError *error))failure;
/**
*  添加房间
*  @param roomName  房间名称
*  @param roomIcon  房间图片（本地基础图片名字）
*  @param success 请求成功后的回调（返回房间ID：hRC）
*  @param failure 请求失败后的回调
*/
+ (void)addRoomName:(NSString *)roomName roomIcon:(NSString *)roomIcon success:(void (^)(SYResponeHCIntegerResult *result))success failure:(void (^)(NSError *error))failure;
/**
*  修改房间
*  @param roomName  房间名称
*  @param roomIcon  房间图片（本地基础图片名字）
*  @param roomId    需要修改的房间ID
*  @param success 请求成功后的回调
*  @param failure 请求失败后的回调
*/
+ (void)updateRoomName:(NSString *)roomName roomIcon:(NSString *)roomIcon  roomId:(NSInteger)roomId success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
/**
*  删除房间
*  @param roomId  房间Id
*  @param success 请求成功后的回调（返回房间ID：hRC）
*  @param failure 请求失败后的回调
*/
+ (void)deleteRoomWithRoomId:(NSInteger)roomId success:(void (^)(SYResponeHCIntegerResult *result))success failure:(void (^)(NSError *error))failure;
/**
*  房间添加设备
*  @param roomId      房间Id
*  @param devicesArr  设备DeviceModel集合
*  @param success     请求成功后的回调（判断回调 code：1 ，全部成功，code：2 部分成功 需解析 外部直接调用数据库数据）
*  @param failure     请求失败后的回调
*/
+ (void)addDevicesToRoomWithRoomId:(NSInteger)roomId devices:(NSArray<DeviceModel*>*)devicesArr success:(void (^)(SYResponeHCDictionaryResult *result))success failure:(void (^)(NSError *error))failure;
/**
*  删除设备
*  @param device  需要删除的设备
*  @param success 请求成功后的回调
*  @param failure 请求失败后的回调
*/
+ (void)deleteDevice:(DeviceModel *)device success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;
/**
*  修改设备信息
*  @param device  修改后的设备模型 (可修改deviceIcon，deviceName)
*  @param success 请求成功后的回调
*  @param failure 请求失败后的回调
*/
+ (void)updateDevice:(DeviceModel *)device success:(void (^)(SYResponeHCStringResult *result))success failure:(void (^)(NSError *error))failure;



##### 4.返回hRA定义（ HTTP错误码说明    ）
1           请求成功    
0            系统异常（未捕获 / 未定位的异常）    
10001    缺少必备参数    
10002    参数长度错误    
10003    参数值错误（ 包括 10001 ，10002）    
10004    参数格式错误 非json请求    
10005    协议版本过低，请升级    
10006    请求格式错误，
1. 非对应 https/http     
10007    房间名称出现特殊字符
10008    智能名称出现特殊字符
10009    设备名称出现特殊字符
10100    登陆token 无效    
10101   邮箱发送频繁，24小时后重试    
10102｛0｝数据不存在
10103｛0｝数据已经存在    
10104    用户对｛0｝的权限不够    
10105    创建的智能会产生闭环    
10106    设备非法
10107   设备被使用
10108   房子 不存在
10109  PID 不存在
10110  用户已存在
10111  验证码错误
10112    账号或密码错误
10113    产品token 错误
10114    房间名称存在
10115    智能名称存在
10116  账号不存在
10117  密码错误
10118    产品pid错误    
10119    MAC地址已经被注册    
10120    智能不存在    
10121    用户不存在该设备    
10122    房间不存在    
10123    用户不存在    
10124    定时不存在    
10125    产品token 生产数量已超过    
10126    设备定时已超过
10127    问题id不存在
10128    不能分享设备给本人    
10129    分享记录不存在    
10130    分享记录已经存在    
10131    家庭不可以被删除    
10132    用户不存在该家庭    
10133    不是当前家庭    
10134    用户不能移动分享设备
10135    家庭名称存在
10136    用户不能操作自己    
10137    家庭已存在该成员    
10138    该成员已被添加，正在等待成员接受    
10139    不能创建多个家庭    
10140    设备不能被被分享者二次分享    
10141    东芝用户不能删除最后一个房间    
10142    用户不存在该房间    
20000   设备不在线    
20001  设备响应超时    
20002   设备不存在改网关    
30000    服务器宕机了    
30001    第三方服务异常    
30002    发送设备失败






