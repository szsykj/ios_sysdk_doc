
#获取当前设备倒计时，查询设备获取，可能为null

```java
/**
* 获取当前设备的倒计时，查询设备获取
*
* @param did 设备的id
* @return
*/
void getCountDownByDeviceId(int did, ResultCallBack<CountDownModel> resultCallBack);
```

#设置倒计时
```java
/**
* @param did              设备的id
* @param minute           要设置的倒计时长，单位为分钟
* @param actions          要设置动作集合 {"onoff":1}
* @param resultCallBack   回调
*/
void setCountDown(int did, final int minute, LinkedHashMap<String, String> actions, ResultCallBack<CountDownModel> resultCallBack);
```

#停止倒计时
```java
/**
* 停止timer
*
* @param did
* @param resultCallBack
*/
void stopCountDown(int did, ResultCallBack resultCallBack);
```


#CountDownModel 数据模型

| 字段名称       | 字段说明    | 类型  | 备注 |
|------------|---------|-----|------------------------------------------------------------------------------------------|
| id         | 倒计时任务的ID  | 数字  |   |
| deviceId   | 设备的did       | 数字  |  |
| targetTime | 目标执行时间     | long | 执行的时间戳 | 
| target     | 执行动作       | 字符串 | {"onoff":"1"}|


