# Recommended System Requirements
* 2 CPU Cores
* 4 GB RAM
* 20 GB Disk Space
* Create your own `Ethereum Hoodi RPC` in [Alchemy](https://dashboard.alchemy.com/) or [QuickNode](https://dashboard.quicknode.com/) or [ankr](https://www.ankr.com/rpc).
--------

# important
 
This guide is for users who have already completed the project tasks on Sepolia.
Make sure that both of your wallet addresses have received Hoodi faucet tokens before getting started.


[faucet1](https://stakely.io/faucet/ethereum-hoodi-testnet-eth)
[faucet2](https://faucet.drosera.io/)


---------

### Install Dependecies
```
sudo apt-get update && sudo apt-get upgrade -y
```
```
sudo apt install curl ufw iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli libgbm1 pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev  -y
```
### Install Docker
```bash
sudo apt update -y && sudo apt upgrade -y
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done

sudo apt-get update
sudo apt-get install ca-certificates curl gnupg
sudo install -m 0755 -d /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
sudo chmod a+r /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update -y && sudo apt upgrade -y

sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin

```
----

## 1. Configure Enviorments
**Drosera CLI**:
```bash
curl -L https://app.drosera.io/install | bash
```
```
source /root/.bashrc
```
```
droseraup
```

**Foundry CLI**:
```
curl -L https://foundry.paradigm.xyz | bash
```
```
source /root/.bashrc
```
```
foundryup
```

**Bun:**
```
curl -fsSL https://bun.sh/install | bash
```
```
source /root/.bashrc
```

---

## 2. Deploy Contract & Trap
```bash
mkdir my-drosera-trap
```
```bash
cd my-drosera-trap
```
**Replace `Github_Email` & `Github_Username`:**
```bash
git config --global user.email "Github_Email"
git config --global user.name "Github_Username"
```
**Initialize Trap**:
```
forge init -t drosera-network/trap-foundry-template
```
**Compile Trap**:
```bash
curl -fsSL https://bun.sh/install | bash

source /root/.bashrc

bun install
```
```bash
forge build
```

##  Whitelist Your Operator
** Edit Trap configuration:**
```bash
cd my-drosera-trap
nano drosera.toml
```
Add the following codes at the bottom of `drosera.toml`:
```toml
private_trap = true
whitelist = ["Operator_Address1","Operator_Address2"]
```
* Replace `Operator_Address` with your EVM wallet `Public Address` between " " symbols
* Your `Public Address` is your `Operator_Address`.

**2- Deploy Trap:**

use Operator_Address1 pv-key

```bash
DROSERA_PRIVATE_KEY=xxx drosera apply
```
* Replace `xxx` with your EVM wallet `privatekey`
* If RPC issue, use `DROSERA_PRIVATE_KEY=xxx drosera apply --eth-rpc-url RPC` and replace `RPC` with your own.
* Enter the command, when prompted, write `ofc` and press Enter.

Your Trap should be private now with your operator address whitelisted internally.



![image](https://github.com/user-attachments/assets/6d1161f1-4423-4ce6-a1a2-77ce567186dc)


## 3. Check Trap in Dashboard
1- Connect your Drosera EVM wallet: https://app.drosera.io/

2- Click on `Traps Owned` to see  your deployed Traps OR search your Trap address.

![image](https://github.com/user-attachments/assets/9c39eea0-0aaf-417d-8552-765ff33f8a5e)

---

## 4. Bloom Boost Trap
Open your Trap on Dashboard and Click on `Send Bloom Boost` and deposit some `Hoodi ETH` on it.

![image](https://github.com/user-attachments/assets/2f5216fd-fdf9-4732-96d0-959b3fbce479)

## 5. Fetch Blocks
```bash
drosera dryrun
```






## 6. Operator CLI
```bash
cd ~
```
```bash
# Download
curl -LO https://github.com/drosera-network/releases/releases/download/v1.20.0/drosera-operator-v1.20.0-x86_64-unknown-linux-gnu.tar.gz

# Install
tar -xvf drosera-operator-v1.20.0-x86_64-unknown-linux-gnu.tar.gz
```
* Currently the Operator CLI version is `v1.20.0`. Verify the latest version [here](https://github.com/drosera-network/releases/releases)
* You have to get the link of `drosera-operator-v1.x.x-x86_64-unknown-linux-gnu.tar.gz`

Test the CLI with `./drosera-operator --version` to verify it's working.
```console
# Check version
./drosera-operator --version

# Move path to run it globally
sudo cp drosera-operator /usr/bin

# Check if it is working
drosera-operator
```

## 7. Install Docker image
```
docker pull ghcr.io/drosera-network/drosera-operator:latest
```

---

## 8. Register Operator

use pv-key from Operator_Address1

```bash
drosera-operator register --eth-rpc-url https://rpc.hoodi.ethpandaops.io --eth-private-key PV_KEY
```

use pv-key from Operator_Address1

```bash
drosera-operator register --eth-rpc-url https://rpc.hoodi.ethpandaops.io --eth-private-key PV_KEY
```

* Replace `PV_KEY` with your Drosera EVM `privatekey`. We use the same wallet as our trap wallet.

---




## 9. Open Ports
```bash
# Enable firewall
sudo ufw allow ssh
sudo ufw allow 22
sudo ufw enable

# Allow Drosera ports
sudo ufw allow 31313/tcp
sudo ufw allow 31314/tcp
sudo ufw allow 31315/tcp
sudo ufw allow 31316/tcp
```

---


## 10. Install & Run Operator

```
mkdir Drosera-Network
```

```
cd Drosera-Network
```
creat file 

```
nano .env
```
Fill `.env` with the following values:  
- Use the private key of `operator1` and `operator2`  
- Use your VPS IP address


```
ETH_PRIVATE_KEY=
ETH_PRIVATE_KEY2=
VPS_IP=
```


creat new file for dependis for run docker:

```
nano docker-compose.yaml
```
use this :

```
version: '3'
services:
  drosera1:
    image: ghcr.io/drosera-network/drosera-operator:latest
    container_name: drosera-node1
    network_mode: host
    volumes:
      - drosera_data1:/data
    command: node --db-file-path /data/drosera.db --network-p2p-port 31313 --server-port 31314 --eth-rpc-url <use-rpc> --eth-backup-rpc-url https://rpc.hoodi.ethpandaops.io --drosera-address 0x91cB447BaFc6e0EA0F4Fe056F5a9b1F14bb06e5D --eth-private-key ${ETH_PRIVATE_KEY} --listen-address 0.0.0.0 --network-external-p2p-address ${VPS_IP} --disable-dnr-confirmation true
    restart: always

  drosera2:
    image: ghcr.io/drosera-network/drosera-operator:latest
    container_name: drosera-node2
    network_mode: host
    volumes:
      - drosera_data2:/data
    command: node --db-file-path /data/drosera.db --network-p2p-port 31315 --server-port 31316 --eth-rpc-url <use-rpc> --eth-backup-rpc-url https://rpc.hoodi.ethpandaops.io --drosera-address 0x91cB447BaFc6e0EA0F4Fe056F5a9b1F14bb06e5D --eth-private-key ${ETH_PRIVATE_KEY2} --listen-address 0.0.0.0 --network-external-p2p-address ${VPS_IP} --disable-dnr-confirmation true
    restart: always

volumes:
  drosera_data1:
  drosera_data2:
```

pls replace `<use-rpc>` with your RPC URL


### 11. Opt-in 2nd Operator

**Method**: via CLI
```bash
drosera-operator optin --eth-rpc-url https://rpc.hoodi.ethpandaops.io --eth-private-key 1nd_Operator_Privatekey --trap-config-address Trap_Address
```
* Replace `1nd_Operator_Privatekey`  & `Trap_Address`

```bash
drosera-operator optin --eth-rpc-url https://rpc.hoodi.ethpandaops.io --eth-private-key 2nd_Operator_Privatekey --trap-config-address Trap_Address
```
* Replace `2nd_Operator_Privatekey`  & `Trap_Address`

### 12. run Operators
```bash
cd ~/Droseta-Network
docker compose up -d
```
* You will get Green Blocks after a while! wait for 10 min pls 

check dashboar 

![image](https://github.com/user-attachments/assets/e639c5e9-cacd-42f4-8c4e-82597a6a71fd)
