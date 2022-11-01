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
  --website=<your_website> \
  --details=<Details about you> \
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
#### If you run more than one Cosmos networks, you should update your peers. Don't forget to change folder direction on the end of the commands.
```
sed -i.bak -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:16658\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:16657\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:16060\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:16656\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":16660\"%" $HOME/.<cosmos>/config/config.toml
```
```
sed -i.bak -e "s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:19090\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:19091\"%" $HOME/.<cosmos>/config/app.toml
```
```
sed -i.bak -e "s%^node = \"tcp://localhost:26657\"%node = \"tcp://localhost:16657\"%" $HOME/.<cosmos>/config/client.toml
```
