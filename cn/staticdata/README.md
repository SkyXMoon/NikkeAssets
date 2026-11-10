# 国服 · 静态数据表（staticdata/）

本目录按**源字段名、源值**逐张导出国服解密源包中的核心战斗 / 角色 / 技能数据表。与 `../data/` 的展示表是两套数据：`data/` 是裁剪、中文列名、单位换算后的展示契约；本目录不裁剪、不翻译、不换算、不改 ID。

## 数据版本

| 项 | 值 |
|---|---|
| 源版本 | `data/ob17/143226` |
| 源包 | `StaticData.zip`（8,845 条目 / 18,684,150 字节） |
| 源包 SHA256 | `1f966c7adbb7a450f59f8fbc8741b05867f798ba659c48c2e2f90c79444ab115` |
| 字段名样式 | snake_case（源 JSON 原字段名） |

## 目录

| 路径 | 内容 |
|---|---|
| `csv/` | 106 张表，每表一个 CSV；UTF-8 BOM，表头 = 源字段名 |
| `json/` | 106 张表，每表一个 JSON：`table / schema_class / source_version / record_count / fields / records` |
| `manifest.core.json` | 逐表 `rows` / `field_count` / `leftover_bytes` / `csv_sha256` / `json_sha256` |
| `README.md` | 本说明 |

## 统计

| 项 | 值 |
|---|---:|
| 数据表 | 106 张 |
| CSV + JSON 文件 | 212 |
| CSV 合计 | 25,694,797 字节 |
| JSON 合计 | 64,511,463 字节 |
| 合计 | 90,206,260 字节（86.0 MB） |

## 数据契约

- 字段名保持源样式；两服源格式不同（国服为 JSON、国际服为 mpk + schema），不强行统一。
- 名称 / 描述列保留 `Locale_...` 原始 key 与源枚举名，不替换为中文；译文请用各自的 Locale 库自行关联。
- 字段取全记录并集，稀疏字段也保留。
- 数值一律为源值，不做换算；下方换算表仅供消费方参考。
- JSON 原生保留数组 / 对象；CSV 中写成紧凑 JSON 字符串。
- 本目录只由国服源包生成，与国际服物理隔离。

## 字段单位参考

| 源字段（国服 / 国际服） | 常见口径 |
|---|---|
| `charge_time` / `ChargeTime` | ÷100 → 秒 |
| `reload_time` / `ReloadTime` | ÷100 → 秒 |
| `burst_energy_pershot` / `BurstEnergyPershot` | ÷10000 → % |
| `full_charge_damage` / `FullChargeDamage` | ÷100 → % |
| `damage` / `Damage` | ÷100 → % |
| `rate_of_fire` / `RateOfFire` | 原值 → RPM |
| `max_ammo` / `MaxAmmo` | 原值 → 发 |

`CoreDamageRate` / `core_damage_rate`、`SkillCooltime` / `skill_cooltime` 可按 ÷100 解读（20000 → 200%、4000 → 40s）；本目录保留原值，不以推断值覆盖源数据。其它字段不假设单位。

## 完整性与校验

- `manifest.core.json` 中 106 张表的 `leftover_bytes` 全为 0（按 schema 完整消费）。
- 逐文件哈希可用 `manifest.core.json` 的 `csv_sha256` / `json_sha256` 自行比对。
