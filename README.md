🚀 BESC Hyperchain — Full Node Setup Guide

This guide will help you quickly spin up a working RPC node for BESC Hyperchain using Hyperledger Besu.

📦 1. Install Besu

Linux

wget https://hyperledger.jfrog.io/artifactory/besu-binaries/besu/23.7.3/besu-23.7.3.tar.gz
tar -xvf besu-23.7.3.tar.gz
sudo ln -s $(pwd)/besu-23.7.3/bin/besu /usr/local/bin/besu

macOS

brew install hyperledger/besu/besu


☕ 2. Install Java

Linux

sudo apt update
sudo apt install openjdk-17-jdk

macOS

brew install openjdk@21


✅ 3. Verify Installation

besu --version


📁 4. Setup Node Directory

mkdir -p ~/besc-node
cd ~/besc-node


🌐 5. Download Chain Configuration

wget https://raw.githubusercontent.com/BESCLLC/chain-info/main/genesis.json
wget https://raw.githubusercontent.com/BESCLLC/chain-info/main/config.toml


⚙️ 6. Start the Node

besu --config-file=config.toml


🔌 7. RPC Endpoints

Once running:
	•	HTTP RPC → http://localhost:3545
	•	WebSocket → ws://localhost:3546


🧪 8. Test Your RPC

curl -X POST http://127.0.0.1:3545 \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","method":"eth_blockNumber","params":[],"id":1}'

✅ You should receive a hex block number.


🔁 9. Run as a Service (Optional)

sudo nano /etc/systemd/system/besu.service

Paste:

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

Enable + start:

sudo systemctl daemon-reload
sudo systemctl enable besu
sudo systemctl start besu


📊 10. Check Logs

journalctl -u besu -f


⚠️ Troubleshooting

❌ 502 Bad Gateway

Your reverse proxy (nginx) is pointing to the wrong port
→ should be 3545

❌ Port already in use

ss -tulnp | grep 3545


❌ Invalid genesis file

cat genesis.json | jq .


🧠 Notes
	•	Do NOT modify genesis.json
	•	All nodes must use the exact same genesis
	•	Ports are set in config.toml (3545 / 3546 by default)
