# AI Experience Log 📝

> 边用 AI 干活边记录，积累素材后一键出稿

这是一个 **Claude Code Skill**，让 AI 自动识别对话中的「有料瞬间」并记录下来，最后一键生成公众号文章。

**适合谁用？**
- 经常用 Claude Code 干活的人
- 想记录 AI 使用心得但懒得手动记的人
- 想把踩坑/发现/技巧写成文章分享的人

---

## ✨ 功能一览

| 功能 | 说明 |
|------|------|
| 🤖 自动记录 | AI 识别踩坑、发现、迭代、搞笑、突破等瞬间，自动记录 |
| ✍️ 手动补充 | 说「记一笔：xxx」手动添加素材 |
| 📄 一键出稿 | 说「出稿」生成 1000 字左右的文章 |
| 🎨 自动排版 | 生成公众号可用的 HTML，全选复制粘贴即可 |
| 🖼️ 封面图提示词 | 基于标题关键词生成 Gemini 友好的头图提示词 |

---

## 🚀 快速开始（5分钟上手）

### 第一步：复制 Skill 文件

```bash
# 克隆仓库
git clone https://github.com/OrangeViolin/ai-experience-log.git

# 复制 skill 到 Claude Code 的 skills 目录
cp -r ai-experience-log/skill/story-logger ~/.claude/skills/
```

### 第二步：创建素材存储目录

在你想存放素材的位置创建目录：

```bash
# 示例：在你的项目目录下创建
mkdir -p ~/my-project/ai-notes/drafts
```

### 第三步：修改存储路径

打开 `~/.claude/skills/story-logger/SKILL.md`，找到「存储位置」部分，改成你自己的路径：

```markdown
## 存储位置

所有素材和产出统一存放在：
/Users/你的用户名/my-project/ai-notes/
├── drafts/
│   └── current.json    # 当前素材列表
├── [文章标题].md        # 产出的文章
└── [文章标题]_公众号.html  # 排版后的公众号格式
```

### 第四步：初始化素材文件

```bash
# 创建空的素材文件
echo '{"topic":"","materials":[],"created":"'$(date +%Y-%m-%d)'"}' > ~/my-project/ai-notes/drafts/current.json
```

### 第五步：开始使用

打开 Claude Code，正常干活就行！

---

## 📖 使用指南

### 自动记录（默认开启）

正常跟 AI 干活，遇到这些情况会自动记录：

| 类型 | 识别信号 | 示例 |
|-----|---------|------|
| 🐛 踩坑翻车 | 预期≠结果、报错、折腾半天 | "试了三种方案都不行" |
| 💡 意外发现 | "没想到"、"原来可以" | "居然这样就解决了" |
| 🔄 迭代打磨 | 改了多版、从复杂到简洁 | "200行改成20行还能跑" |
| 😂 搞笑时刻 | AI 抽风、神奇 bug | "它认真地给我写了一堆错的" |
| ✨ 突破时刻 | 卡了很久终于通 | "困扰一周的bug终于找到了" |
| 🎯 方法沉淀 | 可复用的技巧 | "以后遇到这种情况就这么办" |

记录时**不打断对话**，段落结尾会标记 `（✓ 素材+1）`

### 手动记录

```
记一笔：刚让 Claude 写了 200 行，我说太长，它改成 20 行还能跑
```

或

```
素材+1：发现 Whisper 的 medium 模型比 tiny 准确太多了
```

### 查看素材

```
看看素材
```

或

```
/story
```

### 出稿

```
出稿
```

AI 会：
1. 读取所有素材
2. 分析素材，提炼主题和故事线
3. 写一篇 1000 字左右的文章
4. 生成公众号排版 HTML（自动打开浏览器预览）
5. 输出封面图提示词（复制到 Gemini 生成头图）
6. 询问是否清空当前素材

### 清空素材

```
清空素材
```

---

## 🎨 排版功能（v2 新增）

出稿后会自动调用排版工具，生成公众号可用的 HTML。

**使用流程：**
1. 说「出稿」
2. 浏览器自动打开预览
3. `Cmd+A` 全选，`Cmd+C` 复制
4. 到公众号编辑器 `Cmd+V` 粘贴
5. 完成！

**支持的主题：**
| 主题 | 风格 |
|------|------|
| apple | 极简优雅，技术文章首选 |
| bytedance | 简洁现代，科技感强 |
| cyber | 赛博朋克，个性十足 |

---

## 🖼️ 头图生成（v2 新增）

出稿后会自动生成 Gemini 友好的头图提示词。

**流程：**
```
标题 → 提取关键词 → 翻译英文 → 生成 Gemini 提示词
```

**示例：**

标题：`Agent不像机器，Agent像人，管理Agent也是一门艺术`

生成的提示词：
```
Create a WeChat article cover image (16:9 aspect ratio).

**Title Keywords**: Agent, Human-like, Machine, Management

**Visual Requirements**:
- Main subject: Split composition - left side shows a cold mechanical robot head, right side shows a warm human head silhouette...
- Text overlay: "Agent像人" in bold white Chinese characters, centered
- Style: Modern tech illustration, clean and minimalist
...
```

复制到 Gemini 即可生成头图。

---

## ✍️ 文章风格

**人设：极客朋友** —— 硬核但说人话的技术玩家

| 特点 | 说明 |
|------|------|
| 硬核但通俗 | 用大白话讲明白技术的事 |
| 信息密度高 | 每句话都有信息量，不灌水 |
| 节奏明快 | 短句为主，偶尔长句拉节奏 |
| 真实感 | 会说"丑哭了""折腾了两小时"，不端着 |
| 有态度 | 会说"这个设计有问题""这才是正确的用法" |

**禁忌：**
- ❌ 不说"笔者""本文将介绍"这种书面语
- ❌ 不堆砌专业术语装逼
- ❌ 不写空洞的感慨和鸡汤
- ❌ 不用"震惊""竟然"这种营销号词

---

## 📁 目录结构

```
.
├── README.md                 # 你正在看的文件
├── drafts/
│   ├── current.json          # 当前素材
│   └── [日期]-[主题].json    # 历史素材归档
├── skill/
│   └── story-logger/
│       └── SKILL.md          # Skill 定义文件（核心）
├── *.md                      # 产出的文章（Markdown）
└── *_公众号.html             # 排版后的公众号格式
```

---

## 🤔 常见问题

### Q: 为什么 AI 没有自动记录？

A: 检查几个地方：
1. Skill 文件是否正确复制到 `~/.claude/skills/story-logger/`
2. 存储路径是否正确配置
3. `drafts/current.json` 文件是否存在

### Q: 可以自定义记录的类型吗？

A: 可以。打开 `SKILL.md`，修改「触发条件」表格即可。

### Q: 排版功能需要额外配置吗？

A: 需要安装排版工具。参考 [md2wechat](https://www.md2wechat.cn/) 获取 API Key。

### Q: 可以不用排版功能吗？

A: 可以。出稿时只生成 Markdown 文件，你可以用其他工具排版。

---

## 🌟 Learn in Public

这个仓库本身就是 **Learn in Public** 的实践。

我会把用 AI 干活的过程记录下来，积累素材后出稿，同步到这里和公众号。

**已产出的文章：**
- Agent不像机器，Agent像人，管理Agent也是一门艺术
- 半小时，我用AI给自己造了个素材记录器
- 让AI帮我选电脑，我发现了一个重要趋势
- ...

---

## 🤝 贡献

欢迎 Star、Fork、提 Issue！

如果你有好的想法，欢迎提 PR。

---

## 📜 License

MIT

---

## 🔗 相关链接

- [Claude Code 官方文档](https://docs.anthropic.com/claude-code)
- [md2wechat 排版工具](https://www.md2wechat.cn/)
- [Gemini 生图](https://gemini.google.com/)

---

*Made with ❤️ and Claude Code*
