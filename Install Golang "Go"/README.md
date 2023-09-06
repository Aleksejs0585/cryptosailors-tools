<p align="center">
 <img src="https://miro.medium.com/max/1400/1*CdjOgfolLt_GNJYBzI-1QQ.jpeg"width="900"/></a>
</p>

### 1. Update your server.
```
sudo apt update && sudo apt upgrade -y
```
```
sudo apt install make clang pkg-config libssl-dev libclang-dev build-essential git curl ntp jq llvm tmux htop screen unzip cmake -y
```
### 2. If you installing Golang "Go" on clear server you need input following commands.
```
sudo rm -rvf /usr/local/go/
sudo rm -rvf go
cd /usr/src
sudo rm -Rf go*
sudo wget https://go.dev/dl/`curl -s https://go.dev/dl/?mode=json | jq -r '.[0].version'`.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go*.linux-amd64.tar.gz
cat <<EOF >> ~/.bash_profile
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export GO111MODULE=on
export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin
EOF
source ~/.bash_profile
go version
sudo rm -rf /usr/src/go*.linux-amd64.tar.gz
cd ~
```

### 3. If you would like delete your Golang "Go" from your server you need input following commands.
```
sudo rm -rvf /usr/local/go/
```
```
sudo rm -rvf go
```
🔰[Our Telegram Channel](https://t.me/CryptoSailorsAnn)

🔰[Our WebSite](cryptosailors.tech)

🔰[Our Twitter](https://twitter.com/Crypto_Sailors)

#### Guide created by 
Pavel-LV | C.Sailors#7698 / @SeaInvestor
