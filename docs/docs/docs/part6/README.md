#设备控制



```java
/**
 * 发送控制指令
 * @param parameter 控制指令参数
 * @param callBack  结果回调
 */
void control(CmdParameter parameter, ResultCallBack callBack);
```

#查询设备状态

```java
/**
 * 查询设备状态
 * @param did      设备id
 * @param callBack 结果回调
 */
void getStatus(int did,ResultCallBack<LinkedHashMap<String,String>> callBack);
```

#更新设备信息

```java
/**
 * 更新设备信息
 * @param did      设备id
 * @param name     设备名称
 * @param icon     设备图标
 * @param callBack 结果回调
 */
void updateDeviceInfo(int did, String name, String icon, ResultCallBack callBack);
```

#更新常用设备

```java
/**
 * 更新常用设备 (用于设置单个设备是否常用)
 * @param did      设备id
 * @param isCommon 是否常用设备
 * @param callBack 结果回调
 */
void updateCommonDevice(int did, boolean isCommon, ResultCallBack callBack);
```

#获取设备mcu版本号

```java
/**
 * 获取设备mcu版本号
 * @param did      设备id
 * @param callBack 结果回调
 */
void getMcuVersion(int did, ResultCallBack<String> callBack);
```

#获取设备升级信息

```java
/**
 * 获取设备升级信息
 * @param did      设备id
 * @param callBack 结果回调
 */
void getDeviceUpgradeInfo(int did,ResultCallBack<UpdateInfoBean> callBack);
```

#设备升级

```java
/**
 * 设备升级
 * @param did 设备id
 */
void deviceOTA(int did, ResultCallBack callBack);
```

#设备删除

```java
/**
 * 设备删除
 * @param did      设备id
 * @param callBack 结果回调
 */
void deleteDevice(int did ,ResultCallBack callBack);
```

#设置设备状态改变监听

```java
/**
 * 设置设备状态改变监听
 * @param listener 设备状态改变监听
 */
void registerDeviceStatusListener(OnDeviceStatusListener listener);
```

#取消设备状态改变监听

```java
/**
 * 取消设备状态改变监听
 * @param listener 设备状态改变监听
 */
void unRegisterDeviceStatusListener(OnDeviceStatusListener listener);
```

#设备状态改变回调类 OnDeviceStatusListener

```java
/**
 * 设备添加成功
 * @param did 设备id
 */
void onDeviceAdded(int did);

/**
 * 设备删除成功
 * @param did 设备id
 */
void onDeviceRemoved(int did);

/**
 * 设备信息改变
 * @param did 设备id
 */
void onDeviceInfoChanged(int did);

/**
 * 设备状态上报
 * @param did 设备id
 */
void onDeviceStatusInform(int did);

/**
 * 设备上线
 * @param did 设备id
 */
void onDeviceLogin(int did);

/**
 * 设备离线
 * @param did 设备id
 */
void onDeviceOffline(int did);

/**
 * 设备升级成功
 * @param did 设备id
 */
void onDeviceUpdateSuccess(int did);

/**
 * 设备升级失败
 * @param did 设备id
 */
void onDeviceUpdateFail(int did);
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
| daily           | 数字   | 是否常用设备 0不是 1是           |
| localStatus     | 数字   | 是否本地在线 0离线 1在线          |
| regionCode      | 数字   | 地区编码                    |
| shareInfoId     | 数字   | 分享信息id                  |
| nudStatus       | 数字   | 关系状态                    |
| relationType    | 数字   | 关系类型 1app添加 2设备分享 3家庭分享 |
| deviceAttrs     | 键值对  | 设备属性集合                  |
