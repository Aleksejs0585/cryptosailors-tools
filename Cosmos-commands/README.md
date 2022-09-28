# Commands for projects that run on the Cosmos SDK

#### Init your node
```
<cosmos> init <Your-Node-Name> --chain-id <network-chain-id>
```
#### Crate your wallet
```
<cosmos> keys add <your-wallet-name>
```
#### Recover your wallet
```
<cosmos> keys add <your-wallet-name> --recover
```
#### Show your validator (VALLOPER) address
```
<cosmos> keys show <your-wallet-name> --bech val
```
#### Create your validator
```
<cosmos> tx staking create-validator \ 
 --amount="<1000000ucosmo>" \
 --pubkey=$(<cosmos> tendermint show-validator) \
 --moniker="<moniker>" \
 --chain-id="<chain-id>" \
 --from="<your-wallet-name>" \
 --commission-rate="0.1" \
 --commission-max-rate=0.15 \
 --commission-max-change-rate=0.1 \
 --min-self-delegation=1 \
 --website=<your_website> \
 --details="<Details about you>" \
 --gas=auto
 
 ```
 #### Edit your validator (remove flags, which you don't want edit)
 ```
<cosmos> tx staking edit-validator \
 --amount=<1000000ucosmo> \
 --moniker="<moniker>" \
 --chain-id=<chain-id> \
 --from=<your-wallet-name> \
 --commission-rate=0.1 \
 --commission-max-rate=0.15 \
 --commission-max-change-rate=0.1 \
 --website=<your_website>
 --details=<Details about you>
 --gas=auto
 ```
#### Check your keys
```
<cosmos> keys list
```
#### Check your balance 
```
<cosmos> q bank balances <your-wallet-address>
```
#### Delegate tokens
```
<cosmos> tx staking delegate <to-valoper> <ammountucosmo> --chain-id <chain-id> --from <your-wallet-name> --gas auto -y
```
#### Withdraw delegation rewards
```
<cosmos> tx distribution withdraw-all-rewards --chain-id <chain-id> --from <your-wallet-name> --gas auto -y
```
#### Withdraw rewards + Validator Commissions
```
<cosmos> tx distribution withdraw-rewards <your-valloper> --chain-id <chain-id> --from <your-wallet-name> --gas auto -y
```

