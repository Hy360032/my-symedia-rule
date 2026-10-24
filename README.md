# Symedia 自定义规则 · 个人版

整理自个人 Symedia 实例（`归档设置 → 辅助识别`）的识别规则，共 **636 条有效规则**。

## 订阅地址

在 Symedia 的「归档设置 → 辅助识别」里，四个子标签各自有一个「远程链接」输入框。
一行填一个链接，按下表分别填，不要混填。

### 自定义识别词 → `custom_words.txt`

```text
https://raw.githubusercontent.com/Hy360032/my-symedia-rule/refs/heads/main/custom_words.txt
```

180 条。锁定 TMDB、从文件名抓季集、字幕组与发布组归一、流媒体平台打标。

### 自定义制作组 → `custom_group.txt`

```text
https://raw.githubusercontent.com/Hy360032/my-symedia-rule/refs/heads/main/custom_group.txt
```

402 条。流媒体平台、压制组、字幕组、RAW 源。

### 自定义渲染词 → `custom_rendering_words.txt`

```text
https://raw.githubusercontent.com/Hy360032/my-symedia-rule/refs/heads/main/custom_rendering_words.txt
```

52 条。编码与画质归一、音轨归一、季集重映射。

### 自定义捕获组 → `custom_capturing_group.txt`

```text
https://raw.githubusercontent.com/Hy360032/my-symedia-rule/refs/heads/main/custom_capturing_group.txt
```

2 条。发行地区 `production_country`、内容版本 `edition`。

填好后把「规则自动更新」的 cron 留着（默认 `30 2 * * *`），之后每天自动拉取。

## 文件与配置项对照

| 文件 | 对应子标签 | 后端字段 | 条数 |
|---|---|---|---|
| `custom_words.txt` | 自定义识别词 | `keyword_links` | 180 |
| `custom_group.txt` | 自定义制作组 | `release_group_links` | 402 |
| `custom_rendering_words.txt` | 自定义渲染词 | `render_word_links` | 52 |
| `custom_capturing_group.txt` | 自定义捕获组 | `capturing_group_links` | 2 |

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

注释用 `#` 开头，不参与匹配。所有文件都是一行一条规则，别在一行里塞多条。

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
