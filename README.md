# Docknode ATOM

## Endpoints

- Fullnode: `https://mydomain.com`
- Node exporter: `https://mydomain.com:9100/metrics`

## Install

0. VPS config (optional)

```bash
apt update
apt upgrade
apt install git

# Or all in one command
apt update && apt upgrade -y && apt install -y git

# install docker https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository
```

1. Clone the repository and

```bash
git clone https://github.com/olivbau/docknode-atom.git
cd docknode-atom
```

2. Configure environement variables

```bash
cp .env.example .env

# Generate users passwords for basic auth
docker run --rm caddy:2-alpine caddy hash-password --plaintext 'password'

# Set users and passwords for basic auth
# Set the host
nano .env
```

3. Setup UFW

```bash
ufw allow ssh
ufw deny 1317
ufw deny 26657
ufw deny 9090
ufw enable
```

4. Run

```bash
wget -O ./gaia/genesis.json.gz https://raw.githubusercontent.com/cosmos/mainnet/master/genesis/genesis.cosmoshub-4.json.gz
gzip -d ./gaia/genesis.json.gz
docker compose pull --ignore-pull-failures
docker compose up -d
docker logs -f docknode-atom-gaiad-1 --since 5m
docker compose down
```
