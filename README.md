
---

### 1. **T3RN VPS Setup**
Make sure your VPS meets the following specifications:

| VPS Plan | vCPU Cores | RAM  | Storage                  |
|----------|------------|------|--------------------------|
| VPS 1    | 4          | 8 GB | 100 GB NVMe / 400 GB SSD |
| VPS 2    | 6          | 16 GB| 200 GB NVMe / 400 GB SSD |
| VPS 3    | 8          | 24 GB| 300 GB NVMe / 1.2 TB SSD|

---

### 2. **System Update and Preparation**

Update your system and install the necessary dependencies:

```bash
sudo apt update && sudo apt upgrade -y
```

Install `figlet` for banner display:

```bash
sudo apt-get install figlet -y
figlet -f /usr/share/figlet/starwars.flf
```

---

### 3. **Download and Install T3rn Executor**

#### Fetch the Latest Executor Version:

```bash
curl -s https://api.github.com/repos/t3rn/executor-release/releases/latest | \
grep -Po '"tag_name": "\K.*?(?=")' | \
xargs -I {} wget https://github.com/t3rn/executor-release/releases/download/{}/executor-linux-{}.tar.gz
```

#### Extract the downloaded tarball and clean up:

```bash
tar -xzvf executor-linux-${LATEST_VERSION}.tar.gz
rm -rf executor-linux-${LATEST_VERSION}.tar.gz
cd executor/executor/bin
```

---

### 4. **Set Up Environment Variables**

#### Open a screen session:

```bash
screen -S t3rn
```

#### Set environment variables:

```bash
export PRIVATE_KEY_LOCAL=your-private-key
export ENABLED_NETWORKS='arbitrum-sepolia,base-sepolia,optimism-sepolia,l1rn'
export RPC_ENDPOINTS_L1RN='https://brn.calderarpc.com/'
export RPC_ENDPOINTS_ARBT='your-arbitrum-sepolia-private-rpc'
export RPC_ENDPOINTS_OPSP='your-optimism-sepolia-private-rpc'
export RPC_ENDPOINTS_BSSP='your-base-sepolia-private-rpc'
export RPC_ENDPOINTS_BLSS='your-blast-sepolia-private-rpc'
```

Additional configuration settings:

```bash
export EXECUTOR_PROCESS_PENDING_ORDERS_FROM_API=false
export EXECUTOR_PROCESS_ORDERS_API_ENABLED=false
export EXECUTOR_ENABLE_BATCH_BIDING=true
export EXECUTOR_PROCESS_BIDS_ENABLED=true
export EXECUTOR_MAX_L3_GAS_PRICE=2500
```

---

### 5. **Start the Executor**

Run the executor node:

```bash
./executor
```

You can detach the screen session anytime by pressing **Ctrl + A** then **D**.

To reattach the screen session:

```bash
screen -r t3rn
```

---

### 6. **Additional Resources:**

- **Official Documentation**: T3rn Docs
- **Faucet**: T3rn Faucet
- **Bridge UI**: T3rn Bridge
- **Community**: Twitter

---
