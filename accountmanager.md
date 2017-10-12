# AccountManager {#使用accountmanager和abstractaccountauthenticator建立账户系统}

### 建立账号

```java
accountManager.addAccountExplicitly((Account) account, "password", (Bundle) userdata); // nullable userdata

Account account = new Account(username, accountType);

String accountType = "com.infstory"; // 帳號識別類型
String username = "yongjhih@example.com"; // 帳號名稱
```



