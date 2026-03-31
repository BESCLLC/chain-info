# 🚀 BESC Hyperchain Node Setup

Run your own **BESC Hyperchain RPC node** using Hyperledger Besu.

---

## ⚡ Quick Start (Linux)

```bash
# Install Java
sudo apt update && sudo apt install -y openjdk-17-jdk

# Install Besu
wget https://hyperledger.jfrog.io/artifactory/besu-binaries/besu/23.7.3/besu-23.7.3.tar.gz
tar -xvf besu-23.7.3.tar.gz
sudo ln -s $(pwd)/besu-23.7.3/bin/besu /usr/local/bin/besu

# Setup node
mkdir -p ~/besc-node && cd ~/besc-node

# Download config
wget https://raw.githubusercontent.com/BESCLLC/chain-info/main/genesis.json
wget https://raw.githubusercontent.com/BESCLLC/chain-info/main/config.toml

# Start node
besu --config-file=config.toml
```

---

## 🔌 RPC Endpoints

| Type       | URL                        |
|------------|---------------------------|
| HTTP RPC   | http://localhost:3545     |
| WebSocket  | ws://localhost:3546       |

---

## 🧪 Test Your Node

```bash
curl -X POST http://127.0.0.1:3545 \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}'
```

Expected response:

```json
{"jsonrpc":"2.0","id":1,"result":"0x..."}
```

---

## 🍎 macOS Setup

```bash
brew install hyperledger/besu/besu
brew install openjdk@21

mkdir -p ~/besc-node && cd ~/besc-node
wget https://raw.githubusercontent.com/BESCLLC/chain-info/main/genesis.json
wget https://raw.githubusercontent.com/BESCLLC/chain-info/main/config.toml
besu --config-file=config.toml
```

---

## 🔁 Run as a Service

```bash
sudo nano /etc/systemd/system/besu.service
```

```ini
[Unit]
Description=BESC Hyperchain Node
After=network.target

[Service]
User=root
ExecStart=/usr/local/bin/besu --config-file=/root/besc-node/config.toml
Restart=always
LimitNOFILE=4096

[Install]
WantedBy=multi-user.target
```

```bash
sudo systemctl daemon-reload
sudo systemctl enable besu
sudo systemctl start besu
```

---

## 📊 Logs

```bash
journalctl -u besu -f
```

---

## ⚠️ Troubleshooting

### 502 Bad Gateway
Your reverse proxy is pointing to the wrong port  
→ Use **3545**

---

### Port Already in Use

```bash
ss -tulnp | grep 3545
```

---

### Invalid Genesis File

```bash
cat genesis.json | jq .
```

---

## 🧠 Notes

- Do **NOT** modify `genesis.json`
- All nodes must use the **exact same genesis**
- Default ports:
  - HTTP → **3545**
  - WS → **3546**

---

## ✅ Done

Your RPC node is ready for:
- Wallets  
- dApps  
- Backend services  
