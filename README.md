
---  

# **T3rn Executor Node Setup Guide**  

## **1. VPS Setup**  
To participate in the T3rn network, you'll need a reliable VPS. Consider using **Contabo VPS** or any other provider that meets the required specifications:  

| VPS Plan  | vCPU Cores | RAM  | Storage            |  
|-----------|-----------|------|-------------------|  
| VPS 1     | 4         | 8 GB  | 100 GB NVMe / 400 GB SSD |  
| VPS 2     | 6         | 16 GB | 200 GB NVMe / 400 GB SSD |  
| VPS 3     | 8         | 24 GB | 300 GB NVMe / 1.2 TB SSD |  

---  

## **2. System Update and Preparation**  
First, ensure your system is updated and install necessary dependencies:  

```bash
sudo apt update && sudo apt upgrade -y

# Install figlet for banner display
sudo apt-get install figlet -y
figlet -f /usr/share/figlet/starwars.flf
```  

---  

## **3. Download and Install T3rn Executor**  

1. Fetch the latest executor version:  
   ```bash
   curl -s https://api.github.com/repos/t3rn/executor-release/releases/latest | \
grep -Po '"tag_name": "\K.*?(?=")' | \
xargs -I {} wget https://github.com/t3rn/executor-release/releases/download/{}/executor-linux-{}.tar.gz
   ```  

2. Extract the downloaded archive and clean up:  
   ```bash
   tar -xzvf executor-linux-${LATEST_VERSION}.tar.gz
   rm -rf executor-linux-${LATEST_VERSION}.tar.gz
   cd executor/executor/bin
   ```  

---  

## **4. Set Up Environment Variables**  

Before starting the node, configure the necessary environment variables:  

```bash
screen -S t3rn   # Open a screen session

export NODE_ENV=testnet
export LOG_LEVEL=debug
export LOG_PRETTY=false
export EXECUTOR_PROCESS_ORDERS=true
export EXECUTOR_PROCESS_CLAIMS=true
export EXECUTOR_MAX_L3_GAS_PRICE=50
export EXECUTOR_PROCESS_PENDING_ORDERS_FROM_API=false

# Replace with your private key  
export PRIVATE_KEY_LOCAL=<replace-your-private-key>  

# Enable supported networks  
export ENABLED_NETWORKS='arbitrum-sepolia,base-sepolia,optimism-sepolia,l1rn'
```  

---  

## **5. Start the Executor**  

Once everything is set up, start the executor node with:  
```bash
./executor
```  

You can detach the screen session anytime by pressing `Ctrl + A` then `D`.  
To reattach the screen session, run:  
```bash
screen -r t3rn
```    

---

## **Additional Resources**  
- Official Documentation: [T3rn Docs](https://docs.t3rn.io)  
- Faucet: [T3rn Faucet](https://faucet.brn.t3rn.io/)  
- Bridge UI: [T3rn Bridge](https://bridge.t1rn.io)  
- Community:    
  - [Twitter](https://x.com/Swarup54502259)  

---
