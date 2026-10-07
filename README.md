# Home Lab

Docker-based home lab using Docker Compose, Caddy, dnsmasq, Vaultwarden, Portainer and Immich.

## Requirements

- Linux
- Docker + Docker Compose
- A DuckDNS domain
- A DuckDNS API token

## Configuration

Copy the environment template:

```bash
cp example.env .env
````

Edit `.env` with your DuckDNS details:

```env
DOMAIN="example.duckdns.org"
URL="https://example.duckdns.org"
DUCKDNS_API_TOKEN=00000000-0000-0000-0000-000000000000
```

Replace the example values with your own.


### dnsmasq

Copy the template:

```bash
cp infrastructure/dnsmasq/dnsmasq.conf.template \
   infrastructure/dnsmasq/dnsmasq.conf
```

Edit `dnsmasq.conf` and configure:

* LAN interface
* DuckDNS domain
* Homelab server IP
* Router/gateway IP
* DHCP range, if required

Example:

```conf
interface=YOUR_LAN_INTERFACE
address=/.example.duckdns.org/YOUR_SERVER_IP
server=YOUR_ROUTER_IP
```

Find your network configuration with:

```bash
ip -br link
ip addr
ip route
```

### Immich

Immich uses a separate Compose file:

```bash
cd services/immich
cp .env.example .env
docker compose up -d
```

## Start

Start the main services:

```bash
docker compose up -d
```

Check the status:

```bash
docker compose ps
```
