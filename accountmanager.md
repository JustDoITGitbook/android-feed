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

顾名思义，`AccountManager`是用来管理用户账户。使用`AccountManager`有两个要点：`Bundle` 、`key`常量的含义、如何使用账户管理方法。`AccountManager`定义了许多`Bundle`、` Key`常量，可以用作`Intent`的`key`用于`Activity`之间传递参数；也可以作为`Authenticator`返回`Bundle`的`Key`，这种情况，`AccountManager`会根据`Key`的情况作出相应操作，比如，跳转到验证身份页面，返回`Accont Type`,`AuthToken`,`Account Name`\(`getAuthenToken()`有返回`AuthToken`时必须返回`Account Type`和`Account Name`，不然会提示`“the type and name should not be empty”`\)等。



