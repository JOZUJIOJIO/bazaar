# Bazaar

**给 AI Agent 用的 GitHub 原生技能市场。**

不需要后端。不需要邀请码。不需要装 npm 包。只要有 `gh` CLI 就行。

---

## 为什么做这个？

AI Agent 需要技能——可复用的工作流、MCP 服务器、自动化脚本。但现在的技能市场都要求你：

- 信任一个第三方后端服务器
- 求人要一个邀请码
- 装一个 npm 包增加依赖
- 在又一个平台注册账号

你的技能本来就在 GitHub 上。为什么发现和分发还需要中间商？

## 解决方案

Bazaar 用一个极简约定把 GitHub 变成技能市场：

> **任何打了 `claude-skill` topic 的 repo，就是一个可发现的技能。**

没了。不需要新平台、新账号、新依赖。你的 `gh` CLI 已经登录了——Bazaar 已经可以用了。

## 你能做什么

| 命令 | 做什么 |
|------|--------|
| `bazaar search "爬虫"` | 在整个 GitHub 搜索技能 |
| `bazaar feed` | 浏览最新发布的技能 |
| `bazaar view owner/repo` | 远程读取一个技能的完整 SKILL.md |
| `bazaar install owner/repo` | 一条命令安装到 `~/.claude/skills/` |
| `bazaar publish ./my-skill` | 把你的技能发布到 GitHub |
| `bazaar follow username` | 关注一个技能发布者 |
| `bazaar notifications` | 查看关注的人最近发了什么 |
| `bazaar steal <url>` | 把任何网页变成技能脚手架 |

## 真实场景：它到底有什么用？

### 场景一：你想给 Claude 加一个文生图能力

以前的做法：Google 搜「Claude Code image generation」→ 翻 5 篇文章 → 手动配 API → 写 prompt → 调试半天。

**有了 Bazaar：**

```bash
bazaar search "image generation"
# 找到一个用 Gemini 做图的 skill，看看详情
bazaar view vfxengine/nano-banana-2-skill
# 不错，装上
bazaar install vfxengine/nano-banana-2-skill
```

三条命令，Claude 就会画画了。

---

### 场景二：你写了一套小红书爆款文案流程，想分享给朋友

以前的做法：打包文件 → 发微信 → 对方不知道放哪 → 教他怎么配置 → 来回折腾一下午。

**有了 Bazaar：**

```bash
bazaar publish ./xhs-writing-coach --tags content,xiaohongshu
```

一条命令发布。告诉朋友：

```bash
bazaar install yourname/xhs-writing-coach
```

一条命令安装。完事。

---

### 场景三：你刷到一篇很牛的 AI 工作流文章，想变成自己的工具

以前的做法：收藏链接 → 过两天忘了 → 再也没用过。

**有了 Bazaar：**

```bash
bazaar steal https://example.com/awesome-ai-workflow
# Claude 自动读取文章内容，生成一个 skill 脚手架
# 你稍微改改，然后发布：
bazaar publish ./my-new-skill --tags automation
```

从「收藏吃灰」变成「可执行的工具」，整个过程 5 分钟。

---

## 快速上手

### 1. 确认 `gh` 已登录

```bash
gh auth status
```

### 2. 搜索技能

```bash
bazaar search "browser automation"
```

### 3. 安装一个

```bash
bazaar install oaustegard/claude-skills
```

### 4. 发布你自己的

```bash
bazaar publish ./my-awesome-skill --tags automation,workflow
```

搞定。你的技能现在全球可搜。

## 工作原理

```
你                            GitHub
 |                              |
 |  bazaar search "X"           |
 |  ────────────────────────>   |  gh search repos --topic claude-skill
 |                              |
 |  bazaar install user/repo    |
 |  ────────────────────────>   |  gh repo clone (depth 1)
 |                              |  去掉 .git → 纯技能目录
 |                              |
 |  bazaar publish ./skill      |
 |  ────────────────────────>   |  gh repo create + 设置 topic
 |                              |  git push
 |                              |
 |  bazaar follow user          |
 |  (本地 ~/.bazaar/)           |  不需要 API 调用
 |                              |
 |  bazaar notifications        |
 |  ────────────────────────>   |  gh search repos user:X --topic claude-skill
```

没有中间件。没有代理。没有第三方服务器碰你的数据。

## 发布约定

让你的技能被发现，只需要给 GitHub repo 加上 `claude-skill` topic。就这一个要求。

推荐的 repo 结构：

```
my-skill/
├── SKILL.md          # 必须 — 主指令文件，带 YAML frontmatter
├── references/       # 可选 — 深度文档
├── templates/        # 可选 — 可复用模板
└── scripts/          # 可选 — 辅助脚本
```

SKILL.md 头部格式：

```yaml
---
name: my-skill-name
description: 这个技能做什么，什么时候用。
---
```

## 偷师 → 改造 → 发布

看到别人博客上的好方法？变成技能：

```bash
bazaar steal https://example.com/cool-workflow
# Claude 读取内容，生成技能脚手架
# 你修改完善，然后：
bazaar publish ./new-skill --tags automation
```

标注出处：`<!-- remixed from https://original-source -->`

## 设计哲学

- **GitHub 就是后端。** 已经存在的东西不要重复造。
- **Topic 就是协议。** 一个标签（`claude-skill`）= 全球可发现。
- **本地优先。** 关注列表、安装记录——全在你自己机器上。
- **零信任依赖。** 没有平台拥有你的数据或你的分发渠道。
- **约定大于基建。** 一个共享命名约定胜过一套自建 API。

## 系统要求

- `gh` CLI 已安装并登录
- 没了。

## 版本

0.1.0 — 首次发布。

---

*为那些相信「最好的市场不需要服务器」的 Agent 而造。*
