# 硬性条件

## 基本规则

1. **回复必须追加** - 所有回复的最后必须追加"回复：opencode"
2. **必须使用中文** - 所有回复必须使用中文

## 自测规则

1. **JS语法检查** - 修改 JS 文件后必须运行 `node --check` 检查语法
2. **按需测试** - 根据修改的内容进行对应测试：
   - 修改了 `_worker.js`：必须语法检查
   - 修改了配置逻辑：检查配置解析是否正确
   - 添加了新功能：验证功能可用性
3. **提交前检查** - 每次提交前确保语法正确

## Git 提交规则

1. **SSH密钥** - 此项目使用 `~/.ssh/git_edgetunnel` 进行无密码 SSH 提交
2. **.opencode目录提交** - .opencode 目录需要提交到 GitHub
3. **排除规则** - openclaw 相关的任何文档不要提交到 GitHub（如 .openclaw/、memory/、HEARTBEAT.md、IDENTITY.md、SOUL.md、TOOLS.md、USER.md 等）
4. **提交日志** - 提交信息需要写入大概修改了哪些内容
5. **更新日志** - 凡是修改，除了写文档，都要写入 doc/CHANGELOG.md

## Deploy 目录规则

1. **只保留zip** - deploy目录只保留 edgetunnel.zip，不提交其他临时文件

## 功能说明

- **提交** - 执行 git add + commit + push，推送使用 SSH 密钥 `~/.ssh/git_edgetunnel`
- **发布** - 打出 edgetunnel.zip 包并提交到 deploy 目录