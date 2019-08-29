
#获取设备的所有定时任务
```java
/**
* 获取某个设备的所有定时任务
*
* @param deviceId       设备的id
* @param resultCallBack 回调
*/
void getDeviceTimingList(int deviceId, ResultCallBack<ArrayList<Timing>> resultCallBack);
```

#添加一个定时

```java
/**
* 添加定时
*
* @param deviceId       设备id
* @param name           定时的名称
* @param repeat         循环次数
*                       对于 mode 为自定义时，每一位代表一周中的一天。
*                       最右边的位为低位，代表周一，最左边的位为高位，代表周日。
*                       0：标识该天不需要执行定时。
*                       1：标识该天需要执行定时。
*                       例如，自定义为周二、周四、周五需要执行定时，则可定义为：0011010
* @param time           执行时间 格式为 2018:01:01:01:01 yyyy:MM:dd:HH:mm
* @param actions        执行的动作 如 {"onoff":1,"mode":2}
* @param resultCallBack 回调时间
*/
void addTiming(int deviceId, String name, String repeat, String time, LinkedHashMap<String, String> actions, ResultCallBack resultCallBack);
```

#更新设备的定时任务

```java
/**
* 更新定时
*
* @param deviceId       设备id
* @param timingId       定时id
* @param name           定时的名称
* @param repeat         循环次数
*                       对于 mode 为自定义时，每一位代表一周中的一天。
*                       最右边的位为低位，代表周一，最左边的位为高位，代表周日。
*                       0：标识该天不需要执行定时。
*                       1：标识该天需要执行定时。
*                       例如，自定义为周二、周四、周五需要执行定时，则可定义为：0011010
* @param time           执行时间 格式为 2018:01:01:01:01 yyyy:MM:dd:HH:mm
* @param actions        执行的动作 如 {"onoff":1,"mode":2}
* @param resultCallBack 回调时间
*/
void updateTiming(int deviceId, int timingId, String name, String repeat, String time, LinkedHashMap<String, String> actions, ResultCallBack resultCallBack);
```

#删除设备的某个定时任务


```java
/**
* 删除定时
*
* @param timingId       定时的id
* @param resultCallBack 回调
*/
void deleteTiming(int timingId, ResultCallBack resultCallBack);
```

#更新设备的某个定时任务开启和关闭状态


```java
/**
* 修改定时的开启关闭状态
*
* @param timingId       定时的id
* @param status         1开启 9关闭
* @param resultCallBack 回调
*/
void updateTimingStatus(int timingId, int status, ResultCallBack resultCallBack);
```

#监听所有设备的定时任务变化时的回调

```java
/**
* 监听定时变化
* @param onTimingChangedListener
*/
void addTimingChangeListener(OnTimingChangedListener onTimingChangedListener);
```



#OnTimingChangedListener 定时变化的回调接口类

```java
/**
* @param did     定时发生变更的设备id
* @param timings 发生变更后的定时
*/
void onTimingChanged(int did, List<Timing> timings);
```


#Timing数据模型

| 字段名称       | 字段说明    | 类型  | 备注                                                                                       |
|------------|---------|-----|------------------------------------------------------------------------------------------|
| dtId       | 定时任务的ID | 数字  | \-                                                                                       |
| startInfo  | 启动的信息   | 文本  | \{"time":\{"year":2018,"month":7,"date":8,"hour":12,"min":48\},"trigger":\{"onoff":"0"\} |
| endInfo    | 结束的信息   | 文本  | \{"time":\{"year":2018,"month":7,"date":8,"hour":12,"min":48\},"trigger":\{"onoff":"0"\} |
| dtMode     | 模型      | 字符串 |  模型 once：一次性执行 every：每天 week：工作日 reset：周末 self：自定义                                       |
| dtDays     | 执行日期    | 字符串 |  对于 mode 为自定义时，每一位代表一周中的一天。<br> 最右边的位为低位，代表周一，最左边的位为高位，代表周日。 <br> 0：标识该天不需要执行定时。 <br> 1：标识该天需要执行定时。<br> 例如，自定义为周二、周四、周五需要执行定时，则为：0011010                                                                                    |
| createTime | 创建的时间   | 数字  | \-                                                                                       |
| userId     | 用户ID    | 数字  | \-                                                                                       |
| deviceId   | 设备ID    | 数字  | \-                                                                                       |
| dtStatus   | 任务的状态   | 数字  | 状态 1：打开， 0：关闭                                                                   |

