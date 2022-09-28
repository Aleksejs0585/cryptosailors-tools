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
 --amount=<1000000ucosmo> \
 --pubkey=$(<cosmos> tendermint show-validator) \
 --moniker="<moniker>" \
 --chain-id="<chain-id>" \
 --from=<your-wallet-name> \
 --commission-rate=0.1 \
 --commission-max-rate=0.15 \
 --commission-max-change-rate=0.1 \
 --min-self-delegation=1 \
 --website=<your_website> \
 --details=<Details about you> \
 --gas=auto
 
 ```
 #### Edit your validator 
 ```
<cosmos> tx staking edit-validator \
 --amount=<1000000ucosmo> \
 --pubkey=$(<cosmos> tendermint show-validator) \
 --moniker="<moniker>" \
 --chain-id="<chain-id>" \
 --from=<your-wallet-name> \
 --commission-rate=0.1 \
 --commission-max-rate=0.15 \
 --commission-max-change-rate=0.1 \
 --website=<your_website>
 --details=<Details about you>
 --gas=auto
 ```
