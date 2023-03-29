# In this tutorial, we will set up Snapshot configuration.
- Snapshot - helps to synchronize the node almost immediately after it is launched.
- To run Snapshot, we need two servers. On the first server `distributing` we will keep a constantly working and synchronized node. On the second server `Consumer` we will run a fresh node and synchronize it using Snapshot.

## 1. Configuration of `app.toml` on `distributing` server
In the СOSMOS project, after the initiation of the node by command `cosmos init`, will be created `.cosmos` folder. Inside this folder located all related info about your node and validator.

Input your value instead `<.comsos>` and delete `<>`
- Example `FOLDER=.nibid`
```
FOLDER=<.cosmos>
```
Before do a snapshot you should correctly prune your node and setup proper configuration in your `app.toml`. The line `pruning-interval` must contain natural numbers.In this tutorial i will `pruning-interval=23`. Try to setup diferent number like 3,5,7,11,13,17, and etc.
```
sed -i.bak -e "s/^pruning *=.*/pruning = \"custom\"/" $HOME/$FOLDER/config/app.toml
sed -i.bak -e "s/^pruning-keep-recent *=.*/pruning-keep-recent = \"100\"/" $HOME/$FOLDER/config/app.toml
sed -i.bak -e "s/^pruning-keep-every *=.*/pruning-keep-every = \"0\"/" $HOME/$FOLDER/config/app.toml
sed -i.bak -e "s/^pruning-interval *=.*/pruning-interval = \"23\"/" $HOME/$FOLDER/config/app.toml
```
**Restart your node**

Now stop your node and continue to prepare your snapshot

**Stop your node**
Open new screen  or tmux session
```
screen -S archive
```
```
NAME_ARCHIVE=archive_data
tar -zcvf $NAME_ARCHIVE.tar.gz $FOLDER/data && \
echo -e "\033[0;31m wget http://$(wget -qO- eth0.me):8000/$NAME_ARCHIVE.tar.gz \033[0m" && \
python3 -m http.server 8000
```
If evrything is correct, you wil get a link

<p align="center">
 <img src="https://i.postimg.cc/59LfVfTW/Untitled.jpg"width="600"/></a>
</p>

## 4. On new server `Consumer`
Install node on the new server. Do an `init` and download archive from the `distribution` server.

Input your value instead `<.comsos>` and delete `<>`
- Example `FOLDER=.nibid`
```
FOLDER=<.cosmos>
```
Input peers
```
PEERS=<YOUR_PEERS>
```
```
sed -i.bak -e  "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" ~/$FOLDER/config/config.toml
```
```
cp $HOME/$FOLDER/data/priv_validator_state.json $HOME/$FOLDER/priv_validator_state.json.backup
rm -rf $HOME/$FOLDER/data
```
input your link
```
wget http://78.47.12.250:8000/archive_data.tar.gz -O - | tar -xzf - -C $HOME

mv $HOME/$FOLDER/priv_validator_state.json.backup $HOME/$FOLDER/data/priv_validator_state.json
```
**Start your node.**

#

🔰[Our Telegram Channel](https://t.me/CryptoSailorsAnn)

🔰[Our WebSite](cryptosailors.tech)

🔰[Our Twitter](https://twitter.com/Crypto_Sailors)

🔰[Our Youtube](https://www.youtube.com/@CryptoSailors)

#### Guide created by 
Pavel-LV | C.Sailors#7698 / @SeaInvestor
