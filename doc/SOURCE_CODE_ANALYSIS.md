# EdgeTunnel 源码分析

## 核心函数

### 1. 主入口 `fetch(request, env, ctx)`

位置: `_worker.js:11-402`

处理所有 HTTP 请求，根据路径和请求方法分发到不同处理函数。

- `version` - 版本信息
- `WebSocket` - WebSocket 代理
- `gRPC/XHTTP` - 代理请求
- `/login` - 登录
- `/admin/*` - 管理面板
- `/sub` - 订阅生成
- `/logout` - 登出

### 2. `处理XHTTP请求(request, yourUUID)`

位置: `_worker.js:404-537`

处理 XHTTP 传输的代理请求。

- 读取首包解析协议 (VLESS/Trojan)
- 建立远端连接
- 双向数据转发

关键流程:
```
reader.read() -> 解析首包 -> forwardataTCP/UDP -> 循环读取转发
```

### 3. `处理gRPC请求(request, yourUUID)`

位置: `_worker.js:704-899`

处理 gRPC 传输的代理请求。

- 解析 gRPC 首包
- 建立连接并处理双向流
- 数据帧封装/解封装

### 4. `读取config_JSON(env, hostname, userID, UA, 重置配置)`

位置: `_worker.js:2572-2726`

读取/生成配置 JSON。

- 从 KV 读取或使用默认配置
- 根据环境变量覆盖配置项
- 生成订阅 LINK

### 5. `请求优选API(优选API数组, 端口)`

位置: `_worker.js:2850-3056`

请求外部优选 API 获取 IP 列表。

- 并发请求多个 API
- 解析响应格式
- 返回 IP 数组和反代 IP 池

### 6. `Clash订阅配置文件热补丁(Clash_原始订阅内容, config_JSON)`

位置: `_worker.js:1877-2092`

处理 Clash 订阅配置。

- 替换 UUID
- 处理 ECH 配置
- 处理 gRPC 选项

### 7. `Singbox订阅配置文件热补丁(SingBox_原始订阅内容, config_JSON)`

位置: `_worker.js:2094-2279`

处理 Singbox 订阅配置。

- ECH 配置转换
- DNS 设置
- 协议选项处理

### 8. `请求日志记录(env, request, 访问IP, 请求类型, config_JSON, 是否写入KV日志)`

位置: `_worker.js:2300-2321`

记录请求日志并发送 Telegram 通知。

### 9. 订阅生成逻辑

位置: `_worker.js:309-342`

生成订阅内容的关键步骤:

1. 解析原始 IP 地址 (正则匹配域名/IPv4/IPv6)
2. 生成节点备注
3. 构建节点链接
4. 应用 TLS/ECH 参数

## 数据流

```
客户端 -> Worker.fetch() -> 路由分发
                         |
         +---------------+---------------+
         |               |               |
      /sub           /admin         代理请求
         |               |               |
   订阅生成器         管理API      XHTTP/gRPC
         |                             |
   外部API                       远端服务器
```

## 关键配置

- `UUID`: 用户标识
- `HOST`: 域名
- `PATH`: 路径
- `协议类型`: vl ess/trojan/shadowsocks
- `传输协议`: ws/grpc/xhttp
- `TLS分片`: 开启 TLS 分片
- `ECH`: 加密云蕾