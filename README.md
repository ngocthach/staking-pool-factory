# Exercise: Modify Staking Pool Factory Contract

Code path: https://github.com/ngocthach/staking-pool-factory/tree/main/staking-pool-factory

Modify error message when deposit amount < 30 TGas (30 Near)

cd staking-pool-factory

rustup target add wasm32-unknown-unknown

./build.sh


# Login to NEAR
near login

# Deploy wasm to the <accountId> account
near deploy ngocthach2020.testnet /Users/ngocthach/blockchain/first_project/near/core-contracts/staking-pool-factory/res/staking_pool_factory.wasm 

Starting deployment. Account id: ngocthach2020.testnet, node: https://rpc.testnet.near.org, helper: https://helper.testnet.near.org, file: /Users/ngocthach/blockchain/first_project/near/core-contracts/staking-pool-factory/res/staking_pool_factory.wasm
Transaction Id 91BMCc64KDp4FT1xVr27qa9xqPF3Jv3K9AiyPpFCLuKy
To see the transaction in the transaction explorer, please open this url in your browser
https://explorer.testnet.near.org/transactions/91BMCc64KDp4FT1xVr27qa9xqPF3Jv3K9AiyPpFCLuKy
Done deploying to ngocthach2020.testnet


# View methods
near view ngocthach2020.testnet <method-name>

# Call
near call ngocthach2020.testnet new \
'{"staking_pool_whitelist_account_id": "ngocthach1207.testnet"}' \
 --accountId ngocthach2020.testnet


Scheduling a call: ngocthach2020.testnet.new({"staking_pool_whitelist_account_id": "ngocthach2020.testnet"})
Doing account.functionCall()
Transaction Id DtmccjqegrhmbfXWqM7VABjU3iY1MQsuLnyX27nWMbwG
To see the transaction in the transaction explorer, please open this url in your browser
https://explorer.testnet.near.org/transactions/DtmccjqegrhmbfXWqM7VABjU3iY1MQsuLnyX27nWMbwG


--- Test ---
+ Fail case due to deposit smaller than 30 Near:

near call ngocthach2020.testnet create_staking_pool \
'{"staking_pool_id": "ngocthach2020_pool_id", "owner_id": "ngocthach2020.testnet", "stake_public_key": "KuTCtARNzxZQ3YvXDeLjx83FDqxv2SdQTSbiq876zR7", "reward_fee_fraction": {"numerator": 10, "denominator": 100} }' \
 --accountId ngocthach2020.testnet

 ExecutionError: "Smart contract panicked: panicked at 'Not enough attached deposit to complete staking pool creation. It must be greater than 30 Near', src/lib.rs:147:9"


 + Success case: 


near call ngocthach2020.testnet create_staking_pool \
'{"staking_pool_id": "ngocthach2020_pool_id", "owner_id": "ngocthach2020.testnet", "stake_public_key": "KuTCtARNzxZQ3YvXDeLjx83FDqxv2SdQTSbiq876zR7", "reward_fee_fraction": {"numerator": 10, "denominator": 100} }' \
 --accountId ngocthach2020.testnet --amount 34 --gas 300000000000000


near call ngocthach2020.testnet on_staking_pool_create \
'{"staking_pool_account_id": "ngocthach2020_pool_id.ngocthach2020.testnet", "attached_deposit": "34", "predecessor_account_id": "ngocthach2020.testnet"}' \
 --accountId ngocthach2020.testnet








