# 国 服 · 全量静态数据交付（staticdata/）

> **GitHub 推送范围（A 方案）**：本仓库只推送核心战斗/角色/技能数据表，**不是**本地全量交付的全部内容。完整全量保留在本地工作副本与分卷包，详见文末「GitHub 推送范围」。

生成时间：2026-11-10T07:48:35+08:00

## 这是什么

本地工作副本中的本目录是本服**解密源包内的全部表**，按**源字段名、源值**逐张导出；**GitHub 仓库中只推送其中核心战斗/角色/技能子集**（见文末）。
与 `../data/` 下 4 张网页展示表是两套东西：`data/` 是裁剪+中文列名+单位换算后的展示契约，
本目录是不裁剪、不翻译、不换算的原始全字段数据。**`data/` 及 `characters/` 等既有文件本次未改动。**

## 数据版本

| 项 | 值 |
|---|---|
| 源版本 | `data/ob17/143226` |
| 源 zip | `Runs/cn/pipeline/20261101_1506/StaticData.zip` |
| 源 zip SHA256 | `1f966c7adbb7a450f59f8fbc8741b05867f798ba659c48c2e2f90c79444ab115` |
| 源 zip 字节 | 18,684,150 |
| 源 zip 条目 | 8,845 |
| 版本证据 | `Runs/cn/pipeline/20261101_1506/report.json` |
| 说明 | 国服 11-01 抓取包；11-09 接口复核版本未变（见 11-09 工作日志） |

## 目录

| 路径 | 内容 |
|---|---|
| `csv/` | 每表一个 CSV，UTF-8 BOM，表头=源字段名 |
| `json/` | 每表一个 JSON：`table / schema_class / source_version / record_count / fields / records` |
| `raw/` | 源包内非表结构文件、以及无法结构化解析的原始字节（不丢、不猜） |
| `source/` | 解密后的源 zip 副本，SHA256 与源一致 |
| `manifest.json` | 逐表行数、字段清单、CSV/JSON 的 SHA256、未解析清单 |

## 统计

| 项 | 值 |
|---|---|
| 源条目 | 8,845 |
| 结构化表 | 8,832 |
| 总记录行 | 797,736 |
| CSV 合计 | 203.6 MB |
| JSON 合计 | 335.2 MB |
| 原样保留条目 | 13 |
| 无法解析条目 | 0 |

## 契约与口径

- **字段名样式**：snake_case（源 JSON 原字段名）。两服源格式不同（国服源为 JSON、国际服源为 mpk+schema），因此字段名样式不同，**不强行统一**。
- **不翻译**：名称/描述列保留 `Locale_...` 原始 key 或源枚举名，不替换为中文。需要译文请用各自的 Locale 库自行关联。
- **不裁剪**：字段取全记录并集，稀疏字段也保留（避免首行 keys 丢列）。
- **不换算**：所有数值为源值；下方换算仅说明既有 `data/` 展示表当时的口径，本目录不做换算。
- **嵌套值**：JSON 原生保留数组/对象；CSV 中写成紧凑 JSON 字符串。
- **两服物理隔离**：本目录只由本服源包生成，不与另一服合并。

## 既有展示表用过的单位换算（仅参考，本交付不改值）

来源：`NIKKE_Workflow/Scripts/03_数据更新与打包/add_cn_skill_rows.py` 第 115–129 行。

| 源字段（国服 / 国际服） | 展示表口径 |
|---|---|
| `charge_time` / `ChargeTime` | ÷100 → 秒 |
| `reload_time` / `ReloadTime` | ÷100 → 秒 |
| `burst_energy_pershot` / `BurstEnergyPershot` | ÷10000 → % |
| `full_charge_damage` / `FullChargeDamage` | ÷100 → % |
| `damage` / `Damage` | ÷100 → % |
| `rate_of_fire` / `RateOfFire` | 原值 → RPM |
| `max_ammo` / `MaxAmmo` | 原值 → 发 |

审计中 `CoreDamageRate`/`core_damage_rate`、`SkillCooltime`/`skill_cooltime` 按 ÷100 解读（20000→200%、4000→40s），
但这属于消费方口径推断，**本目录保留原值**，不以推断值覆盖源数据。所有其它字段一律原值直取，不假设单位。

## 未解析 / 原样保留

- `raw/` 内的文件是源包字节，`manifest.json` 的 `raw_entries_detail` / `unresolved` 有逐项说明。
- 国际服 mpk 中带 `.` 后缀的是**分片表**（如 `ScenarioDialogTable.d_main_24_14_s`），按主表名映射 schema 解析；
  早前一次扫描未做该映射，误把 8,934 张分片表当成「无 schema」，本次已按流水线 `convert_single` 规则正确处理。
- 无 schema 可映射的条目不猜结构、不补造记录，原样保留。

## 已知解析不完整（如实标注）

- 无：全部结构化表 `leftover_bytes=0`。

## 自检

`manifest.json` 记录每表 `csv_sha256` / `json_sha256` / `rows` / `fields` / `leftover_bytes`；
`leftover_bytes` 为 mpk 解析后的剩余字节，0 表示完整消费。可用任一哈希工具比对。

构建器：`NIKKE_Workflow/Scripts/03_数据更新与打包/build_full_staticdata.py`

## GitHub 推送范围（A 方案，2026-11-10）

为避免仓库膨胀，GitHub 只跟踪核心数据表；本地 `cn/staticdata/` 的全量文件**未删除、未移动**，仅由仓库根 `.gitignore` 排除。

| 项 | 本服数值 |
|---|---:|
| 全量结构化表 | 8,832 张 |
| 本服推送表 | **106 张**（CSV + JSON 共 212 文件） |
| 推送体积 | **86.0 MB** |

**纳入范围**：审计报告《未交付的核心战斗表清单.csv》的 70 张核心战斗表按本服源包实际存在的表无条件纳入（两服表名不完全相同），另加主表名以 Character/Skill/Shot/Stat/Function/StateEffect/Buff/Monster/Equip/Arena/Weapon/Spot/Burst/Item/Costume 等关键词开头的表；**排除** `ScenarioDialogTable.*` 等剧情对话表与 `FieldMapData_*` 地图数据。核心伤害 `core_damage_rate` / `CoreDamageRate`、爆裂技能 CD `skill_cooltime` / `SkillCooltime`、`CharacterStatTable`、`FunctionTable`、`StateEffectTable`、`BuffTable`、`ArenaTable`、`AutoChargeTable` 等均已包含。

**文件说明**：仓库内的 `manifest.core.json` 是**推送子集**的逐表行数/字段数/SHA256；本地的 `manifest.json` 是**全量**清单（未推送，别拿它核对仓库）。未推送内容主要是剧情文本，与模拟器数值无关。

**获取完整全量**：本地 `cn/staticdata/` 原样保留；或用分卷包 `Runs/data_completeness_audit_20261110/dist/cn/`（解压到同一目录自动合并）。规则与白名单清单见 `Runs/data_completeness_audit_20261110/push_whitelist.json`。
