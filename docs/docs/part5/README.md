#添加房间

```java
/**
 * 添加房间
 * @param hid      家庭id
 * @param name     房间名称
 * @param icon     房间图片
 * @param callBack 结果回调
 */
void addRoom(int hid,String name,String icon,ResultCallBack callBack)
```

#得到房间数据

```java
/**
 * 得到房间数据
 * @param hid      家庭id
 * @param callBack 结果回调
 */
void getRoomList(int hid,ResultCallBack<List<RoomModel>> callBack);
```

#更新房间信息

```java
/**
 * 更新房间信息
 * @param rid      房间id
 * @param name     房间名称
 * @param icon     房间图片
 * @param callBack 结果回调
 */
void updateRoomInfo(int rid,String name,String icon,ResultCallBack callBack);
```

#更新设备所属的房间

```java
/**
 * 更新设备所属的房间
 * @param hid      家庭id
 * @param rid      房间id
 * @param dids     设备id集合
 * @param callBack 结果回调
 */
void updateRoomDevice(int hid,int rid, List<Integer> dids, ResultCallBack callBack);
```

#删除房间

```java
/**
 * 删除房间
 * @param hid      家庭id
 * @param rid      房间id
 * @param callBack 结果回调
 */
void deleteRoom(int hid,int rid,ResultCallBack callBack);
```

#设置房间状态改变监听

```java
/**
 * 设置房间状态改变监听
 * @param listener 房间状态改变监听
 */
void registerRoomStatusListener(OnRoomStatusListener listener);
```

#取消房间状态改变监听

```java
/**
 * 取消房间状态改变监听
 * @param listener 房间状态改变监听
 */
void unRegisterRoomStatusListener(OnRoomStatusListener listener);
```

#房间状态改变回调类 OnRoomStatusListener

```java
/**
 * 房间添加成功
 * @param rid
 */
void onRoomAdded(int rid);

/**
 * 房间删除成功
 * @param rid
 */
void onRoomRemoved(int rid);

/**
 * 房间信息改变
 * @param rid
 */
void onRoomInfoChanged(int rid);

/**
 * 房间下设备改变
 * @param rid
 */
void onRoomDeviceChanged(int rid);
```
#RoomModel数据模型
| 字段名称       | 类型  | 字段说明            |
|------------|-----|-----------------|
| userId     | 数字  | 用户id            |
| homeId     | 数字  | 家庭id            |
| roomId     | 数字  | 房间id            |
| roomName   | 字符串 | 房间名称            |
| roomIcon   | 字符串 | 设备数量            |
| roomType   | 数字  | 房间类型（1：默认 2：新增） |
| createTime | 数字  | 创建时间            |
| regionCode | 数字  | 城市编码            |