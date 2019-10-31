## Github

> docker-compose.yml

```yml
version: '2'

services:
  drone-server:
    container_name: drone-server
    image: drone/drone:1
    restart: always
    ports:
      - '80:80'
      - '443:443'
    environment:
      - DRONE_DEBUG=true
      - DRONE_AGENTS_ENABLED=true
      - DRONE_GITHUB_SERVER=${DRONE_GITHUB_SERVER}
      - DRONE_GITHUB_CLIENT_ID=${DRONE_GITHUB_CLIENT_ID}
      - DRONE_GITHUB_CLIENT_SECRET=${DRONE_GITHUB_CLIENT_SECRET}
      - DRONE_SERVER_HOST=${DRONE_SERVER_HOST}
      - DRONE_SERVER_PROTO=http
      - DRONE_RPC_SECRET=${DRONE_RPC_SECRET}
      - DRONE_LOGS_TRACE=true
    volumes:
      - /data/drone:/data
  drone-agent:
    container_name: drone-agent
    image: drone/agent:1
    restart: always
    depends_on:
      - drone-server
    environment:
      - DRONE_DEBUG=true
      - DRONE_RPC_SECRET=${DRONE_RPC_SECRET}
      - DRONE_RPC_HOST=drone-server
      - DRONE_RPC_PROTO=http
      - DRONE_RUNNER_CAPACITY=3
      - DRONE_LOGS_TRACE=true
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
      - /usr/local/bin/docker:/usr/local/bin/docker
```

> .env

```.env
# Github
DRONE_GITHUB_SERVER=https://github.com
DRONE_GITHUB_CLIENT_ID=fc10bde9367cf04f503b
DRONE_GITHUB_CLIENT_SECRET=6880aace7103e9dbdf9e2054d9fe70a4dc74919b
DRONE_SERVER_HOST=drone.prous.cn

# Gitea
DRONE_GITEA_SERVER=gitea
DRONE_GITEA_CLIENT_ID=
DRONE_GITEA_CLIENT_SECRET=

# 统一密钥
DRONE_RPC_SECRET=9e311c3eb8ef61b0030d1eb2813fb057
```