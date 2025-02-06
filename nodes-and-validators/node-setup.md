---
description: Instruction to install and configure the ggezchaind binary
---

# Node Setup

{% hint style="info" %}
For the tutorial, it is assumed that you are using an Ubuntu LTS release.
{% endhint %}

## Install Requirements <a href="#build-requirements" id="build-requirements"></a>

### Install necessary tools

```
sudo apt update
sudo apt install -y gcc build-essential
```

### Install Go

{% hint style="info" %}
**Go 1.21+** is required.
{% endhint %}

Follow these instructions to install Go.

```
wget https://golang.org/dl/go1.21.13.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.21.13.linux-amd64.tar.gz
```

Then set these in the `.profile` in the user's home (i.e. `~/`) folder

```
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin
```

After updating your `~/.profile` you will need to source it:

```
source ~/.profile
```

### Install Cosmovisor

```
go install cosmossdk.io/tools/cosmovisor/cmd/cosmovisor@v1.6.0
```

In the `.profile` file, usually located at `~/.profile`, add:

```
export DAEMON_NAME=ggezchain
export DAEMON_HOME=$HOME/.ggezchain
export DAEMON_RESTART_AFTER_UPGRADE=true
export DAEMON_ALLOW_DOWNLOAD_BINARIES=false
```

Run `cosmovisor version` to check the cosmovisor version.

### Install Ignite CLI

```
sudo curl https://get.ignite.com/cli! | sudo bash
```

## Install ggezchaind Binary

```
# from $HOME dir
git clone https://github.com/GGEZLabs/ggezchain.git
cd ggezchain
```

Build ggezchaind binary

```
ignite chain build --release.targets linux:amd64 --output ./release --release
```

Extract build file

```
cd release 
tar -xvzf ggezchain_linux_amd64.tar.gz
```

Now run `./ggezchaind -h` to check it.

## Configure ggezchaid

### Initialize Chain <a href="#initialize-chain" id="initialize-chain"></a>

Choose a custom moniker for the node and initialize. By default, the `init` command creates the `~/.ggezchain` directory with subfolders `config` and `data`. In the `/config` directory, the most important files for configuration are `app.toml` and `config.toml`.

```
ggezchaind init custom_moniker
```

### Genesis File <a href="#genesis-file" id="genesis-file"></a>

Once the node is initialized, download the genesis file and move to the `/config` directory of the **ggezchain** home directory.

```
wget https://raw.githubusercontent.com/GGEZLabs/ggez-mainnet/refs/heads/main/genesis/genesis.json
mv genesis.json ~/.ggezchain/config/genesis.json
```

### Seeds & Peers[​](https://hub.cosmos.network/main/hub-tutorials/join-mainnet#seeds--peers) <a href="#seeds--peers" id="seeds--peers"></a>

Upon startup the node will need to connect to peers. If there are specific nodes a node operator is interested in setting as seeds or as persistent peers, this can be configured in `~/.ggezchain/config/config.toml`

```
# Comma separated list of seed nodes to connect to
seeds = "<seed node id 1>@<seed node address 1>:26656,<seed node id 2>@<seed node address 2>:26656"

# Comma separated list of nodes to keep persistent connections to
persistent_peers = "<node id 1>@<node address 1>:26656,<node id 2>@<node address 2>:26656"
```

### Gas Prices

For mainnet, the recommended `minimum-gas-prices` is `0.4uggez1`.

### REST API <a href="#rest-api" id="rest-api"></a>

{% hint style="info" %}
**Note**: This is an optional configuration.
{% endhint %}

By default, the REST API is disabled. To enable the REST API, edit the `~/.ggezchain/config/app.toml` file, and set `enable` to `true` in the `[api]` section.

```
[api]
# Enable defines if the API server should be enabled.
enable = true
# Swagger defines if swagger documentation should automatically be registered.
swagger = false
# Address defines the API server to listen on.
address = "tcp://0.0.0.0:1317"
```

### GRPC <a href="#grpc" id="grpc"></a>

{% hint style="info" %}
&#x20;**Note**: This is an optional configuration.
{% endhint %}

By default, gRPC is enabled on port `9090`. The `~/.ggezchain/config/app.toml` file is where changes can be made in the gRPC section. To disable the gRPC endpoint, set `enable` to `false`. To change the port, use the `address` parameter.

```
[grpc]
# Enable defines if the gRPC server should be enabled.
enable = true
# Address defines the gRPC server address to bind to.
address = "0.0.0.0:9090"
```

### Connect to Other Nodes <a href="#prepare-and-connect-to-other-nodes" id="prepare-and-connect-to-other-nodes"></a>

Follow this [link](https://hub.cosmos.network/main/hub-tutorials/join-mainnet#sync-options) to Sync to Other Nodes

## Initialize Cosmovisor <a href="#initialize-chain" id="initialize-chain"></a>

Before start the node we will init `cosmovisor`

```
cosmovisor init /path/to/ggezchaind
```

## Running via Background Process <a href="#running-via-background-process" id="running-via-background-process"></a>

To run the node in a background process with automatic restarts, it's recommended to use a service manager like `systemd`. To set this up run the following:

```
sudo tee /etc/systemd/system/<service name>.service > /dev/null <<EOF  
[Unit]
Description=GGEZ1 Chain Daemon
After=network-online.target

[Service]
User=$USER
ExecStart=/bin/bash -l -c 'cosmovisor run start'
Restart=always
RestartSec=3
LimitNOFILE=4096
Environment="DAEMON_HOME=$HOME/.ggezchain"
Environment="DAEMON_NAME=ggezchain"
Environment="DAEMON_ALLOW_DOWNLOAD_BINARIES=false"
Environment="DAEMON_RESTART_AFTER_UPGRADE=true"

[Install]
WantedBy=multi-user.target
EOF
```

Run the following to setup the daemon:

```
sudo systemctl daemon-reload
sudo systemctl enable <service name>
```

Then start the process and confirm that it's running.

```
sudo systemctl start <service name>
sudo systemctl status <service name>
# For live status
journalctl -u <service name> -f
```
