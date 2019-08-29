#获取分享的用户列表

```java
  /**
 * 获取分享的用户列表
 *
 * @param did            设备的did
 * @param resultCallBack 回调接口
 */
void getDeviceSharedList(int did, ResultCallBack<List<ShareItemBean>> resultCallBack);
```

#分享设备给用户

```java
/**
 * 分享设备给用户
 * @param did 要分享的设备id
 * @param account 要分享给的账号
 * @param resultCallBack 回调接口
 */
void shareDeviceToUser(int did, String account, ResultCallBack resultCallBack);
```

#删除设备分享

```java
/**
 * 删除设备分享
 * @param shareItemBean 要删除的item
 * @param resultCallBack 回调
 */
void removeDeviceShare(ShareItemBean shareItemBean, ResultCallBack resultCallBack);
```

#ShareItemBean数据模型
| 字段名称              | 类型  | 字段说明          |
|-------------------|-----|---------------|
| userId            | 数字  | 用户id          |
| nudId             | 数字  | 用户设备Id        |
| userName          | 字符串 | 用户名           |
| userAccountNumber | 字符串 | 用户账号分为：手机号和邮箱 |
| iconUrl           | 字符串 | 用户头像地址        |
