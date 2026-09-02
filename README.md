# reader-railway-template
Railway template of reader

## 环境变量

```
# === reader 服务 ===
SPRING_PROFILES_ACTIVE=prod
## 用户上限,默认50
READER_APP_USERLIMIT=5
## 用户书籍上限,默认200
READER_APP_USERBOOKLIMIT=20
## 开启缓存章节内容 V2.0
READER_APP_CACHECHAPTERCONTENT=true
## 远程 Webview 服务 API 地址，服务端之间可以访问即可，不一定需要公网暴露
READER_APP_REMOTEWEBVIEWAPI=${{remote-webview.RAILWAY_PRIVATE_DOMAIN}}
## 下面都是多用户模式配置
## 开启登录鉴权，开启后将支持多用户模式
READER_APP_SECURE=true
## 管理员密码  建议修改
READER_APP_SECUREKEY=请修改为你的密码
## 注册邀请码 建议修改,如不需要可注释或删除
READER_APP_INVITECODE=请修改为你的邀请码

# === read-aloud 服务 ===
## Azure Speech API Key
TOKEN=请填入你的Azure Speech API Key
## 是否开启调试模式
DEBUG=false
```

## reader 镜像版本

镜像说明（三选一）：
  - 标准版 (161MB)：Amazon Corretto JRE，通用场景首选，兼容性最好。
  - Slim版 (256MB)：jlink 定制 JRE，仅含必要模块。
  - OpenJ9版 (616MB)：IBM Semeru JRE，启动快、运行时内存低，适合 ARM64 或小内存服务器。Railway 默认使用。

`services/reader/railway.yml`:

```
[build]
#image = "changshengyu/reader:latest"
#image = "changshengyu/reader:slim-latest"
image = "changshengyu/reader:openj9-latest"

[deploy]
restartPolicyType = "ON_FAILURE"
restartPolicyMaxRetries = 10
```
