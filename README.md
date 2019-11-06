

## 启动

```bash
# 修改 ssh 允许 root ssh 方式登录
# vim /etc/ssh/sshd_config
PermitRootLogin yes
sudo service sshd restart

# 首先启动
docker-compose up -d gitea nginx

# 进入 gitea 创建应用获取
# http://xxxx.com/login
DRONE_GITEA_CLIENT_ID=xxx
DRONE_GITEA_CLIENT_SECRET=xxx

# 启动 drone 
docker-compose up -d drone
# 授权登录

# 激活其中一个项目
# 设置 secret, 名称和你的 .drone.yml 中的一致，对应的值为 可以使用 密钥登录的 id_rsa 文件内容
ssh_password
```



> drone .env 配置

```.env
# Github
DRONE_GITHUB_SERVER=https://github.com
DRONE_GITHUB_CLIENT_ID=
DRONE_GITHUB_CLIENT_SECRET=
DRONE_SERVER_HOST=drone.prous.cn

# Gitea

DRONE_GITEA_SERVER=http://gitea.prous.cn
DRONE_GITEA_CLIENT_ID=
DRONE_GITEA_CLIENT_SECRET=

# 统一密钥, 可以自己按照 drone 官网上的说明自由生成
DRONE_RPC_SECRET=9e311c3eb8ef61b0030d1eb2813fb057
```