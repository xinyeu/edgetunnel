# Changelog

All notable changes to this project will be documented in this file.

## [2026-04-10]

### Added
- 新增 `/opencode` 路由，返回VLESS节点链接，包含访问者IP的地理位置信息（国旗emoji + 城市名 + 序号）
- 订阅节点备注默认显示节点IP的地理位置信息（国旗emoji + 城市名 + 序号）
- 新增 .opencode 智能体配置目录，包含打包规则和工作规则

### Updated
- 更新 AGENTS.md 项目智能体配置文档
- 修复代码缩进问题

## [2026-04-06]

### Added
- 初始版本
- 支持 WebSocket、gRPC、XHTTP 传输
- 支持 VLESS、Trojan、ShadowSocks 协议
- TLS 分片支持
- ECH 加密云蕾支持
- 本地优选 IP 生成
- 订阅转换 (Clash/Singbox/Surge/Quantumult/Loon)
- Admin 管理面板
- Telegram 通知