# TokenPocket Protocol

#### Version：v1.0

### Login

- Param
~~~
{
    protocol	string   //protocol name here is TokenPocket
    version     string   // protocol version here is v1.0
    dappName    string   // optional
    dappIcon    string   // optional
    blockchain  string   // wallet type(eos bos eth moac )
    wallet      string   // account name
    action      string   // neccessary here is login
    actionId    string   // optional   
    callbackUrl string   // optional
    expired	    string   //expire time in seconds
    memo	    string   // optional
}
~~~

- Success data
~~~
{
   "sign": "SIG_K1_KZL9eR4cCQCJHpYHbh44yGrDqu4w8hHzQwb1xTk4Mcd4czqpw4jJUgg9DnWXzE3r",
   "timestamp": "1546613919", //in seconds
   "wallet": "eoseoseosacc", //account name
   "ref": "TokenPocket",
   "action":"login",
   "actionId":"ljsdjljdljf-xjlsdjfkj" //actionId from dapp
   "publickey": "EOS2TtWv19a9eYEQYB8NbGCM28nQNngWP4UcSjVYqtEz6kF7yCnPX",
   "permissions": ["active", "owner"],
   "result": 1
}
~~~

Cancel data
~~~
{
   "action":"login",
   "actionId":"ljsdjljdljf-xjlsdjfkj" 
   "result": 0
}
~~~


### Token transfer

- Param
~~~
{
    protocol    string   //protocol name here is TokenPocket
    version     string   // protocol version here is v1.0
    dappName    string   // optional
    dappIcon    string   // optional
    action      string   // neccessary here is transfer
    actionId    string   // optional
    blockchain  string   //wallet type(eos bos eth moac )
    from        string   // optional
    to          string   // neccessary
    amount      number   // neccessary
    contract    string   // neccessary
    symbol      string   // neccessary
    precision   number   // neccessary
    memo        string   //optional		     
    expired	    string   // expire time in seconds
}
~~~


- Success data
~~~
"ref": "TokenPocket",
"txID": "588c6797534d09e8e0b149c06c11bfd6ca7b96f0d4bba87700fffe7a87b0d988",
"publickey": "EOSX1tWv19a9eKEQQB8Nb2wM28nYNngWP3UcSjVYqtjz6kF7yCnQ",
"action":"transfer",
"actionId":"ljsdljf-xljlsdjfl" //from dapp
"wallet": "eoseoseostes",
"permissions": ["active", "owner"],
"result": 1
~~~

- Cancel data
~~~
"action":"transfer",
"actionId":"ljsdljf-xljlsdjfl" //from dapp
"result": 0
~~~


### Push transaction
- Param
~~~
    protocol    string  //protocol name here is TokenPocket
    version     string   // protocol version here is v1.0
    dappName    string   // optional
    dappIcon    string   // optional
    action      string   // neccessary here is pushTransaction
    actionId    string   // optional 
    blockchain  string   //wallet type(eos bos eth moac )
    actions     string   //actions data
    memo    string  
~~~



- Success data
~~~
"ref": "TokenPocket",
"txID": "588c6797534d09e8e0b149c06c11bfd6ca7b96f0d4bba87700fffe7a87b0d988",
"publickey": "EOSX1tWv19a9eKEQQB8Nb2wM28nYNngWP3UcSjVYqtjz6kF7yCnQ",
"action":"pushTransaction",
"actionId":"ljsdljf-xljlsdjfl" 
"wallet": "eoseoseostes",
"permissions": ["active", "owner"],
"result": 1
~~~

- Cancel data
~~~
"action":"pushTransaction",
"actionId":"ljsdljf-xljlsdjfl"
"result": 0
~~~
