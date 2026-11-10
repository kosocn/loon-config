# loon-config

Personal [Loon](https://nsloon.app) configuration for iOS, version-controlled so the phone can pull it by URL.

## 在 Loon 里填这个地址

配置 → 右上角 `+` → **从 URL 下载**：

```
https://raw.githubusercontent.com/kosocn/loon-config/main/loon.conf
```

`raw.githubusercontent.com` 在国内常常直连不通，备用镜像（择一）：

```
https://cdn.jsdelivr.net/gh/kosocn/loon-config@main/loon.conf
https://ghfast.top/https://raw.githubusercontent.com/kosocn/loon-config/main/loon.conf
```

## 更新流程

1. 改 `loon.conf`
2. 推到 `main`
3. Loon 里进「配置」下拉刷新一下

镜像地址有缓存，改完几分钟内可能还是旧内容；急用就走 raw 或 ghfast。

## 规矩

- **这个仓库是公开的，任何凭证都不许进来。** 订阅链接、节点密码、机场 token 一律不进文件。
- 订阅在 Loon 里单独添加（配置 → 节点 → 添加订阅），只存在手机本地。
- 配置里的 `[Remote Proxy]` 段落保持空着，别手滑填进去。

## 文件

| 文件 | 说明 |
|---|---|
| `loon.conf` | 主配置。基于莫离懒人配置，本地做过加固，改动记录写在文件头 |
