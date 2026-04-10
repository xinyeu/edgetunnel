# edgetunnel 打包 Skill

## 功能
将 edgetunnel 项目打包成 zip 包，结构与原包一致。

## 打包规则

### 目录结构
```
edgetunnel-main/
├── .github/workflows/sync.yml
├── .gitignore
├── LICENSE
├── README.md
├── _worker.js
├── img.png
└── wrangler.toml
```

### 打包流程
1. 从 `deploy/edgetunnel.zip` 解压获取原始文件结构
2. 用最新 `_worker.js` 替换 `edgetunnel-main/_worker.js`
3. 打包成 zip（临时文件放 `/tmp`）
4. 复制到项目根目录和 `deploy/` 目录

### 示例命令
```bash
# 解压原始zip获取结构
cd /tmp && unzip /path/to/deploy/edgetunnel.zip

# 替换_worker.js
cp /path/to/_worker.js /tmp/edgetunnel-main/_worker.js

# 重新打包
cd /tmp && zip -r edgetunnel-main.zip edgetunnel-main

# 复制到项目
cp /tmp/edgetunnel-main.zip /path/to/edgetunnel.zip
cp /path/to/_worker.js /path/to/deploy/_worker.js
```