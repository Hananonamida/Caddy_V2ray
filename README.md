# Caddy V2ray SSL TSL Websocket 整合镜像 Arm版本

[![Build Docker Images](https://github.com/anerg2046/Caddy_V2ray/actions/workflows/workflow.yaml/badge.svg)](https://github.com/anerg2046/Caddy_V2ray/actions/workflows/workflow.yaml)

### 环境需求：
- 一台运行docker的主机，仅限ARM
- 一个域名，可以是二级域名，并已解析A记录到你的主机IP
- 一个邮箱地址，用于caddy申请SSL证书，如果不填将不会申请证书，且caddy只监听80端口
- 可直接使用此镜像 hananonamida/caddy_v2ray_arm:latest 

### 常见操作系统docker安装教程：

参见官方文档
https://docs.docker.com/engine/install/

### 快速开始

可用参数

| 参数名      | 是否必须 | 默认值 | 说明
|----------| ----  | ---- | ----
| DOMAIN   | 是 | 无 | 申请证书的域名，可以是二级域名
| WS_PATH  | 是 | 无 | WS_PATH
| UUID     | 是 | 无 | UUID
| EMAIL    | 否 | 无 | 申请证书的邮箱，如果不填将不会申请证书，且caddy只监听80端口


```
docker run -d \
  --publish=80:80 \
  --publish=443:443 \
  --env=DOMAIN=v2.mooim.com \
  --env=EMAIL=r.anerg@gmail.com \
  --env=EMAIL=r.anerg@gmail.com \
  --env=WS_PATH="/3c5d4d290/" \
  --env=UUID="8a9420cf-c6dd-4d06-ae1d-5519ac8c082f" \
  --restart=always \
  --name=caddy_v2ray_arm \
  hananonamida/caddy_v2ray_arm:latest
```

> 开放`80`端口是因为zerossl在发证书的时候需要先访问80端口

之后运行命令`docker logs caddy_v2ray`（注意，这里的`caddy_v2ray`要和命令中的`--name`的值一致）

你就能看到类似如下的输出：

```
=====================================
V2ray 配置信息
地址（address）: v2.mooim.com
端口（port）： 443
用户id（UUID）： a736b1ef-a96e-4f35-8f6b-5b76a050e282
加密方式（security）： 自适应
传输协议（network）： ws
伪装类型（type）： none
路径（不要落下/）： /8768f5ff9/
底层传输安全： tls
=====================================
=========复制以下内容进行导入==========
vmess://ewogICAgInYiOiAiMiIsCiAgICAicHMiOiAidjIubW9vaW0uY29tIiwKICAgICJhZGQiOiAidjIubW9vaW0uY29tIiwKICAgICJwb3J0IjogIjQ0MyIsCiAgICAiaWQiOiAiYTczNmIxZWYtYTk2ZS00ZjM1LThmNmItNWI3NmEwNTBlMjgyIiwKICAgICJhaWQiOiAiMCIsCiAgICAibmV0IjogIndzIiwKICAgICJ0eXBlIjogIm5vbmUiLAogICAgImhvc3QiOiAidjIubW9vaW0uY29tIiwKICAgICJwYXRoIjogIi84NzY4ZjVmZjkvIiwKICAgICJ0bHMiOiAidGxzIgp9
=========复制以上内容进行导入==========
{"level":"info","ts":1656863534.6378205,"msg":"using provided configuration","config_file":"/etc/caddy/Caddyfile","config_adapter":"caddyfile"}
{"level":"warn","ts":1656863534.6384249,"logger":"caddyfile","msg":"Unnecessary header_up X-Forwarded-For: the reverse proxy's default behavior is to pass headers to the upstream"}
.......
```

