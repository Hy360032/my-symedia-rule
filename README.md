# Symedia 自定义规则 · 个人版

整理自个人 Symedia 实例（`/archive_settings`）的识别规则，共 **636 条有效规则**。
结构参照 [shutu777/symedia-rule](https://github.com/shutu777/symedia-rule)，补充了「捕获组」一类。

## 文件说明

| 文件 | 规则数 | 说明 |
|---|---|---|
| `custom_words.txt` | 180 | 识别词：锁定 TMDB、抓季集、字幕组/发布组/平台归一 |
| `custom_group.txt` | 402 | 制作组：流媒体、压制组、字幕组、RAW 源 |
| `custom_rendering_words.txt` | 52 | 渲染词：编码/画质/音轨归一、季集重映射 |
| `custom_capturing_group.txt` | 2 | 捕获组：发行地区、内容版本 |

合计 636 条规则、52 行分段注释。

## 订阅地址

把对应链接填进 Symedia「归档设置 → 辅助识别」的订阅框：

```text
https://raw.githubusercontent.com/OWNER/REPO/refs/heads/main/custom_words.txt
https://raw.githubusercontent.com/OWNER/REPO/refs/heads/main/custom_group.txt
https://raw.githubusercontent.com/OWNER/REPO/refs/heads/main/custom_rendering_words.txt
https://raw.githubusercontent.com/OWNER/REPO/refs/heads/main/custom_capturing_group.txt
```

填好后把「规则自动更新」的 cron 打开（默认 `30 2 * * *`），之后自动拉取。

## 格式约定

识别词与渲染词：

```text
左式 => 右式
```

- 左式：文件名里的文字或正则，可用 `(?i)` 忽略大小写
- 右式：替换成的片名，或 `{[tmdbid=..;type=tv;s=..;e=..]}` 锁定条目

捕获组：

```text
字段名#正则#
```

- 字段名与正则之间用 `#` 包裹
- 例：`production_country#(?:USA|JPN|KOR)#`

制作组：一行一个组名，顺序不影响识别。

注释用 `#` 开头，不参与匹配。

## 顺序很重要

识别词按顺序匹配，先命中先生效。
所以新增规则不要随意插到中间，改动后建议整段替换。

## 注意事项

- 季集重映射规则会改动归档后的季集编号，改动前先小范围验证
- 带 `tmdbid` 的锁定条目会强制指定条目，写错会导致整剧归错
- 部分规则针对特定剧集定制，换成别的库可能不需要

## 更新日志

见 [CHANGELOG.md](CHANGELOG.md)。

## 许可

MIT
