#创建家庭

```java
/**
 * 创建家庭
 * @param name     家庭名称
 * @param location 家庭地址
 * @param roomList 房间信息
 * @param callBack 结果回调
 */
void createHome(String name, String location, List<RoomBean> roomList, ResultCallBack callBack);
```

#得到用户家庭数据

```java
/**
 * 得到用户家庭数据
 * @param callBack 结果回调
 */
void getHomeList(ResultCallBack<List<HomeBean>> callBack);
```

#更新家庭信息

```java
/**
 * 更新家庭信息
 * @param hid      家庭信息
 * @param name     家庭名称
 * @param location 家庭地址
 * @param callBack 结果回调
 */
void updateHomeInfo(int hid,String name,String location,ResultCallBack callBack);
```

#设置家庭状态改变监听

```java
/**
 * 设置家庭状态改变监听
 * @param listener 家庭状态改变监听
 */
void registerHomeStatusListener(OnHomeStatusListener listener);
```

#取消家庭状态改变监听

```java
/**
 * 取消家庭状态改变监听
 * @param listener 家庭状态改变监听
 */
void unRegisterHomeStatusListener(OnHomeStatusListener listener);
```

#家庭状态改变回调类 OnHomeStatusListener

```java
/**
 * 家庭添加成功
 * @param hid 家庭id
 */
void onHomeAdded(int hid);

/**
 * 家庭邀请通知
 * @param hid 家庭id
 * @param homeName 家庭名称
 */
void onHomeInvite(int hid,String homeName);

/**
 * 家庭删除成功
 * @param hid 家庭id
 */
void onHomeRemoved(int hid);

/**
 * 家庭信息改变
 * @param hid 家庭id
 */
void onHomeInfoChanged(int hid);

/**
 * 切换当前家庭
 * @param hid
 */
void onHomeCurrentChanged(int hid);
```

#家庭模型类
| 字段名称         | 类型  | 字段说明                   |
|--------------|-----|------------------------|
| userId       | 数字  | 用户id                   |
| homeId       | 数字  | 家庭id                   |
| homeName     | 字符串 | 家庭名称                   |
| roomCount    | 数字  | 房间数量                   |
| deviceCount  | 数字  | 设备数量                   |
| homeCurrent  | 数字  | 1：当前家庭 0：其余家庭|
| createDate   | 数字  | 创建时间                   |
| regionCode   | 数字  | 城市编码                   |
| homeLocation | 字符串 | 家庭位置                   |
| userType     | 数字  | 类型1：管理员 9：普通用户 0：超级管理员 |
