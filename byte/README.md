# gecko-evm Docs


### Ports 

- 8545: chain rpc
- 8546: socket rpc


### Recommended server specs

> 8 core, 16 GB ram, 500GB harddisk

### Chain details

- Network name: gecko Network
- chainId: 323
- Symbol: gecko
- RPC: rpc1.m20chain.com
- Explorer: explorer.m20chain.com

# geckochain deployment script

```
sudo apt update
sudo apt upgrade -y
sudo apt install build-essential jq -y
```

## Install Golang:

## Install latest go version https://golang.org/doc/install
```
wget -q -O - https://raw.githubusercontent.com/canha/golang-tools-install-script/master/goinstall.sh | bash -s -- --version 1.18
source ~/.profile
```

## to verify that Golang installed
```
go version
```
// Should return go version go1.18 linux/amd64

## Install the executables

```
sudo rm -rf ~/.gecko
make install

clear

## Running chain
./local.sh

## Create the service file "/etc/systemd/system/geckod.service" with the following content
```
sudo nano /etc/systemd/system/geckod.service
```

## paste following content
```
[Unit]
Description=geckod
Requires=network-online.target
After=network-online.target

[Service]
Restart=on-failure
RestartSec=3
User=root
Group=root
Environment=DAEMON_NAME=geckod
Environment=DAEMON_HOME=/root/.gecko
Environment=DAEMON_ALLOW_DOWNLOAD_BINARIES=on
Environment=DAEMON_RESTART_AFTER_UPGRADE=on
PermissionsStartOnly=true
ExecStart=/root/go/bin/gecko start --pruning="nothing"
ExecReload=/bin/kill -HUP $MAINPID
KillSignal=SIGTERM
LimitNOFILE=4096

[Install]
WantedBy=multi-user.target
## start chain node ##
```
sudo systemctl enable geckod
sudo systemctl start geckod
```
## stop chain node ##
```
sudo systemctl stop geckod
```
# Adding gecko chain on Metamask
## on metamask
![Click Add Network button ](assets/1.png)
![Click Add Network button ](assets/2.png)
![Click Add Network button ](assets/3.png)
![Click Add Network button ](assets/4.png)
![Click Add Network button ](assets/5.png)
## Add account
please create an new account on MM or import private key
