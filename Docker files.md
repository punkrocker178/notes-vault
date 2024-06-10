# Node and Chromium image
```dockerfile
FROM node:22.2-slim

ADD install-chromium.sh /install-chromium.sh

RUN ./install-chromium.sh

ENTRYPOINT ["docker-entrypoint.sh"]
```