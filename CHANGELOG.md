# 更新日志

## 2026-10-24 首次发布

### 规则导入

| 提交类型 | 内容 | 文件 | 条数 |
|---|---|---|---|
| feat | 导入自定义识别词 | `custom_words.txt` | 180 |
| feat | 导入自定义制作组 | `custom_group.txt` | 402 |
| feat | 导入自定义渲染词 | `custom_rendering_words.txt` | 52 |
| feat | 导入自定义捕获组 | `custom_capturing_group.txt` | 2 |

合计 636 条有效规则。

### 修复

- `fix` 修正「奥美迦奥特曼」识别词中的替换字符乱码（U+FFFD）→ `custom_words.txt`

### 文档

- `docs` 订阅地址按四个子标签拆分，附文件与后端字段对照表 → `README.md`

### 基建

- `feat` 加入 `.gitattributes` 锁定 LF 换行、`LICENSE`（MIT）、`.gitignore`
