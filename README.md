## Install Besu

### Linux

```bash
wget https://hyperledger.jfrog.io/artifactory/besu-binaries/besu/23.7.3/besu-23.7.3.tar.gz
tar -xvf besu-23.7.3.tar.gz
sudo ln -s $(pwd)/besu-23.7.3/bin/besu /usr/local/bin/besu
```

---

### macOS

```bash
brew install hyperledger/besu/besu
```

---

### Install Java

#### Linux
```bash
sudo apt update
sudo apt install openjdk-17-jdk
```

#### macOS
```bash
brew install openjdk@21
```

---

### Verify

```bash
besu --version
```

---

## Download Chain Configuration

After installing Besu, download the required network files:

```bash
wget https://raw.githubusercontent.com/BESCLLC/chain-info/main/genesis.json
wget https://raw.githubusercontent.com/BESCLLC/chain-info/main/config.toml
