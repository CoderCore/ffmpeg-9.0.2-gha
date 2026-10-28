# FFmpeg 9.0.2 纯稳定版 · Linux x86_64 静态编译（GitHub Actions 云编译）

把这个目录推送到任意 GitHub 仓库（公开或私有均可，免费额度 2000 分钟/月足够），
Actions 会自动在 GitHub 的 Ubuntu 云 Runner 上完成：

1. 从 ffmpeg.org 官方下载 `ffmpeg-9.0.2.tar.xz` 及 GPG 签名
2. 用 FFmpeg 官方签名公钥 **验签**（失败即终止）
3. `--enable-static --disable-shared` 静态编译
   （含 libx264 / libx265 / libmp3lame / libvorbis / libopus，GPL）
4. 校验产物：`ffmpeg -version` 必须输出 `n9.0.2`，且 `file` 确认为 **statically linked**
5. 打包上传 artifact：`ffmpeg-9.0.2-linux64-static.tar.xz` + sha256

## 操作步骤（约 10~20 分钟）

```bat
cd D:\AI\ffmpeg-9.0.2-gha
git init
git branch -M main
git add .
git commit -m "build ffmpeg 9.0.2 static"
git remote add origin https://github.com/<你的用户名>/<仓库名>.git
git push -u origin main
```

> 在 GitHub 网页上先新建一个**空仓库**（不要勾选生成 README）。
> 不会用命令行也可以：把本目录里的 `.github` 文件夹直接拖进仓库网页上传。

推送后打开仓库的 **Actions** 标签页，等待绿色对勾，然后在该次运行页面
底部的 **Artifacts** 区域下载 `ffmpeg-9.0.2-linux64-static`。

## 在 Linux 上使用

```bash
tar -xJf ffmpeg-9.0.2-linux64-static.tar.xz -C /opt/ff902
/opt/ff902/bin/ffmpeg -version
# 输出第一行应为: ffmpeg version n9.0.2  Copyright ...
```
