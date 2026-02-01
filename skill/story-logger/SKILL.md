---
name: story-logger
description: AI搞事情素材收集器。cc 自动识别有料瞬间并记录，说"出稿"生成文章+排版+封面图提示词。
---

# 素材收集器

边干活边记录，最后出一篇朋友聊天式的硬核短文。

---

## 存储位置

所有素材和产出统一存放在：
```
/Users/mac/Documents/mycc/2-Projects/项目1：01fish-assistant/使用ai过程记录/
├── drafts/
│   └── current.json    # 当前素材列表
│   └── [日期]-[主题].json  # 历史素材归档
├── [文章标题].md        # 产出的文章
└── [文章标题]_公众号.html  # 排版后的公众号格式
```

---

## 工作模式

### 模式一：自动记录（默认开启）

cc 会在对话中**主动识别有料的瞬间**并自动记录，无需手动触发。

**触发条件：**

| 类型 | 识别信号 | 示例 |
|-----|---------|------|
| 🐛 踩坑翻车 | 预期≠结果、报错、折腾半天 | "试了三种方案都不行" |
| 💡 意外发现 | "没想到"、"原来可以"、意外有效 | "居然这样就解决了" |
| 🔄 迭代打磨 | 改了多版、从长变短、从复杂到简洁 | "200行改成20行还能跑" |
| 😂 搞笑时刻 | 对话金句、AI抽风、神奇bug | "它认真地给我写了一堆错的" |
| ✨ 突破时刻 | 卡了很久终于通、长期问题解决 | "困扰一周的bug终于找到了" |
| 🎯 方法沉淀 | 可复用的技巧、工作流、心得 | "以后遇到这种情况就这么办" |

**自动记录时**：不打断对话，段落结尾标记 `（✓ 素材+1）`

### 模式二：手动记录

用户主动说"记一笔：xxx"时记录。

---

## 触发词

**查看/管理素材：**
- "/story" - 查看当前素材状态
- "看看素材" - 查看已记录的素材
- "出稿" - 生成文章+排版+封面图
- "清空素材" - 清空当前素材

**手动补充：**
- "记一笔：xxx" - 手动添加素材
- "素材+1：xxx" - 手动添加素材

---

## current.json 格式

```json
{
  "topic": "主题（可选，出稿时自动提取）",
  "materials": [
    {
      "time": "2026-01-30 14:30",
      "content": "让Claude改了三轮，每轮都说'已经完美了'，结果每轮都还能挑出毛病",
      "type": "😂 搞笑时刻",
      "context": "可选的上下文备注",
      "auto": true
    }
  ],
  "created": "2026-01-30"
}
```

---

## 出稿流程

```
素材积累 → 说"出稿" → 写文章 → 排版HTML → 生成头图提示词 → 完成
```

### 步骤

1. 读取所有素材
2. 分析素材，提炼主题和故事线
3. 按写作规范写文章
4. 保存 Markdown 文件
5. **调用排版工具生成公众号 HTML**
6. **基于标题关键词生成头图提示词**
7. 询问是否清空当前素材

---

## 写作规范

### 人设：极客朋友

一个硬核但说人话的技术玩家。

**核心特质：**
- 真的在用这些工具，不是云评测
- 懂技术原理，但不掉书袋
- 会踩坑，也会分享怎么爬出来
- 有观点，敢下判断

**语言风格：**
- **硬核但通俗**：用大白话讲明白技术的事
- **信息密度高**：每句话都有信息量，不灌水
- **节奏明快**：短句为主，偶尔长句拉节奏
- **真实感**：会说"丑哭了""折腾了两小时"，不端着
- **有态度**：会说"这个设计有问题""这才是正确的用法"

**结构偏好：**
- 先说结论/判断
- 再讲过程/故事
- 提炼方法论/洞察
- 给出下一步/建议

**禁忌：**
- 不说"笔者""本文将介绍"这种书面语
- 不堆砌专业术语装逼
- 不写空洞的感慨和鸡汤
- 不用"震惊""竟然"这种营销号词

### 文章格式

- 标题：吸引人（发现/反常识/有趣现象）
- 正文：1000 字左右，高信息密度
- 开头直接切入，不要"今天我要分享"
- 用分割线 `---` 分段
- 小标题简短有趣
- 结尾给可复制的方法

**结构模板：**

```markdown
# 标题

开头：直接说事，不铺垫

---

## 小标题1
故事/发现/操作过程

---

## 小标题2
更深入的发现/转折/意外

---

## 为什么有效 / 原理
简短分析

---

## 怎么复制
1. xxx
2. xxx
3. xxx

---

*（可选的结尾备注）*
```

---

## 排版配置

写完文章后自动调用 md2wechat API 进行排版。

### 排版命令

```bash
cd "/Users/mac/Documents/mycc/2-Projects/项目1：01fish-assistant/公众号工具流/md-formatter"
python3 md2wechat_formatter.py [文章路径] --theme [主题] --font-size [字号]
```

### 推荐主题

| 主题 | 参数 | 适用场景 |
| --- | --- | --- |
| 苹果范 | `apple` | 极简优雅，技术文章首选 |
| 字节范 | `bytedance` | 简洁现代，科技感强 |
| 赛博朋克 | `cyber` | 未来科幻，个性十足 |

### 推荐字号

- `medium` - 中等 (15px) 默认
- `large` - 大号 (16px) 长文推荐

### 排版输出

排版完成后：
1. 生成 `[文章标题]_公众号.html` 文件
2. 自动用浏览器打开预览
3. 用户全选复制粘贴到公众号即可

---

## 头图生成规范

### 流程

```
标题 → 提取关键词 → 翻译成英文 → 生成 Gemini 提示词
```

### 关键词提取规则

从标题中识别：
1. **核心主题词**：如 Agent、操作系统、Claude、Whisper
2. **情感/动作词**：如 踩坑、发现、突破、死机
3. **对比/冲突词**：如 像人vs像机器、死的vs活的

### Gemini 头图提示词模板

```
Create a WeChat article cover image (16:9 aspect ratio).

**Title Keywords**: [从标题提取的2-3个核心关键词，英文]

**Visual Requirements**:
- Main subject: [基于关键词的视觉主体]
- Text overlay: "[标题中最核心的短语，中文]" in bold, centered, white or bright color
- Style: Modern tech illustration, clean and minimalist
- Color scheme: [根据主题选择配色]
- Mood: [根据文章基调选择氛围]

**Technical specs**:
- Aspect ratio: 16:9 (recommended 900x500px)
- Background: Gradient or solid, not too busy
- Text must be clearly readable
- Leave space for WeChat cropping
```

### 配色参考

| 主题类型 | 推荐配色 |
|---------|---------|
| 技术/工具 | 深蓝+青色渐变 |
| AI/未来 | 紫色+粉色渐变 |
| 踩坑/问题 | 深灰+橙色点缀 |
| 突破/成功 | 绿色+金色点缀 |
| 对比/冲突 | 左右分屏冷暖对比 |

### 示例

**标题**：Agent不像机器，Agent像人，管理Agent也是一门艺术

**提取关键词**：Agent, human-like, management

**生成的提示词**：

```
Create a WeChat article cover image (16:9 aspect ratio).

**Title Keywords**: Agent, Human, AI Management

**Visual Requirements**:
- Main subject: Split composition - left side shows a warm human brain silhouette, right side shows a cool-toned AI/robot brain, connected by glowing neural pathways
- Text overlay: "Agent像人" in bold, centered, white color with subtle glow
- Style: Modern tech illustration, clean and minimalist
- Color scheme: Left warm orange/flesh tones, right electric blue/cyan, golden connections
- Mood: Thoughtful, insightful, balanced

**Technical specs**:
- Aspect ratio: 16:9 (900x500px)
- Background: Dark gradient from warm to cool
- Text must be clearly readable
- Leave space for WeChat cropping
```

---

## 示例对话

### 自动记录

**对话中...**

用户：这个 bug 搞了一下午，最后发现是少了个分号

cc：找到了，`config.ts:42` 行末少了分号。已修复。（✓ 素材+1）

---

### 出稿

**用户**：出稿

**cc**：
好，素材整理完毕，开始出稿...

[写文章并保存为 Markdown]
[调用排版工具生成 HTML]
[浏览器打开预览]

文章已保存：`xxx.md`
排版预览：`xxx_公众号.html`（浏览器已打开）

---

**头图提示词（Gemini）**：

```
Create a WeChat article cover image...
[完整提示词]
```

复制到 Gemini 生成头图即可。

---

要清空当前素材吗？

---

## 方案设计过程

> 这个 skill 是如何诞生的

**需求**：用户希望 cc 能主动帮忙记录干活过程中的有料瞬间，不用每次手动喊"记一笔"。

**方案**：三层主动记录机制

1. **实时感知**：在 CLAUDE.md 中定义「素材嗅觉」规则，cc 在对话中自动识别 6 种有料信号
2. **会话收尾**：通过 Stop hook，对话结束时提醒素材数量
3. **每日沉淀**：在 status.md 中增加「今日素材」区块

**v2 升级（2026-02-01）**：
- 整合排版功能：出稿后自动调用 md2wechat API 生成公众号 HTML
- 规范头图生成：从标题提取关键词，生成 Gemini 友好的详细提示词
