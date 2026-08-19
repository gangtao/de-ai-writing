# de-ai-writing

把十个开源"去 AI 味"项目的思路合成一个 skill。**一个技能，六个入口**——共用一套引擎，但不同用途的改写尺度分开定义。

## 为什么要分入口

博客里的口语化，放进故障报告是灾难；技术文档里的被动语态和术语重复是准确，不是 AI 味。大多数去 AI 味工具只有一套规则，用在正式文档上会把有信息量的句子改成"贼快，直接起飞"。

所以这里把"改到什么程度算对"按用途拆开：

| 入口 | 用途 | 声音层力度 | 及格线 |
|---|---|---|---|
| **A 体检** | 只诊断打分，不改稿 | — | — |
| **B 内容稿** | 博客、公众号、发布说明、演讲稿、社媒 | 全开 | 85 |
| **C 工作沟通** | 邮件、周报、客户回复、Slack、PR 描述 | 收着用 | 80 |
| **D 正式文档** | 技术文档、RCA、白皮书、公告、论文摘要 | 几乎关闭 | 80 |
| **E 对齐我的声音** | 有个人样本时叠加 | 按指纹 | — |
| **F 从零起草** | 手上没稿子时叠加 | 按底层入口 | — |

E 和 F 是叠加项，不是替代。"按我的风格帮我写一篇发布说明" = F + E + B。

## 共用引擎

三遍改写法：信息层（删空话、补事实）→ 句子层（破节奏）→ 声音层（注入人味，力度由入口决定），然后按入口权重打分，不到及格线自己再改一轮。

## 结构

```
de-ai-writing/
├── SKILL.md                    # 入口路由 + 三遍改写法 + 排版 + 打分
└── references/
    ├── genres.md               # 六个入口的尺度、红线、评分权重（B/C/D 前必读）
    ├── patterns-zh.md          # 中文痕迹全表 + 高频词替换 + 误判防护
    ├── patterns-en.md          # 英文 AI tells
    ├── voice-profile.md        # 入口 E：声音指纹提取
    ├── prompt-guard.md         # 入口 F：写前五问与起草约束
    └── examples.md             # 各入口前后对照，含"改过头"的反例
```

## 参考来源

| 来源项目 | 取了什么 |
|---|---|
| [blader/humanizer](https://github.com/blader/humanizer)、[Humanizer-zh](https://github.com/op7418/Humanizer-zh) | 24+ 项痕迹分类，底层是 Wikipedia《Signs of AI writing》 |
| [stop-slop](https://github.com/hardikpandya/stop-slop) | 禁用短语表、结构性套路清单、打分后再交付（原版 /50，这里 /100 且按入口加权） |
| [ai-flavor-remover](https://github.com/hylarucoder/ai-flavor-remover)、[说人话](https://github.com/MrGeDiao/shuorenhua) | 中文语境补充：翻译腔、空心动词、排版指纹 |
| [nuwa-skill](https://github.com/alchaincyf/nuwa-skill) | 从样本蒸馏表达风格 → 入口 E |
| [writing-agent](https://github.com/dongbeixiaohuo/writing-agent) | 分阶段流水线 → 三遍改写法 |
| [De-AI-Prompt-Enhancer](https://github.com/OUBIGFA/De-AI-Prompt-Enhancer-Writer-Booster-SKILL) | 写作前置约束 → 入口 F |
| [chatgpt-comparison-detection](https://github.com/Hello-SimpleAI/chatgpt-comparison-detection) | 检测与评分维度 → 入口 A |
| [taste-skill](https://github.com/Leonxlnx/taste-skill) | 反模板化的判断标准（原项目面向前端设计，只借取向） |

## 安装

**Claude.ai / Claude Code**：上传 `.skill` 文件到 Skills 设置，或点文件卡片上的 Save skill。

**Claude Code 手动**：

```bash
cp -r de-ai-writing ~/.claude/skills/
```

**Codex / Cursor**：把 `SKILL.md` 放进项目规则文件，references 按需粘贴。

## 用法

直接说需求，不用记入口名：

- `这段像不像 AI 写的，打个分` → A
- `帮我把这篇发布说明去下 AI 味` → B
- `这封给客户的邮件太客套了，改一下` → C
- `这份 RCA 读着像 AI 写的，但数据不能动` → D
- `这是我以前写的三篇，按我的风格改` → E + 对应入口
- `帮我写一篇 3.3 版本的发布说明，读者是已有客户的工程师` → F + B

## 一点说明

目的是让文字真的更好，不是骗过 AI 检测器。最有效的去 AI 味从来不是换词，而是往里放真实的信息：数字、时间、踩过的坑、你的判断。缺了这些，改得再干净也还是空的——所以这个技能宁可在文末列"需要你补充"，也不会替你编一个数字出来。
