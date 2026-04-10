# Deploy 打包流程

## 打包步骤

1. 下载 GitHub archive:
   ```
   wget https://github.com/cmliu/edgetunnel/archive/refs/heads/main.zip
   ```

2. 解压到 deploy 目录:
   ```
   unzip main.zip -d deploy
   mv deploy/edgetunnel-main/* deploy/
   rmdir deploy/edgetunnel-main
   ```

3. 创建 zip 压缩包:
   ```
   cd deploy && zip -r ../edgetunnel.zip . && cd ..
   ```

## 目录结构

打包后的目录结构应与 GitHub archive 一致，包括 `.github` 子目录：

```
deploy/
├── .github/
│   └── workflows/
├── src/
├── ... (其他文件)
└── edgetunnel.zip
```

## 需要提交的文件

- `deploy/` 目录
- `edgetunnel.zip`
