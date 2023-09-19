# TokenPocket SDK Wallet Protocol
#### Version：v2.0

### Authorize

~~~
{
    protocol	string   // protocol name TokenPocket
    version     string   // 
    dappName    string   // 
    dappIcon    string   // 
    blockchain  string   // network  "eos evm tron iost"
    blockchains array    // network [{"chainId": "1","network": "ethereum"}]，if you want do action with evm network, use blockchains replace blockchain
    action      string   // login
    actionId    string   //  
    callbackUrl string   // provided by dapp server to get result
}
~~~



### Transfer
~~~
{
    protocol	string   // protocol name TokenPocket
    version     string   // 
    dappName    string   // 
    dappIcon    string   // 
    blockchain  string   // network  "eos evm tron iost"
    blockchains array    // network [{"chainId": "1","network": "ethereum"}]，if you want do action with evm network, use blockchains replace blockchain
    action      string   // transfer
    actionId    string   //  
    from        string   // 
    to          string   // 
    amount      number   // 
    contract    string   
    symbol      string   
    decimal     number   // evm network decimal
    precision   number   // eos network precison
    memo        string   	     
    callbackUrl string   // provided by dapp server to get result
}
~~~

### Sign message

~~~
{
    protocol	string   // protocol name TokenPocket
    version     string   // 
    dappName    string   // 
    dappIcon    string   // 
    blockchain  string   // network  "eos evm tron iost"
    blockchains array    // network [{"chainId": "1","network": "ethereum"}]，if you want do action with evm network, use blockchains replace blockchain
    action      string   // sign
    actionId    string   //  
    message     string   // message to sign
    signType    string   // for evm network,support ethSign and ethPersonalSign
    callbackUrl string   // provided by dapp server to get result
}
~~~


### Sign and push common tx
~~~
    protocol	string   // protocol name TokenPocket
    version     string   // 
    dappName    string   // 
    dappIcon    string   // 
    blockchain  string   // network  "eos evm tron iost"
    blockchains array    // network [{"chainId": "1","network": "ethereum"}]，if you want do action with evm network, use blockchains replace blockchain
    action      string   // transfer
    actionId    string   //  
    
    payload     string   // used by iost network to set tx data
    actions     string   // used by eos network to set tx data
    txData      string   // used by evm and tron network to set tx data

    callbackUrl string   // provided by dapp server to get result
~~~
About "txData": [DEMO](https://github.com/TP-Lab/tp-wallet-sdk/blob/master/TxData%20Example.md)



SDK details：https://github.com/TP-Lab/Mobile-SDK
