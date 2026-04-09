# EdgeTunnel

基于 Cloudflare Workers 的代理工具，支持 VLESS、Trojan、ShadowSocks 协议。

## 功能特性

- **多协议支持**: VLESS、Trojan、ShadowSocks (SS)
- **多种传输方式**: WebSocket、gRPC、XHTTP
- **TLS 分片**: 支持 Shadowrocket、Happ 格式
- **ECH 支持**: 加密云蕾 (Encrypted Client Hello)
- **本地优选生成**: 本地生成优选 IP 订阅
- **订阅转换**: 支持 Clash、Singbox、Surge、Quantumult、Loon 格式
- **Telegram 通知**: 用量告警通知
- **Admin 管理面板**: Web 管理界面

## 环境变量配置

| 变量名 | 必填 | 说明 |
|--------|------|------|
| `ADMIN` | 是 | 管理密码 |
| `KEY` | 否 | 加密密钥 (默认: 勿动此默认密钥) |
| `UUID` | 否 | 用户 UUID (默认: 自动生成) |
| `HOST` | 否 | 域名 (多个用逗号分隔) |
| `PATH` | 否 | 路径 |
| `PROXYIP` | 否 | 反代 IP (多个用逗号分隔) |
| `KV` | 否 | KV 存储命名空间 |
| `URL` | 否 | 伪装页 URL |
| `BEST_SUB` | 否 | 优选订阅生成器 |
| `GO2SOCKS5` | 否 | SOCKS5 白名单 |
| `DEBUG` | 否 | 调试日志 |

## 使用方法

### 1. 部署 Worker

1. 在 Cloudflare Dashboard 创建 Worker
2. 上传 `_worker.js` 代码
3. 设置环境变量

### 2. 获取订阅

```
https://你的域名/sub?token=MD5(域名+UUID)
```

### 3. 订阅参数

| 参数 | 说明 |
|------|------|
| `target` | 订阅类型: clash/singbox/surge/quanx/loon/mixed |
| `b64` | Base64 编码 |
| `sub` | 优选订阅生成器地址 |

### 4. 管理面板

访问 `/admin` 路径，使用管理员密码登录。

- `/admin/config.json` - 查看/保存配置
- `/admin/ADD.txt` - 自定义优选 IP
- `/admin/tg.json` - Telegram 配置
- `/admin/cf.json` - Cloudflare 配置
- `/admin/init` - 重置配置