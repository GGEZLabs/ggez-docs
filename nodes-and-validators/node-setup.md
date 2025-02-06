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
