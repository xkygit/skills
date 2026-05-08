---
name: kingdee-fetch
description: "从金蝶知识库 API 抓取文章并转换为 Markdown。传入知识文章 ID 或 URL，自动调用 API 获取内容，将 HTML 正文转为干净的 Markdown，图片 URL 补全为绝对路径。适用于知识文章（/knowledge/），不支持直播课程（/school/liveCourse/）。"
---

# 金蝶知识库文章抓取

使用 `可转移工具/kingdee-fetch.py` 从金蝶知识库抓取文章并转 Markdown。

## 命令

```bash
python "可转移工具/kingdee-fetch.py" <知识文章ID或URL> [输出文件]
```

- 参数1：金蝶知识文章的数字 ID（19位左右）或完整 URL，脚本会自动提取 ID
- 参数2（可选）：输出文件路径，不传则打印到 stdout

## 功能

- 从 `https://vip.kingdee.com/knowledgeapi/knowledge/{id}` JSON API 获取文章
- HTML 正文自动转换为 Markdown（标题、段落、代码块、链接、图片、加粗）
- 图片相对路径 `/download/...` 自动补全为 `https://vip.kingdee.com/download/...`
- 输出含 YAML frontmatter（标题、作者、标签、分类、浏览/收藏数据）
- 正文末尾列出所有图片链接汇总

## 使用示例

```bash
# 用 URL 抓取
python "可转移工具/kingdee-fetch.py" "https://vip.kingdee.com/knowledge/657296265494963968"

# 用纯 ID 抓取并保存
python "可转移工具/kingdee-fetch.py" "657296265494963968" "文章输出.md"
```

## 限制

- **仅支持知识文章**（`/knowledge/` 路径），直播课程（`/school/liveCourse/`）没有 JSON API，无法抓取正文
- 依赖 Python 3 标准库（`json`, `re`, `urllib`），无需额外安装
