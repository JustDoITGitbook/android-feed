# AccountManager {#使用accountmanager和abstractaccountauthenticator建立账户系统}

### 建立账号

```java
accountManager.addAccountExplicitly((Account) account, "password", (Bundle) userdata); // nullable userdata

Account account = new Account(username, accountType);

String accountType = "com.upup8"; // 账号类型
String username = "otnp50@example.com"; // 账号名
```



