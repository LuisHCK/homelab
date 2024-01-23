# Home Server with Pi-hole and Jellyfin

This repository contains a Docker Compose configuration to set up a personal home server with Pi-hole for network-wide ad blocking and Jellyfin for media streaming. This setup ensures that your network remains ad-free, and you can seamlessly access and stream your media content.

## Pi-hole

### Overview

Pi-hole is a network-wide ad blocker that acts as a DNS sinkhole. It functions by blacklisting known ad-serving domain names, preventing them from being resolved and effectively blocking ads across your entire network.

### Configuration

- **Container Name**: pihole
- **Image**: pihole/pihole:latest
- **Ports**:
  - 53/tcp: DNS server
  - 53/udp: DNS server
  - 80/tcp: Web interface
- **Environment Variables**:
  - `TZ: 'America/Managua'`: Set the timezone to America/Managua.
  - `WEBPASSWORD: '%XTWodu3j5YaTvfB'`: Web interface password for Pi-hole.
- **Volumes**:
  - `./etc-pihole:/etc/pihole`: Store Pi-hole configuration data.
  - `./etc-dnsmasq.d:/etc/dnsmasq.d`: Store additional DNS configurations.
- **Restart Policy**: unless-stopped

To access the Pi-hole web interface, navigate to http://localhost:80/admin. Log in with the specified `WEBPASSWORD`.

## Jellyfin

### Overview

Jellyfin is an open-source media server that allows you to organize, stream, and share your media library.

### Configuration

- **Container Name**: jellyfin
- **Image**: jellyfin/jellyfin
- **Network Mode**: host
- **Volumes**:
  - `./jellyfin/config:/config`: Store Jellyfin configuration data.
  - `/mnt/USB/cache:/cache`: Cache directory for improved performance.
  - `/mnt/USB:/media/media`: Media library directory.
- **Extra Hosts**: 
  - `"host.docker.internal:host-gateway"`: Enable access to the host's networking from within the container.
- **Restart Policy**: unless-stopped

Access the Jellyfin web interface by navigating to http://localhost:8096. Follow the setup wizard to configure your media libraries.

## Getting Started

1. Clone this repository to your local machine.
2. Make sure Docker and Docker Compose are installed.
3. Customize the configuration files (`docker-compose.yml`) as needed.
4. Run `docker-compose up -d` to start the containers in the background.
5. Access Pi-hole at http://localhost:80/admin and Jellyfin at http://localhost:8096.

Feel free to adjust the configuration to suit your specific requirements. For more detailed information, refer to the official documentation of [Pi-hole](https://pi-hole.net/) and [Jellyfin](https://jellyfin.org/).
