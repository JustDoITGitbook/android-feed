# AccountManager {#使用accountmanager和abstractaccountauthenticator建立账户系统}

### 示例：

```java
accountManager.addAccountExplicitly((Account) account, "password", (Bundle) userdata); // nullable userdata

Account account = new Account(username, accountType);

String accountType = "com.upup8"; // 账号类型
String username = "otnp50@example.com"; // 账号名
```

## 为什么要使用AccountManager和AccountAuthenticatr {#为什么要使用accountmanager和accountauthenticatr}

建立账户管理系统，可以使用`SharedPreference`来存储、更新、删除`AuthToken`，也可以用来存储、更新、删除账户和密码。既然这样，为什么还要使用`AccountManager`和`AccountAuthenticator`?

**原因有一下几点：**

1.`AccountManager`是`Android`系统提供的账户管理框架，十分强大和方便，可以管理不同类型账户，不同类型`AuthenToken`

2.`AccountAuthenticator`把账户的验证过程、`AuthToken`的获取过程分离出来，降低程序的耦合性

3.使用`AccountAuthenticator`会在”设置”中添加一个账户入口。

## AccountManager和Authenticator之间的关系 {#accountmanager和authenticator之间的关系}

`AccountManager`和`Authenticator`的方法相对应，比如，`AccountManager`的`addAccount()`方法会调用`Authenticator`的`addAccount()`方法，`Authenticator`的方法会返回一个`Bundle`给`AccountManager`处理。具体细节后面会介绍。

## 使用AccountManager管理账号 {#使用accountmanager管理账号}

顾名思义，`AccountManager`是用来管理用户账户。使用`AccountManager`有两个要点：`Bundle` 、`key`常量的含义、如何使用账户管理方法。`AccountManager`定义了许多`Bundle`、`Key`常量，可以用作`Intent`的`key`用于`Activity`之间传递参数；也可以作为`Authenticator`返回`Bundle`的`Key`，这种情况，`AccountManager`会根据`Key`的情况作出相应操作，比如，跳转到验证身份页面，返回`Accont Type`,`AuthToken`,`Account Name`\(`getAuthenToken()`有返回`AuthToken`时必须返回`Account Type`和`Account Name`，不然会提示`“the type and name should not be empty”`\)等。

| 常用Bundle key |
| :---: |


| key | 含义 |
| :--- | :--- |
| AccountManager.KEY\_ACCOUNT\_AUTHENTICATOR\_RESPONSE | 可以调用onResult\(\)和onError\(\)来相应用户提供的信息 |
| AccountManager.KEY\_INTENT | 开启新Activity和用户进行交互 |
| AccountManager.KEY\_AUTHTOKEN | 令牌 |
| AccountManager.KEY\_ACCOUNT\_TYPE | 账户类型 |
| AccountManager.KEY\_ACCOUNT\_NAME | 账户名 |
| AccountManager.KEY\_ERROR\_CODE | 错误码\(必须大于0\) |
| AccountManager.KEY\_ERROR\_MESSAGE | 错误信息\(必须和错误码一起使用\) |

**常用AccountManager管理账户方法：**

获取`AuthToken`：

```java
@param account 账户
@param authTokenType token类型
@param options 额外的数据
@param activity 用来开启另外的Activity
@param callback 结果回调
@param 回调的线程，null时为主线程
public AccountManagerFuture<Bundle> getAuthToken(
            final Account account, final String authTokenType, final Bundle options,
            final Activity activity, AccountManagerCallback<Bundle> callback, Handler handler)
```

获取账户列表：

```java
@param type 账户列表类型
public Account[] getAccountsByType(String type)
```

从`AccountManager`的缓存中移除`AuthToken`:

```java
@param accountType 账户类型
@param authToken 令牌
public void invalidateAuthToken(final String accountType, final String authToken)
```



