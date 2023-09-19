### EVM

##### Send ETH 

```
{
	"from": "0x5Da73693A062a11589F1b5c68434bf7eAff72366",
	"gas": "0x5208",
	"to": "0x5Da73693A062a11589F1b5c68434bf7eAff72366",
	"value": "0x2386f26fc10000"
}
```


##### Send USDT 

```
{
	"from": "0x5Da73693A062a11589F1b5c68434bf7eAff72366",
	"gas": "0x13880",
	"data": "0xa9059cbb0000000000000000000000005da73693a062a11589f1b5c68434bf7eaff7236600000000000000000000000000000000000000000000000000000000000f4240",
	"to": "0xdAC17F958D2ee523a2206206994597C13D831ec7",
}
```



### TRON

##### Send TRX 

```
{
	"visible": false,
	"txID": "f1b1380b1aaeef89d3de5b2360dc9e2fe429510ec3559fb84132b0ea4006ce2e",
	"raw_data": {
		"contract": [{
			"parameter": {
				"value": {
					"amount": 1000000,
					"owner_address": "41f90a4115ca0859c0db8415d73b3a22626506cbbe",
					"to_address": "41593a115d4e04249a7e4c02a2150b596081b37f9f"
				},
				"type_url": "type.googleapis.com\/protocol.TransferContract"
			},
			"type": "TransferContract"
		}],
		"ref_block_bytes": "8650",
		"ref_block_hash": "ef402f9a30397630",
		"expiration": 1695098220000,
		"timestamp": 1695098162988
	},
	"raw_data_hex": "0a0286502208ef402f9a3039763040e0dbe8ddaa315a67080112630a2d747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e5472616e73666572436f6e747261637412320a1541f90a4115ca0859c0db8415d73b3a22626506cbbe121541593a115d4e04249a7e4c02a2150b596081b37f9f18c0843d70ac9ee5ddaa31"
}
```


##### Send USDT 

```
{
	"visible": false,
	"txID": "0ff31369f276cd2a1f2d0f45274256cccee5095a0f4dc90a3b12af4d5fdded8b",
	"raw_data": {
		"contract": [{
			"parameter": {
				"value": {
					"data": "a9059cbb000000000000000000000000593a115d4e04249a7e4c02a2150b596081b37f9f00000000000000000000000000000000000000000000000000000000000186a0",
					"owner_address": "41f90a4115ca0859c0db8415d73b3a22626506cbbe",
					"contract_address": "41a614f803b6fd780986a42c78ec9c7f77e6ded13c"
				},
				"type_url": "type.googleapis.com\/protocol.TriggerSmartContract"
			},
			"type": "TriggerSmartContract"
		}],
		"ref_block_bytes": "865d",
		"ref_block_hash": "97a350e4aa8501ef",
		"expiration": 1695098259000,
		"fee_limit": 100000000,
		"timestamp": 1695098200128
	},
	"raw_data_hex": "0a02865d220897a350e4aa8501ef40b88cebddaa315aae01081f12a9010a31747970652e676f6f676c65617069732e636f6d2f70726f746f636f6c2e54726967676572536d617274436f6e747261637412740a1541f90a4115ca0859c0db8415d73b3a22626506cbbe121541a614f803b6fd780986a42c78ec9c7f77e6ded13c2244a9059cbb000000000000000000000000593a115d4e04249a7e4c02a2150b596081b37f9f00000000000000000000000000000000000000000000000000000000000186a070c0c0e7ddaa31900180c2d72f"
}
```