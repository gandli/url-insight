---
name: url-insight
description: "Auto-analyze URLs shared in conversation. Triggers when user sends a message containing one or more HTTP/HTTPS URLs without other instructions. Fetches content, generates structured summary, and provides personalized next-step recommendations based on user context (USER.md background). Use for: link analysis, article summarization, tool/project evaluation, tech discovery review."
metadata: { "openclaw": { "emoji": "🔗" } }
---

# URL Insight

When the user sends a URL (with no other instruction), automatically analyze it.

## Workflow

1. **Detect**: Message contains URL(s) and no explicit question/command
2. **Fetch**: Use `web_fetch` to extract page content (markdown mode, maxChars=8000)
3. **Read context**: Load `USER.md` for user background (skip if unavailable)
4. **Analyze & respond** with this structure:

## Output Format

```
📌 **{页面标题}**

> {一句话摘要，30字以内}

**📝 内容概要**
{3-5个要点，bullet list}

**🔍 关键信息**
- 类型：{文章/工具/项目/产品/论文/新闻}
- 技术栈：{如适用}
- 作者/来源：{如有}

**💡 对老板的建议**
{结合 USER.md 中的背景信息，给出 1-3 条具体的下一步行动建议}

🔗 {原始URL}
```

## Rules

- If URL is unreachable, say so and suggest alternatives (archive.org, Google cache)
- For GitHub repos: focus on stars, language, last update, README highlights
- For news/articles: focus on core argument and implications
- For tools/products: focus on features, pricing, alternatives
- Multiple URLs: analyze each one separately
- Language: match user's language (default Chinese)
- Keep total response under 300 words per URL
- The "对老板的建议" section is the key differentiator — make it specific and actionable based on user's projects and interests
