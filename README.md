## 👋 Welcome to smokeping 🚀

Network latency monitoring and graphing tool

## 📋 Description

Network latency monitoring and graphing tool

## 🚀 Services

- **smokeping**: linuxserver/smokeping:latest

## 📦 Installation

### Option 1: Quick Install
```bash
curl -q -LSsf "https://raw.githubusercontent.com/composemgr/smokeping/main/docker-compose.yaml" -o compose.yml
```

### Option 2: Git Clone
```bash
git clone "https://github.com/composemgr/smokeping" ~/.local/srv/docker/smokeping
cd ~/.local/srv/docker/smokeping
docker compose up -d
```

### Option 3: Using composemgr
```bash
composemgr install smokeping
```

## 🔧 Configuration

### Environment Variables

```shell
TZ=America/New_York
```

See `docker-compose.yaml` for complete list of configurable options.

## 🌐 Access

- **Web Interface**: http://172.17.0.1:8100

## 📂 Volumes

- `./volumes/config/smokeping` - Data storage
- `./volumes/data/smokeping` - Data storage

## 🔍 Logging

```shell
docker compose logs -f smokeping
```

## 🛠️ Management

```bash
# Start services
docker compose up -d

# Stop services
docker compose down

# Update to latest images
docker compose pull && docker compose up -d

# View logs
docker compose logs -f

# Restart services
docker compose restart
```

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose V2+

## 🤝 Author

🤖 casjay: [Github](https://github.com/casjay) 🤖  
🦄 composemgr: [Github](https://github.com/composemgr) 🦄
