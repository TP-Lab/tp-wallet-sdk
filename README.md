# TP接入文档

#### 版本：v2.0，支持 EVM系列网络，EOS，TRON, IOST

### 授权登录


- 协议格式
~~~
{
    protocol	string   // 协议名，钱包用来区分不同协议，本协议为 TokenPocket
    version     string   // 协议版本信息，如2.0
    dappName    string   // dapp名字
    dappIcon    string   // dapp图标
    blockchain  string   // 网络  "eos evm网络 tron iost"
    blockchains array    // 网络 [{"chainId": "1","network": "ethereum"}]，如果该操作针对evm网络钱包或者eosio网络钱包，推荐使用该字段替换blockchain字段
    action      string   // 赋值为login
    actionId    string   // dapp 生成的，唯一标识本次操作  
    callbackUrl string   // dapp server 用于接收操作结果，如果是deeplink或者扫二维码方式拉起钱包操作，想要接收到操作结果，该字段必须提供
}
~~~

### 转账

- 协议格式
~~~
{
    protocol    string   // 协议名，钱包用来区分不同协议，本协议为 TokenPocket
    version     string   // 协议版本信息，如2.0
    dappName    string   // dapp名字，用于在钱包APP中展示，可选
    dappIcon    string   // dapp图标Url，用于在钱包APP中展示，可选
    action      string   // 转账设置为transfer,必须
    actionId    string   // dapp 生成的，唯一标识本次操作  
    blockchain  string   // 网络  "eos evm网络 tron iost"
    blockchains array    // 网络 [{"chainId": "1","network": "ethereum"}]，如果该操作针对evm网络钱包或者eosio网络钱包，推荐使用该字段替换blockchain字段
    from        string   // 付款钱包或者账号，可选
    to          string   // 收款钱包或者账号，必须
    amount      number   // 转账数量，必须
    contract    string   
    symbol      string   
    decimal     number   // evm网络使用该字段设置转账代币的decimal,其他使用precision
    precision   number   // 转账的token的精度，小数点后面的位数，必须
    memo        string   	     
    callbackUrl string   // dapp server 用于接收操作结果，如果是deeplink或者扫二维码方式拉起钱包操作，想要接收到操作结果，该字段必须提供
}
~~~


### 签名

- 协议格式
~~~
{
    protocol    string   // 协议名，钱包用来区分不同协议，本协议为 TokenPocket
    version     string   // 协议版本信息，如2.0
    dappName    string   // dapp名字，用于在钱包APP中展示，可选
    dappIcon    string   // dapp图标Url，用于在钱包APP中展示，可选
    action      string   // 转账设置为transfer,必须
    actionId    string   // dapp 生成的，唯一标识本次操作  
    blockchain  string   // 网络  "eos evm网络 tron iost"
    blockchains array    // 网络 [{"chainId": "1","network": "ethereum"}]，如果该操作针对evm网络钱包或者eosio网络钱包，推荐使用该字段替换blockchain字段
    message     string   // 签名数据
    signType    string   // evm系列网络支持ethSign ethPersonalSign
    callbackUrl string   // dapp server 用于接收操作结果的，如果是deeplink或者扫二维码方式拉起钱包操作，想要接收到操作结果，该字段必须提供
}
~~~


### 通用操作
- 协议格式
~~~
     protocol    string  // 协议名，钱包用来区分不同协议，本协议为 TokenPocket
    version     string   // 协议版本信息，如2.0
    dappName    string   // dapp名字，用于在钱包APP中展示，可选
    dappIcon    string   // dapp图标Url，用于在钱包APP中展示，可选
    action      string   // 支付时，赋值为transfer，必须
    actionId    string   // dapp 生成的，唯一标识本次操作  
    blockchain  string   // 网络  "eos evm网络 tron iost"
    blockchains array    // 网络 [{"chainId": "1","network": "ethereum"}]，如果该操作针对evm网络钱包或者eosio网络钱包，推荐使用该字段替换blockchain字段
    
    payload     string   // iost网络使用该字段传递签名数据
    actions     string   // eos 网络使用该字段传递签名数据
    txData      string   // evm网络和tron网络使用该字段传递签名数据

    callbackUrl string   // dapp server 用于接收操作结果，如果是deeplink或者扫二维码方式拉起钱包操作，想要接收到操作结果，该字段必须提供

~~~

sdk详情请见：https://github.com/TP-Lab/Mobile-SDK
