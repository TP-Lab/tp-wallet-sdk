# TP接入文档

#### 版本：v1.0

### TokenPocket扫码登陆

TP钱包扫描二维码，本地授权登陆，通知Dapp，完成登陆过程

- 登陆二维码协议格式
~~~
{
    protocol	string   // 协议名，钱包用来区分不同协议，本协议为 SimpleWallet
    version     string   // 协议版本信息，如1.0
    dappName    string   // dapp名字
    dappIcon    string   // dapp图标
    blockchain  string   //底层  "eos enu eth moac"
    wallet      string   // 登陆的钱包（可以唯一表示一个钱包的信息）可选
    action      string   // 赋值为login
    actionId    string   // dapp 生成的，用于此次操作的唯一标识   
    callbackUrl string   // dapp server上用于接受登录验证信息的url
    expired	    string   //二维码过期时间，时间为秒
    memo	    string   // 登录备注信息，钱包用来展示，可选
}
~~~

- 钱包对登陆信息签名
~~~
data = timestamp + wallet + actionId + ref
sign = ecc.sign(data, privateKey)
~~~


- 钱包将签名后的信息通过post请求发送到callbackUrl
~~~
{
    protocol  string
    version   string
    timestamp string
    sign      string
    actionId  string
    wallet    string
    ref       string
}
~~~

- DAPP验证登陆信息

### 拉起TokenPocket授权登陆
如果dapp没有登陆服务器，只需要拉起钱包获取相关账户信息，则不需要callbackUrl
- 拉起TokenPocket转账和扫扫码转账相比，多了callbackSchema字段，用于回调通知Dapp操作结果。其他字段一样
- 协议格式
~~~
    ...
    callbackSchema    string // Dapp自定义回调schema，例如：appABC://abc.com?action=login 返回结果为：appABC://abc.com?action=login&result=1&param={json param} result的值为：0为用户取消，1为成功,  2为失败
    ...
~~~

##### 拉起TokenPocket授权登陆返回信息json格式如下
~~~
{
   "wallet": "eoseoseosacc",
   "publickey": "EOS2TtWv19a9eYEQYB8NbGCM28nQNngWP4UcSjVYqtEz6kF7yCnPX",
   "permissions": ["active", "owner"],
   "result": 1
}
~~~

- 使用TokenPocket SDK，Dapp不需要传递callbackSchema字段以及处理相关操作，只需要调用SDK相关方法即可
- 其他过程和扫码类似

### TokenPocket扫码转账
TP钱包扫描二维码，完成转账操作，钱包将txId告诉Dapp，Dapp轮询支付结果

- 转账二维码协议
~~~
{
    protocol    string   // 协议名，钱包用来区分不同协议，本协议为 SimpleWallet
    version     string   // 协议版本信息，如1.0
    dappName    string   // dapp名字，用于在钱包APP中展示，可选
    dappIcon    string   // dapp图标Url，用于在钱包APP中展示，可选
    action      string   // 支付时，赋值为transfer，必须
    actionId    string   // 本次支付的唯一标识
    blockchain  string   //底层  "eos enu eth moac"
    from        string   // 付款人的EOS账号，可选
    to          string   // 收款人的EOS账号，必须
    amount      number   // 转账数量，必须
    contract    string   // 转账的token所属的contract账号名，必须
    symbol      string   // 转账的token名称，必须
    precision   number   // 转账的token的精度，小数点后面的位数，必须
    memo        string   // 由dapp生成的业务参数信息，需要钱包在转账时附加在memo中发出去，格式为:k1=v1&k2=v2，可选
			     // 钱包转账时还可附加ref参数标明来源，如：k1=v1&k2=v2&ref=walletname
    desc	    string   // 交易的说明信息，钱包在付款UI展示给用户，最长不要超过128个字节，可选			     
    expired	    string   // 二维码过期时间，unix时间戳
    callbackUrl string //回调url，例如：https://abc.com?action=transfer&qrcID=123，则回调结果为：
       https://abc.com?action=transfer&qrcID=123&result=0&txID=xxx
       其中result（0为用户取消，1为成功,2为失败）txID为执行成功的transactionHash
}
~~~

### 拉起TokenPocket转账
- 拉起TokenPocket转账和扫扫码转账相比，多了callbackSchema字段，用于回调通知Dapp操作结果。其他字段一样
- 协议格式
~~~
    ...
    callbackSchema    string // Dapp自定义回调schema，例如：appABC://abc.com?action=transfer 返回结果为：appABC://abc.com?action=transfer&result=0&txID=xxx&param={json param} result的值为：0为用户取消，1为成功,  2为失败
    ...
~~~

转账完成后返回的json param格式如下
~~~
"ref": "TokenPocket",
"txid": "588c6797534d09e8e0b149c06c11bfd6ca7b96f0d4bba87700fffe7a87b0d988",
"publickey": "EOSX1tWv19a9eKEQQB8Nb2wM28nYNngWP3UcSjVYqtjz6kF7yCnQ",
"wallet": "eoseoseostes",
"permissions": ["active", "owner"],
"result": 1
~~~


- 使用TokenPocket SDK，Dapp不需要传递callbackSchema字段以及处理相关操作，只需要调用SDK相关方法即可
- 其他过程和扫码类似

### TokenPocket扫码执行合约
使用TokenPocket扫码，执行pushTransaction操作
- 协议格式
~~~
    protocol    string   // 协议名，钱包用来区分不同协议，本协议为 SimpleWallet
    version     string   // 协议版本信息，如1.0
    dappName    string   // dapp名字，用于在钱包APP中展示，可选
    dappIcon    string   // dapp图标Url，用于在钱包APP中展示，可选
    action      string   // 支付时，赋值为transfer，必须
    actionId    string   // 本次支付的唯一标识
    blockchain  string   //底层  "eos enu eth moac"
    actions     string   //json数组 每个对象是一个action

    memo    string   // 由dapp生成的业务参数信息，需要钱包在转账时附加在memo中发出去，格式为:k1=v1&k2=v2，可选
			     // 钱包转账时还可附加ref参数标明来源，如：k1=v1&k2=v2&ref=walletname
    desc	    string   // 交易的说明信息，钱包在付款UI展示给用户，最长不要超过128个字节，可选			     
    expired	    number   // 二维码过期时间，unix时间戳
    callbackUrl string //回调url，例如：https://abc.com?action=pushTransaction&qrcID=123，则回调结果为：
https://abc.com?action=pushTransaction&qrcID=123&result=0&txID=xxx
其中result（0为用户取消，1为成功,  2为失败）txID为执行成功的transactionHash 
~~~

### 拉起TokenPocket 执行合约
Dapp 拉起TokenPocket 执行合约操作，和扫码执行合约操作相比，多了callbackSchema字段，用于通知Dapp操作结果，其他字段一样
- 协议格式
~~~
    ...
    callbackSchema    string     // Dapp自定义回调schema，例如：appABC://abc.com?action=pushTransaction 返回结果为：appABC://abc.com?action=pushTransaction&result=0&txID=xxx&param={json param} result的值为：0为用户取消，1为成功,  2为失败
    ...
~~~


合约执行完成后返回的json param格式如下
~~~
"ref": "TokenPocket",
"txid": "588c6797534d09e8e0b149c06c11bfd6ca7b96f0d4bba87700fffe7a87b0d988",
"publickey": "EOSX1tWv19a9eKEQQB8Nb2wM28nYNngWP3UcSjVYqtjz6kF7yCnQ",
"wallet": "eoseoseostes",
"permissions": ["active", "owner"],
"result": 1
~~~

使用TokenPocket SDK，Dapp不需要传递callbackSchema字段以及处理相关操作，只需要调用SDK相关方法即可

sdk详情请见：https://github.com/TP-Lab/Mobile-SDK
