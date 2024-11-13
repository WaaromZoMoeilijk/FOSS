# Awesome Self-Hosted Open Source Software (Version 0.3)

A curated list of valuable open-source software that can be self-hosted using Docker Compose. This repository provides categories, descriptions, links, and examples to help you get started.

## Table of Contents

- [Applications](#applications)
  - [Amnezia VPN](#amnezia-vpn)
  - [Nextcloud All-in-One](#nextcloud-all-in-one)
  - [BTCPay Server](#btcpay-server)
  - [Semaphore (Ansible GUI)](#semaphore-ansible-gui)
  - [Organizr](#organizr)
  - [Uptime Kuma](#uptime-kuma)
  - [GitLab](#gitlab)
  - [Nginx Proxy Manager](#nginx-proxy-manager)
  - [Home Assistant](#home-assistant)
  - [Invoice Ninja](#invoice-ninja)
  - [AdGuard Home](#adguard-home)
  - [Vaultwarden](#vaultwarden)
  - [WireGuard UI](#wireguard-ui)
  - [Headscale](#headscale)
  - [Simple URL Shortener](#simple-url-shortener)
  - [Jitsi Meet](#jitsi-meet)
  - [Matrix Server (Synapse) and Element Client](#matrix-server-synapse-and-element-client)
  - [Keycloak](#keycloak)
  - [Coolify](#coolify)
  - [n8n](#n8n)
- [Usenet and P2P](#usenet-and-p2p)
  - [SABnzbd](#sabnzbd)
  - [Radarr](#radarr)
  - [Sonarr](#sonarr)
  - [Bazarr](#bazarr)
  - [Prowlarr](#prowlarr)
  - [Lidarr](#lidarr)
  - [Readarr](#readarr)
  - [Overseerr](#overseerr)
  - [Transmission](#transmission)
- [Tools](#tools)
  - [Ansible](#ansible)
  - [Docker & Docker Compose](#docker--docker-compose)
  - [WireGuard](#wireguard)
- [Additional Resources](#additional-resources)

---

## Applications

### Amnezia VPN

**Description:** Amnezia VPN is an open-source VPN client and server solution that simplifies the process of setting up personal VPN servers. It supports multiple VPN protocols, including OpenVPN and WireGuard, providing secure and private internet access. Amnezia VPN allows you to deploy a VPN server on your own hardware or cloud instance, ensuring full control over your data.

**Link:** [Amnezia VPN](https://amnezia.org/)

**Note:** Amnezia VPN currently does not provide an official Docker image. For Docker-based VPN solutions, consider alternatives like [OpenVPN](https://github.com/kylemanna/docker-openvpn) or [WireGuard](https://www.wireguard.com/).

---

### Nextcloud All-in-One

**Description:** Nextcloud All-in-One provides a simple way to install a Nextcloud instance along with all official Nextcloud apps in a single Docker container. It includes features like file sharing, collaborative document editing, calendar, contacts, and more. Nextcloud ensures data privacy by allowing you to host your own data.

**Link:** [Nextcloud All-in-One](https://github.com/nextcloud/all-in-one)

**Docker Compose Example:**

```yaml
version: '3'

services:
  nextcloud:
    image: nextcloud/all-in-one:latest
    restart: always
    container_name: nextcloud
    volumes:
      - nextcloud_aio_mastercontainer:/mnt/docker-aio-config
    ports:
      - 8080:8080

volumes:
  nextcloud_aio_mastercontainer:
    name: nextcloud_aio_mastercontainer
```

**Usage:**

After starting the container, access Nextcloud via `http://localhost:8080` and follow the on-screen instructions to complete the setup.

---

### BTCPay Server

**Description:** BTCPay Server is a secure, self-hosted, open-source cryptocurrency payment processor that allows merchants to accept Bitcoin and other cryptocurrencies without intermediaries. It supports various integrations, invoicing, and payment tracking features, ensuring full control over your financial transactions.

**Link:** [BTCPay Server](https://btcpayserver.org/)

**Docker Compose Example:**

BTCPay Server recommends using their deployment script for a complete setup. Here's a simplified example:

```yaml
version: '3'

services:
  btcpayserver:
    image: btcpayserver/btcpayserver:latest
    restart: always
    environment:
      BTCPAY_HOST: 'btcpay.yourdomain.com'
      NBITCOIN_NETWORK: 'mainnet'
      BTCPAYGEN_CRYPTO1: 'btc'
      LIGHTNING_ALIAS: 'BTCPayServer'
    volumes:
      - ./btcpay_data:/datadir
    ports:
      - '49392:80'
      - '49393:443'
```

**Note:** For production environments, it's recommended to follow the official [BTCPay Server Docker Deployment](https://docs.btcpayserver.org/Deployment/Docker/) guide.

---

### Semaphore (Ansible GUI)

**Description:** Semaphore is an open-source web-based user interface for Ansible. It simplifies the management of Ansible playbooks, inventories, and tasks. Semaphore enhances team collaboration by providing role-based access control, logging, and a user-friendly interface for automation tasks.

**Link:** [Semaphore](https://ansible-semaphore.com/)

**Docker Compose Example:**

```yaml
version: '3'

services:
  semaphore:
    image: ansiblesemaphore/semaphore:latest
    container_name: semaphore
    ports:
      - '3000:3000'
    environment:
      SEMAPHORE_DB_DIALECT: 'sqlite3'
      SEMAPHORE_DB: '/data/semaphore.db'
      SEMAPHORE_PLAYBOOK_PATH: '/tmp'
    volumes:
      - './data:/data'
      - './playbooks:/tmp'
    restart: always
```

**Usage:**

Access the Semaphore UI at `http://localhost:3000`. The initial setup wizard will prompt you to create an admin user.

---

### Organizr

**Description:** Organizr is a self-hosted application that serves as a unified frontend for all your web applications. It allows you to organize your self-hosted services into a single, easy-to-use dashboard with customizable tabs and user authentication.

**Link:** [Organizr](https://github.com/causefx/Organizr)

**Docker Compose Example:**

```yaml
version: '3'

services:
  organizr:
    image: lscr.io/linuxserver/organizr:latest
    container_name: organizr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Your_Timezone
    volumes:
      - './config:/config'
    ports:
      - '80:80'
    restart: unless-stopped
```

**Usage:**

Navigate to `http://localhost` to access Organizr and start configuring your dashboard.

---

### Uptime Kuma

**Description:** Uptime Kuma is a self-hosted monitoring tool that provides real-time status and notifications for your websites and applications. It features a sleek dashboard, multiple notification methods, and supports various monitoring protocols like HTTP(s), TCP, Ping, and DNS.

**Link:** [Uptime Kuma](https://github.com/louislam/uptime-kuma)

**Docker Compose Example:**

```yaml
version: '3'

services:
  uptime-kuma:
    image: louislam/uptime-kuma:1
    container_name: uptime-kuma
    volumes:
      - './data:/app/data'
    ports:
      - '3001:3001'
    restart: unless-stopped
```

**Usage:**

Access Uptime Kuma at `http://localhost:3001` and begin setting up your monitors.

---

### GitLab

**Description:** GitLab is an all-in-one DevOps platform that provides Git repository management, code reviews, issue tracking, CI/CD pipelines, and more. Self-hosting GitLab gives you complete control over your codebase and development workflows.

**Link:** [GitLab](https://about.gitlab.com/)

**Docker Compose Example:**

```yaml
version: '3'

services:
  gitlab:
    image: gitlab/gitlab-ce:latest
    restart: always
    hostname: 'gitlab.example.com'
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url 'http://gitlab.example.com'
    ports:
      - '80:80'
      - '443:443'
      - '22:22'
    volumes:
      - './config:/etc/gitlab'
      - './logs:/var/log/gitlab'
      - './data:/var/opt/gitlab'
```

**Usage:**

After starting the container, GitLab will be accessible at `http://gitlab.example.com`. Remember to update DNS records or `/etc/hosts` as necessary.

---

### Nginx Proxy Manager

**Description:** Nginx Proxy Manager is a user-friendly interface for managing Nginx proxy hosts. It simplifies setting up SSL certificates, reverse proxies, and redirections, making it easier to manage multiple web services on the same server.

**Link:** [Nginx Proxy Manager](https://nginxproxymanager.com/)

**Docker Compose Example:**

```yaml
version: '3'

services:
  app:
    image: jc21/nginx-proxy-manager:latest
    restart: unless-stopped
    ports:
      - '80:80'
      - '81:81'   # Admin interface
      - '443:443'
    environment:
      - DB_SQLITE_FILE=/data/database.sqlite
    volumes:
      - './data:/data'
      - './letsencrypt:/etc/letsencrypt'
```

**Usage:**

Access the admin interface at `http://localhost:81`. Default credentials are `admin@example.com` / `changeme`.

---

### Home Assistant

**Description:** Home Assistant is an open-source platform for home automation that puts local control and privacy first. It supports a wide range of devices and services, allowing you to automate and control your smart home from a single interface.

**Link:** [Home Assistant](https://www.home-assistant.io/)

**Docker Compose Example:**

```yaml
version: '3'

services:
  homeassistant:
    image: ghcr.io/home-assistant/home-assistant:stable
    container_name: homeassistant
    volumes:
      - './config:/config'
      - '/etc/localtime:/etc/localtime:ro'
    environment:
      - TZ=Your_Timezone
    restart: unless-stopped
    network_mode: host
```

**Usage:**

Home Assistant uses host networking to discover devices on your network. Access the UI at `http://localhost:8123`.

---

### Invoice Ninja

**Description:** Invoice Ninja is a comprehensive platform for invoicing, billing, payments, and client management. It offers features like customizable invoices, recurring billing, and supports multiple payment gateways.

**Link:** [Invoice Ninja](https://www.invoiceninja.com/)

**Docker Compose Example:**

```yaml
version: '3'

services:
  server:
    image: invoiceninja/invoiceninja:latest
    container_name: invoiceninja
    volumes:
      - './storage:/var/www/app/storage'
    environment:
      - APP_URL=http://yourdomain.com
      - APP_KEY=base64:your_app_key
      - MULTI_DB_ENABLED=false
    depends_on:
      - db
    restart: unless-stopped
    ports:
      - '8000:80'

  db:
    image: mysql:5
    container_name: db
    environment:
      - MYSQL_ROOT_PASSWORD=ninja
      - MYSQL_DATABASE=ninja
      - MYSQL_USER=ninja
      - MYSQL_PASSWORD=ninja
    volumes:
      - './mysql:/var/lib/mysql'
    restart: unless-stopped
```

**Usage:**

Access Invoice Ninja at `http://localhost:8000` and complete the setup using the provided database credentials.

---

### AdGuard Home

**Description:** AdGuard Home is a network-wide software for blocking ads and trackers. It functions as a DNS server that filters out unwanted content, providing privacy protection and improved browsing speeds for all devices on your network.

**Link:** [AdGuard Home](https://github.com/AdguardTeam/AdGuardHome)

**Docker Compose Example:**

```yaml
version: '3'

services:
  adguardhome:
    image: adguard/adguardhome:latest
    container_name: adguardhome
    volumes:
      - './work:/opt/adguardhome/work'
      - './conf:/opt/adguardhome/conf'
    ports:
      - '53:53/tcp'
      - '53:53/udp'
      - '67:67/udp'  # DHCP (optional)
      - '68:68/udp'  # DHCP (optional)
      - '80:80/tcp'
      - '443:443/tcp'
      - '3000:3000/tcp'  # Admin interface
    restart: unless-stopped
```

**Usage:**

Access the admin interface at `http://localhost:3000` to configure AdGuard Home.

---

### Vaultwarden

**Description:** Vaultwarden (formerly Bitwarden_rs) is an unofficial, lightweight, and efficient implementation of the Bitwarden server API, written in Rust. It allows you to self-host your own password manager, providing secure storage and synchronization of passwords, notes, and other sensitive data.

**Link:** [Vaultwarden](https://github.com/dani-garcia/vaultwarden)

**Docker Compose Example:**

```yaml
version: '3'

services:
  vaultwarden:
    image: vaultwarden/server:latest
    container_name: vaultwarden
    volumes:
      - './vw-data:/data'
    environment:
      - WEBSOCKET_ENABLED=true  # Enable WebSocket notifications
      - SIGNUPS_ALLOWED=false   # Set to true to allow new signups
      - ADMIN_TOKEN=your_admin_token
    ports:
      - '80:80'
    restart: unless-stopped
```

**Usage:**

Access Vaultwarden at `http://localhost` and use the Bitwarden clients to connect to your server.

---

### WireGuard UI

**Description:** WireGuard UI is a web user interface for the WireGuard VPN server, designed to simplify the management of WireGuard configurations. It provides an easy-to-use interface to create, manage, and revoke client configurations.

**Link:** [WireGuard UI](https://github.com/ngoduykhanh/wireguard-ui)

**Docker Compose Example:**

```yaml
version: '3.8'

services:
  wireguard-ui:
    image: ngoduykhanh/wireguard-ui:latest
    container_name: wireguard-ui
    volumes:
      - './config:/config'
    ports:
      - '5000:5000'
      - '51820:51820/udp'  # WireGuard port
    environment:
      - WIREGUARD_UI_ADDRESS=0.0.0.0
      - WIREGUARD_UI_PORT=5000
      - WIREGUARD_UI_CONFIG=/config/wg0.conf
    cap_add:
      - NET_ADMIN
    restart: unless-stopped
```

**Usage:**

Access the UI at `http://localhost:5000` to manage your WireGuard server and clients.

---

### Headscale

**Description:** Headscale is an open-source, self-hosted implementation of the Tailscale coordination server. It allows you to create your own private mesh VPN network using the Tailscale client without relying on Tailscale's proprietary servers.

**Link:** [Headscale](https://github.com/juanfont/headscale)

**Docker Compose Example:**

```yaml
version: '3'

services:
  headscale:
    image: headscale/headscale:latest
    container_name: headscale
    volumes:
      - './config:/etc/headscale'
      - './data:/var/lib/headscale'
    environment:
      - HEADSCALE_SERVER_URL=http://headscale:8080
      - HEADSCALE_IPV4_PREFIX=100.64.0.0/10
      - HEADSCALE_DB_TYPE=sqlite3
      - HEADSCALE_DB_PATH=/var/lib/headscale/db.sqlite
    ports:
      - '8080:8080'
    restart: unless-stopped
```

**Usage:**

Configure your Tailscale clients to use your Headscale server by setting the `--login-server` parameter.

---

### Simple URL Shortener

**Description:** Simple-URL-Shortener is a lightweight and straightforward URL shortening service that you can self-host. It provides a minimalist interface to create short URLs, with features like QR code generation and basic statistics.

**Link:** [Simple-URL-Shortener](https://github.com/azlux/Simple-URL-Shortener/)

**Docker Compose Example:**

```yaml
version: '3'

services:
  urlshortener:
    image: azlux/surl:latest
    container_name: simple-url-shortener
    ports:
      - '8000:80'
    volumes:
      - './data:/var/www/data'
    environment:
      - SURL_BASE=https://yourdomain.com
      - SURL_ADMIN=user:password
    restart: unless-stopped
```

**Usage:**

- Access the application at `http://localhost:8000`.
- To access the admin interface, navigate to `http://localhost:8000/admin` and use the credentials set in `SURL_ADMIN`.

---

### Jitsi Meet

**Description:** Jitsi Meet is a free, open-source video conferencing solution that allows you to host secure and high-quality video meetings. It supports features like screen sharing, recording, live streaming, and integrates with various calendar services.

**Link:** [Jitsi Meet](https://jitsi.org/jitsi-meet/)

**Docker Compose Example:**

Due to the complexity of Jitsi's architecture, it's recommended to use the official Docker setup:

- **Repository:** [jitsi/docker-jitsi-meet](https://github.com/jitsi/docker-jitsi-meet)

**Usage:**

Clone the repository and follow the instructions in the README to set up your `.env` file and start the services.

---

### Matrix Server (Synapse) and Element Client

**Description:** Matrix is an open network for secure, decentralized communication. Synapse is a Matrix homeserver implementation, and Element is a feature-rich client for Matrix, enabling secure messaging, VoIP, and integrations with other networks.

**Links:**

- [Matrix](https://matrix.org/)
- [Synapse](https://github.com/matrix-org/synapse)
- [Element](https://element.io/)

**Docker Compose Example:**

```yaml
version: '3'

services:
  synapse:
    image: matrixdotorg/synapse:latest
    container_name: synapse
    volumes:
      - './data:/data'
    ports:
      - '8008:8008'
    environment:
      - SYNAPSE_SERVER_NAME=your.domain.com
      - SYNAPSE_REPORT_STATS=yes
    restart: unless-stopped

  element:
    image: vectorim/element-web:latest
    container_name: element
    volumes:
      - './element-config:/app/config'
    ports:
      - '8080:80'
    restart: unless-stopped
```

**Usage:**

- Access Synapse at `http://localhost:8008`.
- Access Element at `http://localhost:8080`.

Configure Element to connect to your Synapse server.

---

### Keycloak

**Description:** Keycloak is an open-source Identity and Access Management solution aimed at modern applications and services. It offers features like single sign-on (SSO), social login, multifactor authentication, user federation, and user management.

**Link:** [Keycloak](https://www.keycloak.org/)

**Docker Compose Example:**

```yaml
version: '3'

services:
  keycloak:
    image: quay.io/keycloak/keycloak:latest
    container_name: keycloak
    command: start-dev
    environment:
      - KEYCLOAK_ADMIN=admin
      - KEYCLOAK_ADMIN_PASSWORD=admin_password
    ports:
      - '8080:8080'
    restart: unless-stopped
```

**Usage:**

Access Keycloak at `http://localhost:8080` and log in with the admin credentials.

---

### Coolify

**Description:** Coolify is an open-source, self-hostable alternative to Heroku and Netlify. It allows you to deploy applications, databases, and services with a simple UI or API, supporting multiple programming languages and frameworks.

**Link:** [Coolify](https://coolify.io/)

**Docker Compose Example:**

```yaml
version: '3.3'

services:
  coolify:
    image: coollabsio/coolify:latest
    container_name: coolify
    ports:
      - '3000:3000'
    volumes:
      - './data:/app/data'
    environment:
      - COOLIFY_SECRET_KEY=your_secret_key
    restart: unless-stopped
```

**Usage:**

Access Coolify at `http://localhost:3000` and start deploying your applications.

---

### n8n

**Description:** n8n is a free and open-source workflow automation tool. It enables you to connect different services together with custom logic, similar to platforms like Zapier or IFTTT, but self-hosted and more flexible.

**Link:** [n8n](https://n8n.io/)

**Docker Compose Example:**

```yaml
version: '3'

services:
  n8n:
    image: n8nio/n8n:latest
    container_name: n8n
    ports:
      - '5678:5678'
    volumes:
      - './n8n_data:/home/node/.n8n'
    environment:
      - N8N_BASIC_AUTH_ACTIVE=true
      - N8N_BASIC_AUTH_USER=your_username
      - N8N_BASIC_AUTH_PASSWORD=your_password
      - N8N_HOST=localhost
      - N8N_PORT=5678
      - WEBHOOK_TUNNEL_URL=http://localhost:5678
    restart: unless-stopped
```

**Usage:**

Access n8n at `http://localhost:5678` and start creating your workflows.

---

## Usenet and P2P

### SABnzbd

**Description:** SABnzbd is a free and open-source binary newsreader written in Python, designed to automate the downloading of files from Usenet. It offers a web-based interface, supports custom scripts, RSS feeds, and download scheduling.

**Link:** [SABnzbd](https://sabnzbd.org/)

**Docker Compose Example:**

```yaml
version: '3'

services:
  sabnzbd:
    image: lscr.io/linuxserver/sabnzbd:latest
    container_name: sabnzbd
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Your_Timezone
    volumes:
      - './config:/config'
      - './downloads:/downloads'
    ports:
      - '8080:8080'
      - '9090:9090'
    restart: unless-stopped
```

**Usage:**

Access the web interface at `http://localhost:8080` to configure your Usenet settings.

---

### Radarr

**Description:** Radarr is a movie collection manager for Usenet and BitTorrent users. It can monitor multiple RSS feeds for new releases and will automatically download, sort, and manage movies according to your preferences.

**Link:** [Radarr](https://radarr.video/)

**Docker Compose Example:**

```yaml
version: '3'

services:
  radarr:
    image: lscr.io/linuxserver/radarr:latest
    container_name: radarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Your_Timezone
    volumes:
      - './config:/config'
      - './movies:/movies'
      - './downloads:/downloads'
    ports:
      - '7878:7878'
    restart: unless-stopped
```

**Usage:**

Access Radarr at `http://localhost:7878` and configure your movie library.

---

### Sonarr

**Description:** Sonarr is a PVR for Usenet and BitTorrent users that automates the downloading, organizing, and management of TV series. It supports episode monitoring, quality management, and can integrate with various download clients and indexers.

**Link:** [Sonarr](https://sonarr.tv/)

**Docker Compose Example:**

```yaml
version: '3'

services:
  sonarr:
    image: lscr.io/linuxserver/sonarr:latest
    container_name: sonarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Your_Timezone
    volumes:
      - './config:/config'
      - './tv:/tv'
      - './downloads:/downloads'
    ports:
      - '8989:8989'
    restart: unless-stopped
```

**Usage:**

Access Sonarr at `http://localhost:8989` to set up your TV series tracking.

---

### Bazarr

**Description:** Bazarr is a companion application to Sonarr and Radarr that manages and downloads subtitles for movies and TV shows. It integrates seamlessly with your existing setup to ensure your media library always has the correct subtitles.

**Link:** [Bazarr](https://www.bazarr.media/)

**Docker Compose Example:**

```yaml
version: '3'

services:
  bazarr:
    image: lscr.io/linuxserver/bazarr:latest
    container_name: bazarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Your_Timezone
    volumes:
      - './config:/config'
      - './tv:/tv'
      - './movies:/movies'
    ports:
      - '6767:6767'
    restart: unless-stopped
```

**Usage:**

Access Bazarr at `http://localhost:6767` and configure subtitle providers and settings.

---

### Prowlarr

**Description:** Prowlarr is an indexer manager/proxy for Sonarr, Radarr, Lidarr, and Readarr. It integrates with all *arr applications to provide a unified interface for adding and managing indexers.

**Link:** [Prowlarr](https://wiki.servarr.com/prowlarr)

**Docker Compose Example:**

```yaml
version: '3'

services:
  prowlarr:
    image: lscr.io/linuxserver/prowlarr:develop
    container_name: prowlarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Your_Timezone
    volumes:
      - './config:/config'
    ports:
      - '9696:9696'
    restart: unless-stopped
```

**Usage:**

Access Prowlarr at `http://localhost:9696` and add your indexers.

---

### Lidarr

**Description:** Lidarr is a music collection manager for Usenet and BitTorrent users. It can monitor multiple RSS feeds for new album releases and will automatically download, organize, and manage music libraries.

**Link:** [Lidarr](https://lidarr.audio/)

**Docker Compose Example:**

```yaml
version: '3'

services:
  lidarr:
    image: lscr.io/linuxserver/lidarr:latest
    container_name: lidarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Your_Timezone
    volumes:
      - './config:/config'
      - './music:/music'
      - './downloads:/downloads'
    ports:
      - '8686:8686'
    restart: unless-stopped
```

**Usage:**

Access Lidarr at `http://localhost:8686` and configure your music library.

---

### Readarr

**Description:** Readarr is a book collection manager for Usenet and BitTorrent users. It automates the process of finding, downloading, and organizing eBooks and audiobooks.

**Link:** [Readarr](https://readarr.com/)

**Docker Compose Example:**

```yaml
version: '3'

services:
  readarr:
    image: lscr.io/linuxserver/readarr:develop
    container_name: readarr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Your_Timezone
    volumes:
      - './config:/config'
      - './books:/books'
      - './downloads:/downloads'
    ports:
      - '8787:8787'
    restart: unless-stopped
```

**Usage:**

Access Readarr at `http://localhost:8787` to manage your book collection.

---

### Overseerr

**Description:** Overseerr is a request management and media discovery tool for your media library. It integrates with services like Sonarr and Radarr, allowing users to request new content and administrators to approve and track requests.

**Link:** [Overseerr](https://overseerr.dev/)

**Docker Compose Example:**

```yaml
version: '3'

services:
  overseerr:
    image: lscr.io/linuxserver/overseerr:latest
    container_name: overseerr
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Your_Timezone
    volumes:
      - './config:/app/config'
    ports:
      - '5055:5055'
    restart: unless-stopped
```

**Usage:**

Access Overseerr at `http://localhost:5055` to set up user accounts and connect to your media services.

---

### Transmission

**Description:** Transmission is a fast, easy, and free BitTorrent client with a focus on simplicity and minimal resource usage. It supports features like encryption, peer exchange, magnet links, and webseed support.

**Link:** [Transmission](https://transmissionbt.com/)

**Docker Compose Example:**

```yaml
version: '3'

services:
  transmission:
    image: lscr.io/linuxserver/transmission:latest
    container_name: transmission
    environment:
      - PUID=1000
      - PGID=1000
      - TZ=Your_Timezone
      - USER=username
      - PASS=password
    volumes:
      - './config:/config'
      - './downloads:/downloads'
      - './watch:/watch'
    ports:
      - '9091:9091'
      - '51413:51413'
      - '51413:51413/udp'
    restart: unless-stopped
```

**Usage:**

Access the web interface at `http://localhost:9091` to manage your torrents.

---

## Tools

### Ansible

**Description:** Ansible is an open-source automation tool used for software provisioning, configuration management, and application deployment. It uses simple YAML syntax called playbooks and operates over SSH, eliminating the need for agents on remote systems.

**Link:** [Ansible](https://www.ansible.com/)

**Installation:**

```bash
# On Ubuntu
sudo apt update
sudo apt install ansible
```

**Example Playbook (site.yml):**

```yaml
---
- name: Configure web servers
  hosts: webservers
  become: true

  tasks:
    - name: Ensure Apache is installed
      apt:
        name: apache2
        state: present

    - name: Copy index.html
      copy:
        src: files/index.html
        dest: /var/www/html/index.html
```

---

### Docker & Docker Compose

**Description:** Docker is a platform for building, deploying, and managing containerized applications. Docker Compose is a tool that allows you to define and manage multi-container Docker applications using a YAML file.

**Links:**

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)

**Installation:**

```bash
# Install Docker 
curl https://get.docker.com -o /tmp/docker.sh
nano /tmp/docker.sh
bash /tmp/docker.sh
```

---

### WireGuard

**Description:** WireGuard is a modern, high-performance VPN protocol that utilizes state-of-the-art cryptography. It's designed to be faster, simpler, and more secure than traditional VPN protocols.

**Link:** [WireGuard](https://www.wireguard.com/)

**Installation:**

```bash
# On Ubuntu
sudo apt update
sudo apt install wireguard
```

**Example Configuration (`/etc/wireguard/wg0.conf`):**

```ini
[Interface]
PrivateKey = <server_private_key>
Address = 10.0.0.1/24
ListenPort = 51820

[Peer]
PublicKey = <client_public_key>
AllowedIPs = 10.0.0.2/32
```

**Usage:**

Start the WireGuard interface:

```bash
sudo wg-quick up wg0
```

---

## Additional Resources

- **Awesome Self-Hosted:** A list of Free Software network services and web applications which can be hosted on your own servers. It covers a wide range of categories and is a great resource for finding new self-hosted solutions.

  **Link:** [awesome-selfhosted/awesome-selfhosted](https://github.com/awesome-selfhosted/awesome-selfhosted)

- **Ansible-NAS:** A comprehensive Ansible playbook for configuring a home network attached storage (NAS) server. It automates the setup of various services like media servers, file sharing, and backup solutions.

  **Link:** [DaveStephens/ansible-nas](https://github.com/DaveStephens/ansible-nas)

---

This document provides a starting point for setting up and deploying various open-source applications using Docker Compose. For detailed configurations, security considerations, and advanced setups, please refer to the official documentation of each application.
