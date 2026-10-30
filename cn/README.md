---
AIGC:
    Label: "1"
    ContentProducer: 001191440300708461136T1XGW3
    ProduceID: d3a1ba1f58fa9696e95b19f8bb7f2aba_f86662a3d3b211f19101525400de85a5
    ReservedCode1: G3UHen+BjycKgZOA4f/uSmkmPJ0llrBiwAVpHXUcYwgfNxmesK8V3hreg3x2I3Nv9wExBlC8wFqAsTK7RGPeZRop7yak3VnbWb6OIyV+EU9x5sE09l0vGQcwuDneWRBKjqvAnU5kqtlmaWDSUIP0L2AZNEKshAg0MspfhgQ2Ba0nDZCpQ643d0SRNn4=
    ContentPropagator: 001191440300708461136T1XGW3
    PropagateID: d3a1ba1f58fa9696e95b19f8bb7f2aba_f86662a3d3b211f19101525400de85a5
    ReservedCode2: G3UHen+BjycKgZOA4f/uSmkmPJ0llrBiwAVpHXUcYwgfNxmesK8V3hreg3x2I3Nv9wExBlC8wFqAsTK7RGPeZRop7yak3VnbWb6OIyV+EU9x5sE09l0vGQcwuDneWRBKjqvAnU5kqtlmaWDSUIP0L2AZNEKshAg0MspfhgQ2Ba0nDZCpQ643d0SRNn4=
---

# NIKKE 国服（CN）数据分区

本目录存放《NIKKE：胜利女神》国服（CN）角色的本地资源提取数据。数据来源于国服客户端本地资源（NKAB 缓存 + 明文 lss 本地化），以国服已提取资源为准，与国际服（global）数据相互独立。

## 数据说明

- 角色数：161
- 多皮肤角色数：74
- 皮肤变体总数（full/mi 对数）：270
- 图片总数：1270（full 270 / mi 270 / si 272 / skills 458）
- 技能图标数：265
- 技能等级数据行：9810（技能组 1071 个）
- 部队数：57（nikke_characters.csv 部队字段唯一值）
- 部队图标数：50（data/squad_icons/，来自国服本地 icons-squad bundle 解包）

国服角色数量少于国际服属正常现象（两服数据自然不同），本分区仅保证国服自身数据自洽：角色清单（index/characters_index.csv）与实际图片目录（characters/）完全一致，0 缺失 0 多出。

## 目录结构

```text
cn/
├── characters/       # 按角色组织：{角色码}/images/{full,mi,si,skills} + meta.json
│   └── {角色码}/     # 例：c102（麦斯威尔）
│       ├── images/
│       │   ├── full/     # 立绘大图
│       │   ├── mi/       # 中型立绘
│       │   ├── si/       # 小型立绘
│       │   └── skills/   # 技能图标
│       └── meta.json     # 角色元数据（images_dir 为相对路径 cn/characters/{角色码}/images）
├── data/             # 全量数据表 + skill_icons 技能图标库
│   ├── nikke_characters.csv    # 角色表（161 行）
│   ├── nikke_combat.csv        # 战斗数值表（161 行）
│   ├── nikke_skills.csv        # 技能表（483 行）
│   ├── nikke_skill_levels.csv  # 技能等级表（9810 行）
│   ├── squad_list.csv          # 部队清单（57 行，含图标引用）
│   └── squad_icons/            # 部队图标（50 个）
└── index/            # 索引
    ├── characters_index.csv    # 角色索引（161 行）
    └── index.json              # 分区统计
```

## 版本

- client_version：430767（NKSD 版本标识；国服数据表无可靠版本表，以最新 NKSD 标识为准）
- core_revision：null（无对应数据）

## 引用约定

- 分区内全部文件使用相对路径引用（如 cn/characters/c102/images），不依赖绝对路径。
- 图片按角色码目录存放，角色码格式为 c + ResourceId（3 位补零），如 c102。
*（内容由AI生成，仅供参考）*
