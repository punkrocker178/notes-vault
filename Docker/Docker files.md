[[install-chromium.sh]]
[[Docker commands]]
# Node and Chromium image
```dockerfile
FROM node:22.2-slim
ADD install-chromium.sh /install-chromium.sh
RUN ./install-chromium.sh

ENTRYPOINT ["docker-entrypoint.sh"]
```

# Custom Keycloak image
```Dockerfile
FROM quay.io/keycloak/keycloak:23.0.1
// Custom theme
COPY ./themes/opphub-theme/ /opt/keycloak/themes/opphub-theme/

ENTRYPOINT [ "/opt/keycloak/bin/kc.sh" ]
```
# Compose Keycloak
```yml
services:
  web:
    image: "nginx:latest"
    ports:
      - "8081:80"
    networks:
      - hiu-network
    # volumes:
    #   - .:/code
    # environment:

  stmp4dev:
    image: "rnwood/smtp4dev"
    ports:
      - "3000:80"
      - "2525:25"
    networks:
      - hiu-network
  keycloak:
    image: "hiu/keycloak"
    command: ["start-dev", "--spi-theme-static-max-age=-1", "--spi-theme-cache-themes=false", "--spi-theme-cache-templates=false"]
    ports:
      - "8080:8080"
    environment:
      - KEYCLOAK_ADMIN=admin
      - KEYCLOAK_ADMIN_PASSWORD=admin
    networks:
      - hiu-network

networks:
  hiu-network:
    name: hiu-bridge-network
    external: true
```