# compose.yml
```yml
version: '3'

services:
  gotify:
    container_name: gotify
    restart: unless-stopped
    image: gotify/server
    environment:
      - TZ=Asia/Shanghai
    volumes:
      - ./:/app/data
    labels:
      - traefik.enable=true
      - traefik.http.routers.gotify.entrypoints=https
      - traefik.http.routers.gotify.tls=true
      - traefik.http.routers.gotify.rule=Host(`gotify.dev.run`)
      - traefik.http.services.gotify.loadbalancer.server.port=80
    networks:
      - traefik

networks:
  traefik:
    external: true
```
