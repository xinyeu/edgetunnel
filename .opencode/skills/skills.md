# edgetunnel 打包 Skill

## 功能
将 edgetunnel 项目打包成 zip 包，结构与原包一致。

## 目录结构
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

## 打包流程

1. **创建临时目录** - 在项目根目录创建 `edgetunnel-main/`（此目录已加入 .gitignore）
2. **从原始zip解压** - 从 `deploy/edgetunnel.zip` 解压获取文件结构
3. **替换_worker.js** - 用最新 `_worker.js` 替换 `edgetunnel-main/_worker.js`
4. **打包成zip** - 在 `edgetunnel-main/` 目录执行打包
5. **移动到deploy** - 复制 `edgetunnel-main.zip` 到 `deploy/edgetunnel.zip`
6. **清理临时文件** - 删除 `edgetunnel-main/` 临时目录

## 示例命令
```bash
# 1. 创建临时目录并解压原始结构
mkdir -p edgetunnel-main
cd /tmp && unzip -o /path/to/edgetunnel.zip -d edgetunnel-main

# 2. 复制最新worker.js
cp /path/to/_worker.js edgetunnel-main/_worker.js

# 3. 打包（在edgetunnel-main目录内执行）
cd edgetunnel-main && zip -r ../edgetunnel-main.zip .

# 4. 移动到deploy目录
mv ../edgetunnel-main.zip deploy/edgetunnel.zip

# 5. 清理临时目录
cd .. && rm -rf edgetunnel-main
```

## 注意事项
- 临时目录 `edgetunnel-main/` 已在 .gitignore 中，不会提交到 GitHub
- deploy 目录只保留 edgetunnel.zip，不要提交其他文件