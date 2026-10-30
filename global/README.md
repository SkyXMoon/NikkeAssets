# NIKKE Global 角色数据仓库

国际服全部可玩角色的本地资源提取数据。

## 目录结构

```nglobal/
├── characters/                 # 按角色组织（角色码目录）
│   └── {角色码}/
│       ├── images/
│       │   ├── full/           # 全身立绘（1024×1024，部分 2048×2048）
│       │   ├── mi/             # 半身（256×512）
│       │   ├── si/             # 头像（128×128 基准，含资源原始裁剪尺寸）
│       │   └── skills/         # 该角色技能图标（技能1/技能2/爆裂）
│       └── meta.json           # 角色元数据 + 文件引用
├── data/                       # 全量数据表 + 技能图标库
│   ├── nikke_characters.csv    # 角色清单（含技能 Id 与图标引用）
│   ├── nikke_combat.csv        # 战斗数据（HP/攻击/防御/武器参数）
│   ├── nikke_skills.csv        # 技能数据（槽位/Id/中英名/描述/图标）
│   ├── nikke_skill_levels.csv  # 技能每级数值（全量）
│   ├── squad_list.csv          # 部队清单（SquadInfoTable，含图标引用）
│   └── squad_icons/            # 全量部队图标 PNG
└── index/                      # 索引与统计
    ├── characters_index.csv    # 角色索引（角色码/ResourceId/中英名/皮肤/技能图标/目录）
    └── index.json              # 汇总统计
```n
## 数据口径

- **战斗数据**（nikke_combat.csv）：Damage 除以 100；ChargeTime/ReloadTime 除以 1000 换算秒；BurstEnergyPerShot 除以 10000 换算百分比；FullChargeDamage 除以 100 换算百分比。
- **技能每级数值**（nikke_skill_levels.csv）：来自 SkillInfoTable（DescriptionValueList），覆盖全部技能组的每一级成长数值，技能组 Id 与 nikke_skills.csv 的技能组 Id 对应。
- **皮肤序号**：00/01/02/…/99 等为各皮肤变体序号；同一角色多皮肤时 images/full、mi、si 内同名序号互相对应。
- **头像 si**：资源合图（Sprite Atlas）导出，尺寸以资源原始裁剪为准（基准 128×128）。
- **立绘 full**：极少数角色皮肤为 2048×2048 原生高清立绘，按资源原样保留。
- **部队图标**（squad_icons/）：来自 icons-squad(hd) 资源组解包，命名 icn_material_present_squad_<slug>.png，共 49 个；部队清单 69 个（SquadInfoTable），20 个无图标资源（联动/空降小队等），详见 squad_list.csv。
