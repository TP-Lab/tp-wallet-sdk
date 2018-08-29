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
    compressedData string //压缩后的协议内容，如果使用了压缩算法，则该字段表示整个json字符串压缩后的内容，如果没有压缩，该字段可以为空
    compress    number   //0 代表不压缩，其他待定
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
    desc	string   // 交易的说明信息，钱包在付款UI展示给用户，最长不要超过128个字节，可选			     
    expired	string   // 二维码过期时间，unix时间戳
    callbackUrl string //回调url，通过此url将txId和actionId通过post请求告诉dappServer

    compressedData string //压缩后的协议内容，如果使用了压缩算法，则该字段表示整个json字符串压缩后的内容，如果没有压缩，该字段可以为空
    compress  number //对协议内容压缩方式 0 表示不压缩 其他待定
}
~~~

- 钱包执行transfer成功，将结果通过post请求告知Dapp
~~~
    protocol string
    version  string
    result  转账结果 0 成功 1 失败 2 取消
    actionId  string
    txId  string 如果转账或者取消，这个字段可以为空
    ref      string
~~~
