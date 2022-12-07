# Testing the contract
- Install Contract : 
	`88.52748 CSPR	($2.59)`
	ContractHash : `fdc89ab04fd32afbd3929189bc7021a1702bb8786ed584b5970469f5b9ac3d32`
	ContractLink : https://testnet.cspr.live/contract/fdc89ab04fd32afbd3929189bc7021a1702bb8786ed584b5970469f5b9ac3d32

- Testing Mint Method : `4.21051 CSPR	($0.12)`
	price : 100cspr
	recipient : DroplinkTest1 with hash : `account-hash-1d157a96564cc5743a4dc6f489f0a49ba57482165af3e1ace934ecd3d86edad2`
	amount : 1000
	-command :
	```bash
	casper-client put-deploy --node-address http://144.76.110.71:7777 --chain-name casper-test --secret-key deploy/keys/matin2_secret_key.pem --session-hash fdc89ab04fd32afbd3929189bc7021a1702bb8786ed584b5970469f5b9ac3d32 --payment-amount 10000000000 --session-entry-point "mint" --session-arg "metadata:String='{\"name\" : \"good1\", \"token_uri\" : \"Qma5d2ofV94oXP4ojxt5pwN6WvEaBAHXQ8cLX1zaxWpdkJ\" , \"checksum\":\"3c06868a39c5e0b6a121d1a4e151b198dafafe839ebb9670dccdbbd437ad4fe0\"}'" --session-arg "price:u256='100000000000'" --session-arg "amount:u64='1000'" --session-arg "recipient:key='account-hash-1d157a96564cc5743a4dc6f489f0a49ba57482165af3e1ace934ecd3d86edad2'"
	```

- Testing Approve Method : `3.30966 CSPR	($0.10)`
	publisher-account : DroplinkTest2 with hash : `account-hash-1a233ce41f1313be69faf792f0a5c606891e6b0aa947301adc1b2dcfbee5c021`
	amount : 200
	percentage : 10% (hardcoded, edit it at main.rs:172)
	holder_id : 1
	-command : 
	```bash
		casper-client put-deploy --node-address http://144.76.110.71:7777 --chain-name casper-test --secret-key deploy/keys/DropLinkTest1_secret_key.pem --session-hash fdc89ab04fd32afbd3929189bc7021a1702bb8786ed584b5970469f5b9ac3d32 --payment-amount 10000000000 --session-entry-point "approve" --session-arg "publisher-account:key='account-hash-1a233ce41f1313be69faf792f0a5c606891e6b0aa947301adc1b2dcfbee5c021'" --session-arg "amount:u64='200'" --session-arg "holder_id:u64='1'"
	```

- Testing Buy Method : 
	TODO: we need a method to return the price of a single approved_id or token
	approved_id : 1
	Customer : DropLinkTest2 with hash : `account-hash-1a233ce41f1313be69faf792f0a5c606891e6b0aa947301adc1b2dcfbee5c021`
	amount : 3 (3*100 = 300 cspr)
	-command :
	```bash
		casper-client put-deploy -n http://144.76.110.71:7777 --chain-name casper-test --payment-amount 100000000000 -k deploy/keys/DropLinkTest2_secret_key.pem --session-path deploy/buy_contract.wasm --session-arg "amount:u64='3'" --session-arg "approved_id:u64='1'" --session-arg "contract_hash:key='hash-fdc89ab04fd32afbd3929189bc7021a1702bb8786ed584b5970469f5b9ac3d32'"
	```
