# In this tutorial, we will set up StateSync configuration.
- StateSync - helps to synchronize almost from the last block through the distributor node. This helps to synchronize the node almost immediately after it is launched.
- To run StateSync, we need two servers. On the first server `distributing` we will keep a constantly working and synchronized node. On the second server `Consumer` we will run a fresh node and synchronize it using StateSync.
- **Please Note** - StateSync may **NOT** always start immediately. This is her main drawback. This depends on the number of peers that have connected and synchronized from the "Distributor" node. Sometimes projects don't support StateSync.

## 1. Configuration of `config.toml` and `app.toml` on `distributing` server
In the СOSMOS project, after the initiation of the node by command `cosmos init`, will be created `.cosmos` folder. Inside this folder located all related info about your node and validator.

Input your value instead `<.comsos>` and delete `<>`
- Example `FOLDER=.nibid`
```
FOLDER=<.cosmos>
```
```
sed -i.bak -e "s%^laddr = \"tcp://127.0.0.1:26657\"%laddr = \"tcp://0.0.0.0:26657\"%" $HOME/$FOLDER/config/config.toml
sed -i.bak -e "s/^pruning *=.*/pruning = \"custom\"/" $HOME/$FOLDER/config/app.toml
sed -i.bak -e "s/^pruning-interval *=.*/pruning-interval = \"17\"/" $HOME/$FOLDER/config/app.toml
sed -i.bak -e "s/^pruning-keep-every *=.*/pruning-keep-every = \"2000\"/" $HOME/$FOLDER/config/app.toml
sed -i.bak -e "s/^snapshot-interval *=.*/snapshot-interval = \"2000\"/" $HOME/$FOLDER/config/app.toml
sed -i.bak -e "s/^snapshot-keep-recent *=.*/snapshot-keep-recent = \"5\"/" $HOME/$FOLDER/config/app.toml
```

## 2. Pull out your ID and IP
Change `<cosmos>` on your binary name and delete `<>`
- Example `echo -e "$(nibid tendermint sh...`
```
echo -e "$(<cosmos> tendermint show-node-id)@$(curl -s ifconfig.me)$(grep -A 3 "\[p2p\]" ~/$FOLDER/config/config.toml | egrep -o ":[0-9]+")"
```
The output should be something like:
`8dd57aaef961d9943d5d7f0fcae6683c331065a3@81.34.157.35:26656` This peer we will use in our `Consumer` server later.

## 3. Check your IP

Restart your node than do:
```
echo http://$(wget -qO- eth0.me):26657/
```
You should receive `http://81.34.157.35:26657/` and then try to open it in your browser. This IP address we will use at our `Consumer` server later.

<p align="left">
 <img src="https://i.postimg.cc/6qPvHs75/Untitled.jpg.jpg"width="300"/></a>
</p>

## 4. On new server `Consumer`
Install node on the new server. Do an `init` and proceed to configure `config.toml` and `app.toml`

Input your value instead `<.comsos>` and delete `<>`
- Example `FOLDER=.nibid`
```
FOLDER=<.cosmos>
```
```
PEERS=8dd57aaef961d9943d5d7f0fcae6683c331065a3@81.34.157.35:26656
```
```
SNAP_RPC=81.34.157.35:26657
```
```
LATEST_HEIGHT=$(curl -s $SNAP_RPC/block | jq -r .result.block.header.height); \
BLOCK_HEIGHT=$((LATEST_HEIGHT - 2000)); \
TRUST_HASH=$(curl -s "$SNAP_RPC/block?height=$BLOCK_HEIGHT" | jq -r .result.block_id.hash)
```
```
echo $LATEST_HEIGHT $BLOCK_HEIGHT $TRUST_HASH
```

<p align="center">
 <img src="https://i.postimg.cc/X7F3GVRk/Untitled.jpg"width="900"/></a>
</p>

```
sed -i.bak -e  "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" ~/$FOLDER/config/config.toml
sed -i.bak -E "s|^(enable[[:space:]]+=[[:space:]]+).*$|\1true| ; \
s|^(rpc_servers[[:space:]]+=[[:space:]]+).*$|\1\"$SNAP_RPC,$SNAP_RPC\"| ; \
s|^(trust_height[[:space:]]+=[[:space:]]+).*$|\1$BLOCK_HEIGHT| ; \
s|^(trust_hash[[:space:]]+=[[:space:]]+).*$|\1\"$TRUST_HASH\"| ; \
s|^(seeds[[:space:]]+=[[:space:]]+).*$|\1\"\"|" ~/$FOLDER/config/config.toml
```
**Start your node.**

#

🔰[Our Telegram Channel](https://t.me/CryptoSailorsAnn)

🔰[Our WebSite](cryptosailors.tech)

🔰[Our Twitter](https://twitter.com/Crypto_Sailors)

🔰[Our Youtube](https://www.youtube.com/@CryptoSailors)

#### Guide created by 
Pavel-LV | C.Sailors#7698 / @SeaInvestor
