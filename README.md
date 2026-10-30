# NikkeAssets

NIKKE 公共数据资产仓库。

当前内容已清理：旧版 QQ 推荐图静态快照不再维护。QQ 推荐图已改为服务器端按实时统计数据动态生成，不依赖本仓库。

后续本仓库仅用于发布公共数据资产，按 `global/`（国际服）与 `cn/`（国服）同构目录组织，两个区各自版本管理。

## 分区

| 分区 | 内容 | 状态 |
| --- | --- | --- |
| `global/` | 国际服（Global）数据 | 已交付 |
| `cn/` | 国服（CN）数据 | 已交付 |

两个区目录结构一致：

```text
global/            cn/
├── characters/    ├── characters/     # 按角色：{角色码}/images/{full,mi,si,skills} + meta.json
├── data/          ├── data/           # 角色表 / 技能 / 等级 / 图标
└── index/         └── index/          # index.json 统计 + characters_index.csv 清单
```

## CDN 引用

仓库通过 jsDelivr 提供 CDN 访问，**请按标签或提交号引用，不要使用浮动地址**。

```text
https://cdn.jsdelivr.net/gh/SkyXMoon/NikkeAssets@<标签或提交号>/global/...
https://cdn.jsdelivr.net/gh/SkyXMoon/NikkeAssets@<标签或提交号>/cn/...
```

当前标签：

| 标签 | 说明 |
| --- | --- |
| `2026-10-data` | 2026-10 完整发布 |

示例：

```text
# 国际服索引
https://cdn.jsdelivr.net/gh/SkyXMoon/NikkeAssets@2026-10-data/global/index/index.json

# 国服索引
https://cdn.jsdelivr.net/gh/SkyXMoon/NikkeAssets@2026-10-data/cn/index/index.json

# 单个角色元数据（国服 麦斯威尔）
https://cdn.jsdelivr.net/gh/SkyXMoon/NikkeAssets@2026-10-data/cn/characters/c102/meta.json
```

说明：

- GitHub 单文件上限 100MB，jsDelivr 单文件上限 20MB；本仓库当前最大文件 11.5MB，均在限内。
- 标签发布后 CDN 首次访问可能有短暂缓存延迟；内容更新请发新标签，不要依赖同一地址的内容变化。
- `@main` 可取最新，但生产环境建议固定标签或提交号。

## 版本记录

完整版本信息见 [`releases.json`](releases.json)：各区服客户端版本、数据更新时间、角色 / 图片 / 图标数量。

## 说明

- 旧文件与历史提交已移除，旧链接不再保证可用。
- 引用请使用明确版本，不要依赖浮动地址。
- 国服角色数量少于国际服属正常现象，两服内容自然不同；各分区仅保证自身数据自洽：`index/characters_index.csv` 与实际 `characters/` 目录一致。
