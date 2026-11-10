# loon-config

Personal [Loon](https://nsloon.app) configuration for iOS, version-controlled so the phone pulls it by URL.

## 在 Loon 里填这个地址

**推荐这条**——实时透传，没有缓存：

```
https://ghfast.top/https://raw.githubusercontent.com/kosocn/loon-config/main/loon.conf
```

直连 raw（时通时不通，可用但看运气）：

```
https://raw.githubusercontent.com/kosocn/loon-config/main/loon.conf
```

**不要用 jsdelivr 那个镜像。** 它按分支缓存约 12 小时，改完配置你半天看不到新内容，会以为没生效。

换完内容后，Loon 里要进「配置」下拉刷新才会重新拉取。

## 结构

分流逻辑照搬家里那台 OpenClash（openclash-config-v9.1）：**按服务分策略组**，不是只按地区切一刀。

| 类别 | 组 | 说明 |
|---|---|---|
| 服务 | 默认代理 / 漏网之鱼 / Gemini / ChatGPT / YouTube / Google / GitHub / OneDrive / Microsoft / TikTok / Netflix / Telegram / PayPal | 远程规则里 `policy=` 指向的就是这些名字 |
| 地区·自动 | 全部自动 / 香港自动 / 台湾自动 / 日本自动 / 狮城自动 / 美国自动 | `url-test`，延迟最低者胜，会漂 |
| 地区·故转 | 香港故转 / 台湾故转 / 日本故转 / 狮城故转 / 美国故转 | `fallback`，按序取第一个可用，IP 稳定不漂 |
| 地区·手选 | 全部节点 / 香港节点 / 台湾节点 / 日本节点 / 狮城节点 / 美国节点 | `select`，可挑单个节点 |

**每个服务组的第一位都是「全部自动」。** 这样即使你的机场没有某个地区的节点、对应的地区组是空的，也不会断网——最多是没走到「最想走的那条路」。

想让 Gemini 固定走美国：进「策略」→ Gemini → 选「美国自动」或「美国节点」。规则不用改。

## 规则从哪来

- 本地规则：`[Rule]` 段，二手平台按站点地区出站、强制直连白名单、自有服务走默认代理。这部分是从家里配置逐条搬过来的。
- 远程规则：`[Remote Rule]` 段，全部取自 [blackmatrix7/ios_rule_script](https://github.com/blackmatrix7/ios_rule_script) 的 Loon 格式，每天自动更新。
- 顺序：本地规则 → 远程规则（局域网 → 国内 → 苹果 → 各服务 → 境外兜底）→ `FINAL`。

## 插件

只开了 4 个：`blockAds`（538 款 App 去广告）、`YouTube_remove_ads`、`SubStore`（订阅转换）、`ScriptHub`。

其余在文件里列着但 `enabled=false`，想要哪个把 false 改成 true。

**全部插件依赖 MitM。** 不装证书就只有分流、一个广告都拦不住。路径：设置 → 通用 → 关于本机 → 证书信任设置 → 打开 Loon 那一项。

## 排错

| 现象 | 原因 | 处理 |
|---|---|---|
| 策略页某个地区组是空的 | 节点名里没有该地区关键词，`[Remote Filter]` 的正则没匹配上 | 改 `FilterKey` 适配你的节点命名，或把该组的规则改指「默认代理」 |
| 全部组也是空的 | 订阅没加载进来 | 先解决订阅，配规则没用 |
| 能上外网但广告还在 | MitM 证书没信任 | 装证书 |
| 国内网站变慢 | `GEOIP,CN,DIRECT` 没生效 | 检查 `geoip-url` 能不能下载 |

## 规矩

- **这个仓库是公开的，任何凭证都不许进来。** 订阅链接、节点密码、机场 token 一律不进文件。
- 订阅在 Loon 里单独添加（配置 → 节点 → 添加订阅），只存在手机本地。
- `[Remote Proxy]` 段保持空着。

## 更新流程

1. 改 `loon.conf`
2. 推到 `main`
3. Loon 里进「配置」下拉刷新

镜像地址有缓存，改完几分钟内可能还是旧内容；急用就走 raw 或 ghfast。
