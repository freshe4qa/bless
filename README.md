<p align="center">
  <img height="100" height="auto" src="https://github.com/user-attachments/assets/18a5130f-4b45-4606-a9d6-d26c2f07c3b8">
</p>

# Bless - Testnet

Official documentation:
>- [Guide](https://docs.bless.network/welcome)

Explorer:
>- [Explorer](https://bless.network/dashboard)

### Minimum Hardware Requirements
 - 3x CPUs; the faster clock speed the better
 - 4GB RAM
 - 100GB of storage (SSD or NVME)
 - Ubuntu 22.04

Установка ноды:

```
sudo apt update && sudo apt upgrade -y
```

```
sudo apt install curl iptables build-essential git wget lz4 jq make gcc nano automake autoconf tmux htop nvme-cli pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev git-all protobuf-compiler screen -y
```

```
for pkg in docker.io docker-doc docker-compose podman-docker containerd runc; do sudo apt-get remove $pkg; done
```

```
sudo apt-get install ca-certificates curl gnupg
```

```
sudo install -m 0755 -d /etc/apt/keyrings
```

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
```

```
sudo chmod a+r /etc/apt/keyrings/docker.gpg
```

```
echo \
  "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
  "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

```
apt install docker.io -y
```

```
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```

```
mkdir bless
```

```
cd bless
```

```
nano .env
```

Вставляем данные значения в файл:
```
NODE_ROLE=worker
BOOT_NODES=/ip4/143.244.211.194/tcp/9010/p2p/12D3KooWGuBya7RYHTzZmR7uLJYUXffSPuBUPKnmYSfsgwyjqFuw

# (Optional) S3 Backup Configuration
AWS_ACCESS_KEY_ID=<s3_id>
AWS_SECRET_ACCESS_KEY=<s3_key>
KEY_PATH=<backup_key_path>
KEY_PASSWORD=<key_password>
```
Сохраняем CTRL + O далее Enter, выйти CTRL + X

Запускаем ноду:

```
docker run -d \
  --name blessnetwork-node \
  -p 9527:9527 \
  --env-file .env \
  -v ${PWD}/node-data:/app/keys \
  --restart unless-stopped \
  ghcr.io/blessnetwork/b7s:0.6.6.patch3
```

Посмотреть логи:

```
docker logs -f blessnetwork-node
```

Сохраняем данные ноды:

Address - /bless/node-data/identity

Public key - /bless/node-data/pubkey.txt
