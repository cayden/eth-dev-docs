环境搭建
==================
web3.js 是一个通过RPC 调用 和本地以太坊节点进行通信的js库。web3.js可以与任何暴露了RPC接口的以太坊节点连接。 web3中提供了eth对象 - web3.eth来与以太坊区块链进行交互。
这里使用web3.js+html进行开发，也可以使用node.js项目进行开发
### web3.js+html
需要下载web3.js文件
下载地址：
https://github.com/cayden/web3-js/tree/master/js

### node.js项目
1、新建一个node.js项目并初始化
```shell
$ mkdir web3test && cd web3test
$ npm init

```
2、导入web3.js
```shell
npm install web3 --save
```
