#获取产品列表

```java
/**
 * 添加智能
 * @param model    智能模型
 * @param callBack 回调结果
 */
void addWisdom(WisdomModel model, ResultCallBack<WisdomModel> callBack);
```

#删除智能

```java
/**
 * 删除智能
 * @param wid      智能id
 * @param callBack 回调结果
 */
void deleteWisdom(int wid, ResultCallBack callBack);
```

#获取智能数据集合

```java
/**
 * 获取智能数据集合
 * @param callBack 回调结果
 */
void getWisdomList(ResultCallBack<List<WisdomModel>> callBack);
```


#开关智能

```java
/**
 * 开关智能
 * @param wid      智能id
 * @param onoff    开关
 * @param callBack 回调结果
 */
void switchWisdom(int wid,boolean onoff,ResultCallBack callBack);
```

#修改智能

```java
/**
 * 修改智能
 * @param model    智能数据
 * @param callBack 回调结果
 */
void updateWisdom(WisdomModel model, ResultCallBack callBack);
```

#手动执行智能

```java
/**
 * 手动执行智能
 * @param wid 智能id
 */
void executeWisdom(int wid);
```

#设置智能状态改变监听

```java
/**
 * 设置智能状态改变监听
 * @param listener 智能状态改变监听
 */
void registerWisdomStatusListener(OnWisdomStatusListener listener);
```

#取消智能状态改变监听

```java
/**
 * 取消智能状态改变监听
 * @param listener 智能状态改变监听
 */
void unRegisterWisdomStatusListener(OnWisdomStatusListener listener);
```

# WisdomModel数据模型

| 字段名称            | 类型        | 字段说明                                                                |
|-----------------|-----------|---------------------------------------------------------------------|
| wid             | 数字        | 智能ID                                                                |
| userID          | 数字        | 用户ID                                                                |
| hid             | 数字        | 家庭ID                                                                |
| wisdomIcon      | 字符串       | 图片地址                                                                |
| wisdomname      | 字符串       | 智能名字                                                                |
| createTime      | 数字        | 创建时间                                                                |
| andOr           | 数字        | 执行条件：1  一起执行，2 满足其中一个就执行                                            |
| wisdomStatus    | 字符串       | 状态： 1正常 ，2配置中，3配置失败, 9无效                                            |
| wisdomType      | 数字        | 智能类型： \(默认\)1点击执行，2设备联动执行， 3 定时智能                                   |
| updateNum       | 数字        | 修改次数                                                                |
| onoff           | 数字        | 状态 1：打开 9：关闭                                                        |
| supportHomePage | 数字        | 是否放在首页。0：不支持，1：支持                                                   |
| wcid            | 数字        | 条件ID                                                                |
| Id              | 字符串       | 设备ID                                                                |
| createTime      | 数字        | 创建时间                                                                |
| conditionStatus | 数字        | 状态 1：正常 ，2：配置中，3：配置失败, 9：无效                                         |
| conditionType   | 数字        | 条件类型,S\(1\-2\) 1：用户点击，2：设备执行 3：定时条件                                 |
| conditionName   | 字符串       | 条件名字                                                                |
| appointment     | 字符串       | 条件约定grt：大于 less：小于 equal：等于 geq：大于等于 leq：小于等于 redge：上跳触发 fedge：下跳触发 |
| conditionValue  | 数字        | 条件值                                                                 |
| timeInfo        | Linkedmap | 定时智能的时间信息,若type为3的时候必传，字段定义和新增定时的时间信息一致                             |
| tokenID         | 数字        | 条件中的tokenId                                                         |
| wiid            | 数字        | 执行ID                                                                |
| Id              | 数字        | 执行的ID：implementType = 2 的时候为设备 id                                   |
| implementStatus | 数字        | 状态 1：打开 9：无效                                                        |
| implementName   | 字符串       | 执行名字                                                                |
| implementType   | 数字        | 执行类型：2：设备执行                                                         |
| implementValue  | 字符串       | 执行的值                                                                |
| tokenId         | 数字        | 执行中的tokenId                                                         |
