## 👋 Welcome to Smokeping 🚀

Network latency monitoring and graphing tool

## 📋 Description

Smokeping is a network latency monitoring and graphing tool. It pings a set of
targets on a schedule, records the round trip time of each probe, and renders
the results as latency graphs and loss history. This stack runs the linuxserver
Smokeping image behind the host nginx proxy, with its configuration and RRD
data kept on bind mounts.

Targets and their ping intervals are defined in the Smokeping config, which
lives on the config volume, not in the compose environment. The variables
below only cover how the container itself is set up.

## 🚀 Services

- **app**: lscr.io/linuxserver/smokeping:latest

## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/smokeping/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/smokeping" ~/.local/srv/docker/smokeping
cd ~/.local/srv/docker/smokeping
cp default.env .env
docker compose --env-file .env up -d
```

### Option 3: Using composemgr
```bash
composemgr install smokeping
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
SERVICE_USER=1000
SERVICE_GROUP=1000
```

See `docker-compose.yaml` for complete list of configurable options.

### Environment Files

`default.env.sample` holds the full set of variables and is copied to `.env`
before starting the stack:

```bash
cp default.env .env
docker compose --env-file .env up -d
```

`app.env.sample` holds the app-specific overrides and is copied to `app.env`:

```bash
cp app.env.sample app.env
```

`composemgr up` applies `app.env` and `default.env` automatically. Raw
`docker compose` commands need `--env-file .env` to pick up the same values.

### Reverse Proxy

Three standalone compose files ship in this repo:

| File | Use |
|------|-----|
| `docker-compose.yaml` | Default, published on `172.17.0.1:64345` |
| `docker-compose.traefik.yaml` | Behind an existing external `traefik` network |
| `docker-compose.tunnel.yaml` | Behind an existing external `cloudflare` tunnel network |

```bash
docker compose -f docker-compose.traefik.yaml --env-file .env up -d
```

## 🌐 Access

- **Web Interface**: http://172.17.0.1:64345

## 📂 Volumes

- `./volumes/config/smokeping` - Smokeping configuration, generated on first start
- `./volumes/data/smokeping` - RRD round trip time and probe history

## 🔐 Security

- Set `SERVICE_USER` and `SERVICE_GROUP` to the host user that should own the
  volumes, otherwise the container writes them as root
- Use HTTPS via the reverse proxy in production, the web UI is unauthenticated
  by default and shows your full network topology
- The container is published only on the dockerhost address `172.17.0.1`, it is
  not reachable from other hosts
- Regularly update Docker images for security patches
- Backup your data regularly

## 🔍 Logging

```shell
docker compose --env-file .env logs -f app
```

## 🛠️ Management

```bash
# Start services
docker compose --env-file .env up -d

# Stop services
docker compose --env-file .env down

# Update to latest images
docker compose --env-file .env pull && docker compose --env-file .env up -d

# View logs
docker compose --env-file .env logs -f

# Restart services
docker compose --env-file .env restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
