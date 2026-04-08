# Competitive Hypothesis Validator（竞争性假设验证器）

A Claude Code skill for validating competitive hypotheses in academic research, grounded in your own local literature database.

---

## 这个 skill 做什么

给定一个研究议题（如"绩效压力对官员行为的影响"），或一对已有的竞争性假设（H1a/H1b），它会：

1. 从你的本地文献库中检索相关理论依据
2. 判断这对假设是否真正构成"理论竞争"（而不是实证不一致或调节效应）
3. 为每个假设构建完整的**理论来源 + 关键引用 + 推理链**
4. 输出格式化的**竞争性假设验证报告**

**核心原则**：它是验证者，不是生成者。只引用数据库中真实存在的文献，不会捏造引用。

---

## 安装方法

### 1. 复制 skill 文件

将整个文件夹复制到 Claude Code 的 skills 目录：

```bash
# macOS / Linux
cp -r competitive-hypothesis-validator ~/.claude/skills/

# Windows
xcopy competitive-hypothesis-validator %USERPROFILE%\.claude\skills\competitive-hypothesis-validator /E /I
```

### 2. 配置你的文献数据库

编辑 `references/database-guide.md`，按照其中的说明：
- 填写你的文献库根路径
- 列出你的文献库文件及对应主题
- 建立议题→文件速查表

### 3. 建立文献库文件

在你指定的路径下，按 `references/database-guide.md` 中的格式，创建你自己领域的文献库文件。

---

## 文献库格式（简要）

每个文献库文件是一个 Markdown 文件，包含精读文献条目：

```markdown
# [主题]文献库

### Author, A. (Year). Title. *Journal*.
- **核心主张**：[该论文的中心论点]
- **对竞争性假设的贡献**：[支持哪个方向，为什么]
- **被引量**：TC: xxx
```

完整格式说明见 `references/database-guide.md`。

---

## 使用方式

安装并配置完成后，在 Claude Code 中直接输入：

```
/competitive-hypothesis-validator 绩效压力对街头官僚避责行为的影响，帮我验证能否提出竞争性假设
```

或：

```
/competitive-hypothesis-validator H1a：透明度提升会增强问责效果；H1b：透明度提升会加剧避责行为。这两个假设真的竞争吗？
```

---

## 什么是"真正的竞争性假设"

很多研究者混淆了以下三种情况：

| 情形 | 正确处理方式 |
|------|------------|
| 同一X→Y，两种理论预测方向相反 | ✅ 真竞争，写成 H1a/H1b |
| 条件A下正效应，条件B下负效应 | ❌ 不是竞争，应写成调节假设 H2 |
| 实证文献中结果不一致 | ❌ 不是理论竞争，是实证分歧 |

判断标准：**H1a 和 H1b 能同时为真吗？如果能，它们不是竞争性假设。**

---

## 适用领域

本 skill 的工作流程是通用的，适用于任何有本地文献库的研究领域。原始版本针对**公共管理**领域设计，但只需替换文献库内容，即可用于：
- 政治学、社会学、经济学
- 管理学、组织行为学
- 任何需要从理论文献出发构建假设的社会科学研究

---

## 文件结构

```
competitive-hypothesis-validator/
├── README.md                    ← 本文件
├── SKILL.md                     ← skill 核心逻辑（Claude 读取）
└── references/
    └── database-guide.md        ← 文献库配置模板（用户填写）
```

---

## License

MIT
