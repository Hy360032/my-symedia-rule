# Symedia 自定义规则 · 个人版

整理自个人 Symedia 实例（`归档设置 → 辅助识别`）的识别规则，共 **637 条有效规则**。

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

403 条。流媒体平台、压制组、字幕组、RAW 源。

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

### 拉不动 raw 怎么办

国内网络直连 `raw.githubusercontent.com` 会间歇性报 `SSL: UNEXPECTED_EOF_WHILE_READING`，连不上时换反代前缀即可，路径原样接在后面：

```text
https://ghfast.top/https://raw.githubusercontent.com/Hy360032/my-symedia-rule/refs/heads/main/custom_words.txt
```

四个子标签都按这个办法加前缀。备选：`https://gh-proxy.com/`、`https://ghproxy.net/`；`cdn.jsdelivr.net/gh/Hy360032/my-symedia-rule@main/custom_words.txt` 也能用，但有约 12 小时缓存，刚推的改动不会立刻生效。

## 二级分类规则 → `mt_category.yaml`

这一份不走「远程链接」，需要手动粘贴。

在「归档设置 → 二级分类」里，把 `mt_category.yaml` 的全部内容整体覆盖进去。

```text
https://raw.githubusercontent.com/Hy360032/my-symedia-rule/refs/heads/main/mt_category.yaml
```

电影 6 类、剧集 8 类，共 14 个分类，按顺序自上而下匹配。

### 转载版 → `mt_category-ccdccf-v2.1.2.yaml`

作者 `ccdccf@爱影`，比自用版细致得多：54 个分类（电影 27 + 剧集 27），三级路径（如 `电影/华语电影/大陆地区电影`），额外支持 `year`、`series_keywords`、`series_actors` 字段。

```text
https://raw.githubusercontent.com/Hy360032/my-symedia-rule/refs/heads/main/mt_category-ccdccf-v2.1.2.yaml
```

**前提**：Symedia 版本需高于 `v1.0.52.20`。
两份二选一粘贴，不要混用。

## 自定义通知模板 → `notify-*.j2`

这两份也不走订阅，需要手动粘贴。位置在「工具箱 → 自定义通知模板」，两个通道各一个文本框，别混填。

粘贴时整份文件内容原样贴进去即可（`title` 与 `text` 两个键都在里面），这两份是配置文本而非纯 Jinja2 模板，所以用 `.txt`。

### 归档通知 → `notify-transfer_task-symedia.txt`

```text
https://raw.githubusercontent.com/Hy360032/my-symedia-rule/refs/heads/main/notify-transfer_task-symedia.txt
```

现网在用版本 v2.3，正文 10884 字。入库一条通知依次给：标题、评分、媒体类型、归类、质量、规格、文件数、大小、TMDB ID、发布组、用时、简介、TMDB/豆瓣/IMDb 三行外链，最后一句评语。

评语按分辨率、来源、色彩、体积、速度、评分分档；字段为空的行整行不输出。

### Emby 通知 → `notify-emby_mediamsg-symedia.txt`

```text
https://raw.githubusercontent.com/Hy360032/my-symedia-rule/refs/heads/main/notify-emby_mediamsg-symedia.txt
```

现网在用版本 v2，正文 5157 字。按事件分流：新入库、开始播放、停止播放、登录成功、登录失败、标记了、测试。播放类另带进度、来源 IP、播放设备、用户。

外链同样各占一行，无链接时整块不输出。

## 文件与配置项对照

| 文件 | 对应位置 | 后端字段 | 条数 |
|---|---|---|---|
| `custom_words.txt` | 自定义识别词 | `keyword_links` | 180 |
| `custom_group.txt` | 自定义制作组 | `release_group_links` | 403 |
| `custom_rendering_words.txt` | 自定义渲染词 | `render_word_links` | 52 |
| `custom_capturing_group.txt` | 自定义捕获组 | `capturing_group_links` | 2 |
| `mt_category.yaml` | 二级分类（自用版） | 手动粘贴 | 14 个分类 |
| `mt_category-ccdccf-v2.1.2.yaml` | 二级分类（转载版） | 手动粘贴 | 54 个分类 |
| `notify-transfer_task-symedia.txt` | 自定义通知模板（归档） | `transfer_task` | 10884 字 |
| `notify-emby_mediamsg-symedia.txt` | 自定义通知模板（Emby） | `emby_mediamsg` | 5157 字 |

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
