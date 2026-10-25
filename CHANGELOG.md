# 更新日志

## 2026-10-25 通知模板

| 提交类型 | 说明 | 文件 | 字数 |
|---|---|---|---|
| feat | 首次导出 Symedia 归档通知模板 | `notify-transfer_task-symedia-v2.3.j2` | 10884 |
| feat | 首次导出 Symedia Emby 通知模板 | `notify-emby_mediamsg-symedia-v2.j2` | 5157 |
| docs | README 补通知模板两个通道、订阅说明与字段对照 | `README.md` | — |

两份均为现网在用的版本，行尾 LF，与 Symedia「自定义通知模板」里的配置逐字一致。

## 2026-10-24 首次发布

### 规则导入

| 提交类型 | 说明 | 文件 | 条数 |
|---|---|---|---|
| feat | 首次导出 Symedia 自定义识别词 | `custom_words.txt` | 180 |
| feat | 首次导出 Symedia 自定义制作组 | `custom_group.txt` | 402 |
| feat | 首次导出 Symedia 自定义渲染词 | `custom_rendering_words.txt` | 52 |
| feat | 首次导出 Symedia 自定义捕获组 | `custom_capturing_group.txt` | 2 |

合计 636 条有效规则。

### 修复

- `fix` 修正「奥美迦奥特曼」识别词中的替换字符乱码（U+FFFD）→ `custom_words.txt`

### 文档

- `docs` 订阅地址按四个子标签拆分，附文件与后端字段对照表 → `README.md`

### 新增

- `feat` 新增二级分类规则 `mt_category.yaml`，电影 6 类、剧集 8 类，共 14 个分类
- `feat` 收录转载版二级分类规则 `mt_category-ccdccf-v2.1.2.yaml`（作者 ccdccf@爱影，54 个分类，行尾统一为 LF）

### 基建

- `feat` 首次导出时一并加入 `.gitattributes` 锁定 LF 换行、`LICENSE`（MIT）、`.gitignore`
