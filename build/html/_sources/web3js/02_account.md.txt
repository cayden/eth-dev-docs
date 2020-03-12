添加账户
==================
### 引入web3.js文件

### 新建index.html
```html
<script src="js/web3.js"></script>

```
代码如下
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<script src="js/web3.js"></script>
<input type="button" value="获取账号">

<input type="button" value="创建账号">
<input type="button" value="解锁账号">
<input type="button" value="获取余额">
<input type="button" value="测试合约">
<script>
        var web3 = new Web3(new Web3.providers.HttpProvider("http://127.0.0.1:8545"));
        var abi=[
            {
                "constant": false,
                "inputs": [
                    {
                        "name": "_msg",
                        "type": "string"
                    }
                ],
                "name": "set",
                "outputs": [],
                "payable": false,
                "stateMutability": "nonpayable",
                "type": "function"
            },
            {
                "constant": true,
                "inputs": [],
                "name": "say",
                "outputs": [
                    {
                        "name": "",
                        "type": "string"
                    }
                ],
                "payable": false,
                "stateMutability": "view",
                "type": "function"
            }
        ]
        var addr="0x60823932b688af82c81a082f2292e95f879a0cb0"

        document.querySelectorAll("input")[0].onclick=function(){
             //使用web3 的api 去操作节点。jsonrpc

            web3.eth.getAccounts(function(error,result){
                console.log(result);
                var res="查询账号信息:<br>";
                for (var i=0;i<result.length;i++){
                    res+="账号"+(i+1)+":"+result[i]+"<br>";
                }
                document.getElementById("result").innerHTML=res;
            });

        }
        document.querySelectorAll("input")[1].onclick=function(){
            console.log("www");
            web3.personal.newAccount("123456",function(error,result){
                console.log(result);
            });
        }
        document.querySelectorAll("input")[2].onclick=function(){
            web3.personal.unlockAccount("0x89ed26fe35814f839b8b62e5de09521280247cfd","123456",function(error,result){
                console.log(result);
                console.log("解绑成功");
            });
        }

        document.querySelectorAll("input")[3].onclick=function(){
            web3.eth.getBalance("0xb258e5b1b30215b112881c13f22ab5a47a624b81",function(error,result){
                console.log(result);

                document.getElementById("result").innerHTML="余额："+result.c[0];
                console.log("获取余额成功");
            });
        }

        document.querySelectorAll("input")[4].onclick=function(){
            var adoption = web3.eth.contract(abi).at(addr)
            console.log("获取account[0]"+web3.eth.accounts[0]);
            adoption.set.sendTransaction("I'm here!!!", {from:web3.eth.accounts[0]})

           var str= adoption.say();
            console.log("获取成功"+str);
        }


</script>
<div id="result"></div>
</body>
</html>
```
### 点击创建账号
点击创建会执行
```html
web3.personal.newAccount("123456",function(error,result){
                console.log(result);
            });
```
转账涉及发送交易，发送交易使用sendtransaction这个方法。
```html
web3.eth.sendTransaction(transactionObject [, callback])
```
第二个参数是回调函数用来获得发送交易的Hash值。

第一个参数是一个交易对象，交易对象里面有几个字段：

- from : 就是从哪个账号发送金额
- to : 发动到到哪个账号
- value 是发送的金额
- gas: 设置gas limit
- gasPrice: 设置gas 价格

如果from没有的话，他就会用当前的默认账号， 如果是转账to和value是必选的两个字段。

```javascript
//  这里使用Metamask 给的gas Limit 及 gas 价
var fromAccount = $('#fromAccount').val();
var toAccount = $('#toAccount').val();
var amount = $('#amount').val();

// 对输入的数字做一个检查
if (web3.isAddress(fromAccount) &&
            web3.isAddress(toAccount) &&
            amount != null && amount.length > 0） {
    var message = {from: fromAccount, to:toAccount, value: web3.toWei(amount, 'ether')};

    web3.eth.sendTransaction(message, (err, res) => {
        var output = "";
        if (!err) {
            output += res;
        } else {
            output = "Error";
        }
    }
}
```

具体代码
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<script src="js/web3.js"></script>
<input type="button" value="获取账号">

<input type="button" value="创建账号">
<input type="button" value="解锁账号">
<input type="button" value="获取余额">
<input type="button" value="测试合约">

<input type="button" value="转账">
<script>
        var web3 = new Web3(new Web3.providers.HttpProvider("http://127.0.0.1:8545"));
        var abi=[
            {
                "constant": false,
                "inputs": [
                    {
                        "name": "_msg",
                        "type": "string"
                    }
                ],
                "name": "set",
                "outputs": [],
                "payable": false,
                "stateMutability": "nonpayable",
                "type": "function"
            },
            {
                "constant": true,
                "inputs": [],
                "name": "say",
                "outputs": [
                    {
                        "name": "",
                        "type": "string"
                    }
                ],
                "payable": false,
                "stateMutability": "view",
                "type": "function"
            }
        ]
        var addr="0x60823932b688af82c81a082f2292e95f879a0cb0"

        document.querySelectorAll("input")[0].onclick=function(){
             //使用web3 的api 去操作节点。jsonrpc

            web3.eth.getAccounts(function(error,result){
                console.log(result);
                var res="查询账号信息:<br>";
                for (var i=0;i<result.length;i++){
                    res+="账号"+(i+1)+":"+result[i]+"<br>";
                }
                document.getElementById("result").innerHTML=res;
            });

        }
        document.querySelectorAll("input")[1].onclick=function(){
            console.log("www");
            web3.personal.newAccount("123456",function(error,result){
                console.log(result);
            });
        }
        document.querySelectorAll("input")[2].onclick=function(){
            web3.personal.unlockAccount("0x89ed26fe35814f839b8b62e5de09521280247cfd","123456",function(error,result){
                console.log(result);
                console.log("解绑成功");
            });
        }

        document.querySelectorAll("input")[3].onclick=function(){
            web3.eth.getBalance("0xb258e5b1b30215b112881c13f22ab5a47a624b81",function(error,result){
                console.log(result);

                document.getElementById("result").innerHTML="余额："+result.c[0];
                console.log("获取余额成功");
            });
        }

        document.querySelectorAll("input")[4].onclick=function(){
            var adoption = web3.eth.contract(abi).at(addr)
            console.log("获取account[0]"+web3.eth.accounts[0]);
            web3.personal.unlockAccount(web3.eth.accounts[0],"123456",function(error,result){
                console.log(result);
                console.log("解绑成功");
                adoption.set.sendTransaction("I'm here!!!", {from:web3.eth.accounts[0]})

                var str= adoption.say();
                console.log("获取成功"+str);
            });

        }

        document.querySelectorAll("input")[5].onclick=function(){
            console.log('oooo');
            console.log("获取account[0]"+web3.eth.accounts[0]);
            var fromAccount='0xb258e5b1b30215b112881c13f22ab5a47a624b81';
            var toAccount='0xf417953e3b736a68cf7c60f89f459a28d25880da';
            var amount=2000;
            var message={from:fromAccount,to:toAccount,value:web3.toWei(amount,'ether')}
            web3.personal.unlockAccount(web3.eth.accounts[0],"123456",function(error,result){
                console.log(result);
                console.log("解绑成功");
                web3.eth.sendTransaction(message,function(error,result){
                    var output='';
                    if(!error){
                        output+=result;
                    }else{
                        output="Error";
                    }
                    console.log(output);
                })
            });

        }


</script>
<div id="result"></div>
</body>
</html>
```
执行成功后，返回交易地址
<div align=center>

![Message.sol](../images/5e13c2f66db99.png)
</div>
