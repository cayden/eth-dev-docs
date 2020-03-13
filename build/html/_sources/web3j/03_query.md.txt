转账和余额查询功能实现
======================
详见测试类
```java
package com.cayden.ethereum;

import com.cayden.ethereum.pojo.AccountInfo;
import org.web3j.protocol.parity.methods.response.PersonalAccountsInfo;

import java.math.BigDecimal;
import java.math.BigInteger;
import java.util.List;

/**
 * Created by cuiran on 18/7/6.
 */
public class AccountTest {
    public static void main(String args[]) {
        createAccount();

//        getBalance();

//        queryAccount();
//        trade();

//        getAccountInfo();
    }

    public static void getBalance(){
        Account account = new Account();
        BigInteger ba = account.getBalance("0xb258e5b1b30215b112881c13f22ab5a47a624b81");
        System.out.print(ba);



    }

    public static void getAccountInfo(){
        Account account = new Account();
        PersonalAccountsInfo.AccountsInfo accountsInfo = account.getAccountInfo("0x5bd2328251e8abd5bc39393a9549586634785938");
        System.out.println(accountsInfo.toString());


    }
    public static  void queryAccount(){
        Account account = new Account();
        List<String> accounts = account.getAccountlist();
        for(String accountId:accounts){
            System.out.println(accountId);
        }
    }

    public static void trade(){
        Trade trade = new Trade();
        boolean result=trade.trasfer("0x1a95f4df6dbf7511b8ec820833df628ea743c458","123456","0x91140c3170f4aa959f09aff9b5393e9d0cd2a54c",new BigDecimal(5));
        System.out.println("trade:"+result);

    }
    public static void createAccount(){
        Account account = new Account();
        AccountInfo accountInfo = new AccountInfo();
        accountInfo.setPhone("12345678901");
        accountInfo.setAddress("北街家园");
        accountInfo.setSchool("清华大学");
        accountInfo.setUserName("cayden");
        String accountId = account.createAccount("cayden","123456",accountInfo);
        System.out.println("注册账户成功:"+accountId);
//        PersonalAccountsInfo.AccountsInfo accountsInfo = account.getAccountInfo("0xad7bbca86e02e503076b06931e05938e51e49fb9");
//        System.out.println(accountsInfo.toString());
    }
}

```

本项目的源码 访问地址
v1.0 钱包功能模块

https://github.com/cayden/ethsample/releases/tag/v1.0
