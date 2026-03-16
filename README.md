# bb-agent

**Let any LLM automate the real web.** Including the cheap ones.

bb-agent is an AI agent that uses [bb-browser](https://github.com/epiral/bb-browser) site adapters to interact with real websites — Twitter, Bilibili, Xiaohongshu, Douban, Reddit, YouTube, and [90+ more](https://github.com/epiral/bb-sites). No scraping, no Puppeteer, no screenshots. Just CLI commands that return structured JSON.

bb-agent 是一个基于 [bb-browser](https://github.com/epiral/bb-browser) site adapter 的 AI Agent。通过 CLI 操作真实网站，不需要写爬虫，不需要截图识别，不需要 Puppeteer。一行命令，结构化 JSON 返回。

## Why / 为什么做这个

There's a dirty secret about AI agents today: **most of them need Opus/GPT-5 tier models to do anything useful on the web.** Because "using a website" actually means writing code — reverse-engineering APIs, handling auth, parsing responses. That's senior-developer-level work.

现在 AI Agent 有一个大家不太说的事实：**大部分 Agent 要在网上做点实际的事，需要 Opus/GPT-5 级别的模型。** 因为"使用一个网站"其实意味着写代码，逆向 API、处理认证、解析响应。这是高级开发的活。

bb-browser's site adapters change this equation:

bb-browser 的 site adapter 改变了这个等式：

```
Before / 之前:
  Agent + Opus → (write code to call Twitter API) → get tweets

After / 之后:
  Agent + any model → bb-browser site twitter/search "query" → get tweets
```

**The intelligence requirement drops from "senior developer" to "CLI boy".**

**对模型的智力要求从"高级开发"降到了"会用命令行"。**

This means Qwen, GLM, DeepSeek, Doubao — or any model that can string together a few CLI commands — can now do what previously required frontier models. Use expensive models to BUILD the adapters. Use cheap models to RUN them.

这意味着通义千问、智谱、DeepSeek、豆包，或者任何能拼几个 CLI 命令的模型，现在都能干之前只有顶级模型才能干的事。用贵的模型来造 adapter，用便宜的模型来跑任务。

## What it can do / 能做什么

With 95 adapters across 35+ platforms, bb-agent can:

基于 35+ 平台的 95 个 adapter，bb-agent 可以：

- **Cross-platform intelligence** — Search Twitter, check Xiaohongshu, read Reddit, summarize YouTube, all in one workflow
- **Social graph analysis** — Follow chains, find key people, map relationships
- **Content monitoring** — Track keywords across platforms, aggregate sentiment
- **Research automation** — Collect, compare, and synthesize information from multiple sources

- **跨平台情报** — 搜推特、查小红书、读 Reddit、总结 YouTube，一个工作流搞定
- **社交图谱分析** — 追踪关注链，找关键人物，画关系图
- **内容监控** — 跨平台关键词追踪，舆情聚合
- **调研自动化** — 从多个信息源收集、对比、综合信息

## Architecture / 架构

```
bb-agent (orchestrator, any LLM)
    │
    ├── bb-browser site twitter/search "query"    → JSON
    ├── bb-browser site twitter/following user     → JSON
    ├── bb-browser site bilibili/search "query"   → JSON
    ├── bb-browser site xiaohongshu/search "query" → JSON
    ├── bb-browser site youtube/search "query"     → JSON
    │         ...95 adapters across 35 platforms
    │
    ▼
  Structured results → LLM reasoning → next action
```

The key insight: **the browser is already logged in.** bb-browser runs in your Chrome with your cookies, your sessions, your auth. No API keys, no OAuth flows, no rate limit BS. The adapter runs JS in the page context — it IS the page.

核心洞察：**浏览器已经登录了。** bb-browser 运行在你的 Chrome 里，用你的 cookie、你的会话、你的登录态。不需要 API key，不需要 OAuth，没有频率限制的破事。adapter 在页面上下文里运行 JS，它就是页面本身。

## Status / 状态

Early stage. Building in public.

早期阶段，公开构建中。

## Related / 相关项目

- [bb-browser](https://github.com/epiral/bb-browser) — The browser automation CLI that powers everything
- [bb-sites](https://github.com/epiral/bb-sites) — Community-maintained site adapters (95 adapters, 35+ platforms)

## License

MIT
