# zhcash-core
Official ZHCASH node software
### Dockerfile
FROM ubuntu:20.04

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && apt-get install -y \
    build-essential \
    curl \
    git \
    cmake \
    pkg-config \
    libssl-dev \
    libboost-all-dev \
    libzmq3-dev \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY . .

RUN make -j$(nproc)

CMD ["./zhcd"]


### install.sh
#!/bin/bash

set -e

echo "Installing ZHCASH node dependencies..."
sudo apt update
sudo apt install -y build-essential curl git cmake pkg-config libssl-dev libboost-all-dev libzmq3-dev

echo "Cloning ZHCASH repository..."
git clone https://github.com/ZHCASH-Development/zhcash-core.git
cd zhcash-core

echo "Building node..."
make -j$(nproc)

echo "ZHCASH node installed successfully. Run ./zhcd to start."


### build-from-source.md
# Build ZHCASH Node from Source

This guide explains how to build and run a ZHCASH full node from source.

## Requirements
- Ubuntu 20.04+
- 2+ GHz CPU / 4+ cores
- 8GB+ RAM
- 100GB SSD

## Steps
```bash
sudo apt update && sudo apt install -y \
    build-essential curl git cmake pkg-config \
    libssl-dev libboost-all-dev libzmq3-dev

git clone https://github.com/ZHCASH-Development/zhcash-core.git
cd zhcash-core
make -j$(nproc)
```

## Run node
```bash
./zhcd
```

---

### .gitignore
/build/
/bin/
*.log
*.tmp
*.swp
*.o
zhcd
node_modules/
.env
.cache


### README.md
# ZHCASH Core

Official source code and build instructions for the ZHCASH full node (`zhcd`).

## Build from source
See [`build-from-source.md`](./build-from-source.md)

## Docker
```bash
docker build -t zhc-node .
docker run -it --rm zhc-node
```

## License
GPL-3.0 License
