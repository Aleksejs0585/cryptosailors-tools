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

[Проверить высоту блоки и синхронизацию ноды]
curl -s localhost:26657/status
<defundd> status 2>&1 | jq .SyncInfo

#Ределегация токенов
<gravity> tx staking redelegate <from-valoper> <to-valper> <ammount><ugraviton> --chain-id gravity-bridge-1 --from <wallet-address> --gas auto

#Делигрование токеноа
gravity tx staking delegate <to-valoper> <ammount><ugraviton> --chain-id gravity-bridge-1 --from <wallet-address> --gas auto

#Вывести все награды
gravity tx distribution withdraw-all-rewards --chain-id gravity-bridge-1 --from <wallet-address> --gas auto

Команда на выплату комиссионых с валидатора
axelard tx distribution withdraw-rewards <axelarvaloper> --commission -y --from validator  --chain-id <axelar-testnet-lisbon-3> --gas=auto --gas-adjustment 1.5

#Проверка готовности нод
curl -s 127.0.0.1:26657/consensus_state | jq .result.round_state.height_vote_set[0].prevotes_bit_array

#Показать Node-Id
defundd tendermint show-node-id

#Показать сколько пиров подключилось (Нужно изменить prometeus c false на true)
curl -s http://localhost:26660/ | grep tendermint_p2p_peers

#Выташить свой пир
echo -e "$(<defundd> tendermint show-node-id)@$(curl -s ifconfig.me)$(grep -A 3 "\[p2p\]" ~/<.defund>/config/config.toml | egrep -o ":[0-9]+")"

#Показать неактивный сет валидаторов
uptickd q staking validators -o json --limit=1000 | jq '.validators[] | select(.status=="BOND_STATUS_UNBONDED")' | jq -r '.tokens + " - " + .description.moniker' | sort -gr | nl

#Показать активный сет валидаторов
uptickd q staking validators -o json --limit=1000 | jq '.validators[] | select(.status=="BOND_STATUS_BONDED")' | jq -r '.tokens + " - " + .description.moniker' | sort -gr | nl

#IBC транзакция
icad tx ibc-transfer transfer transfer channel-0 quick13h9fg04k9f3qje2n3s502taf8fmwcls9ymdedy 1uatom --from Pavel-Lv --chain-id kqcosmos-1 -y

#Если стоит две ноды на одном сервере то может запросить:
--node "tcp://127.0.0.1:26652"

#Выйти из тюрми
gravity tx slashing unjail --from gravity1pske98rrpg6vwayjauncjqvfs6tj06xh2surp0  --chain-id=gravity-bridge-3

#Проголосовать в Proposal
gravity tx gov vote 67 yes --chain-id gravity-bridge-3 --gas auto --from gravity1pske98rrpg6vwayjauncjqvfs6tj06xh2surp0 -y

#Если стоит две ноды на одном сервере то в папке, где находяться файлы сonfig.toml и app.toml нужно заменить
sed -i.bak -e "s%^proxy_app = \"tcp://127.0.0.1:26658\"%proxy_app = \"tcp://127.0.0.1:26653\"%; s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://127.0.0.1:26652\"%; s%^pprof_laddr = \"localhost:6060\"%pprof_laddr = \"localhost:6061\"%; s%^laddr = \"tcp://0.0.0.0:26656\"%laddr = \"tcp://0.0.0.0:26651\"%; s%^prometheus_listen_addr = \":26660\"%prometheus_listen_addr = \":26655\"%" config.toml
sed -i.bak -e "s%^address = \"0.0.0.0:9090\"%address = \"0.0.0.0:9092\"%; s%^address = \"0.0.0.0:9091\"%address = \"0.0.0.0:9093\"%" app.toml
  
