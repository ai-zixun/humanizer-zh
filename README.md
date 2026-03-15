# humanizer-zh

[中文](./README.md) | [English](./README.en.md)

`humanizer-zh` 是一个兼容 Codex、Claude Code 和 OpenClaw 的中文去 AI 味技能。它用于重写、润色或审阅中文博客、评论、产品分析、newsletter、书稿章节等长文本，让文字更像中文母语者写出来的，而不是翻译腔、模型拼接稿或营销通稿。

这个仓库采用「单目录即技能包」结构：仓库根目录本身就是技能目录。发布到 GitHub 后，可以直接 clone 到不同代理的 skills 路径中使用。

## 适用场景

- 中文博客、专栏、社论、评论稿的去 AI 味改写
- 中文产品分析、行业观察、长邮件、newsletter 的自然化润色
- 中译中修订，重点清理翻译腔、机械对照句、空泛大词和口号式收束
- 需要解释「这段中文为什么像 AI 写的」并给出修改前后示例

## 能力范围

- 识别并改写翻译腔、结构腔、排版腔和判断腔
- 识别并校正文级结构问题，检查开头、主体、结尾是否服务同一条主线
- 统一中文引号、日期、英文术语大小写与排版细节
- 根据文本类型调整改写力度，避免把说明文硬改成抒情文
- 深度改写时按需读取 `references/patterns.md`，解释常见问题模式
- 快速选择中文参照时，先读 `references/corpus-quickpick.md`
- 需要找中文母语参照时，按需读取 `references/corpus.md`

## 兼容性

| 平台 | 状态 | 说明 |
| --- | --- | --- |
| Codex | 支持 | 直接读取根目录下的 `SKILL.md`；`agents/openai.yaml` 只提供 Codex UI 展示元数据。 |
| Claude Code | 支持 | 读取同一份 `SKILL.md`；支持个人技能和项目技能目录。 |
| OpenClaw | 支持 | 按 AgentSkills 兼容目录读取同一份 `SKILL.md`；可放在托管技能目录或工作区技能目录。 |

真正决定技能行为的是 `SKILL.md` 与它引用的 `references/` 文件，不是 README。README 只用于 GitHub 或其他代码托管平台展示。

## 仓库结构

```text
humanizer-zh/
├── .gitignore
├── LICENSE
├── SKILL.md
├── README.md
├── README.en.md
├── agents/
│   └── openai.yaml
└── references/
    ├── corpus-quickpick.md
    ├── corpus.md
    └── patterns.md
```

## 安装

同一个仓库目录可以直接安装到不同代理的 skills 目录中。

### Codex

如果设置了 `CODEX_HOME`，放到 `$CODEX_HOME/skills`；默认路径一般是 `~/.codex/skills`。

```bash
mkdir -p ~/.codex/skills
git clone <your-repo-url> ~/.codex/skills/humanizer-zh
```

### Claude Code

Claude Code 支持个人技能和项目技能两种路径。

个人技能：

```bash
mkdir -p ~/.claude/skills
git clone <your-repo-url> ~/.claude/skills/humanizer-zh
```

项目技能：

```bash
mkdir -p ./.claude/skills
git clone <your-repo-url> ./.claude/skills/humanizer-zh
```

### OpenClaw

OpenClaw 支持托管技能目录和工作区技能目录。

托管技能：

```bash
mkdir -p ~/.openclaw/skills
git clone <your-repo-url> ~/.openclaw/skills/humanizer-zh
```

工作区技能：

```bash
mkdir -p ./skills
git clone <your-repo-url> ./skills/humanizer-zh
```

发布到 GitHub 之后，如果本地 OpenClaw 版本支持 CLI 安装，也可以尝试：

```bash
openclaw skills install github:<your-user>/humanizer-zh
```

## 使用方式

不同代理的触发方式略有区别，但运行入口都是同一份 `SKILL.md`。

### Codex

可以显式提到技能名：

```text
请用 $humanizer-zh 把这段中文改得更像中文母语者写的，减少翻译腔和空泛大词。
```

### Claude Code

Claude Code 的 Skills 以自动匹配为主，通常直接描述需求即可：

```text
把这篇中文稿子润色成更自然的母语表达，重点去掉翻译腔、机械排比和过火结论。
```

### OpenClaw

OpenClaw 既可以自动匹配，也可能把技能暴露为用户可调用命令，具体取决于本地配置：

```text
Use humanizer-zh to rewrite this Chinese draft so it reads like native Chinese writing.
```

## 运行时布局

- `SKILL.md` 是运行时入口，包含触发描述、工作流和输出约定
- `agents/openai.yaml` 只提供 Codex 的展示元数据，不影响 Claude Code 或 OpenClaw
- `references/corpus-quickpick.md` 是运行时速查表，先帮模型缩小参照范围
- `references/patterns.md` 是按需加载的深度参考，不会在每次触发时都占用上下文
- `references/corpus.md` 是按文体选参照的语料索引，不是固定模仿模板

## 设计约束

- frontmatter 只依赖通用字段 `name` 和 `description`，避免把代理私有配置写进运行入口
- 技能名使用小写连字符 `humanizer-zh`，便于兼容多代理的命名与路径约定
- 所有资源都通过相对路径组织，整个目录可以被直接复制或 symlink 到任意 skills 根目录

## 致谢

这个技能的整体方向与分享方式受到 [blader/humanizer](https://github.com/blader/humanizer) 的启发。原仓库把英文文本去 AI 味整理成可复用的 Claude Code skill；`humanizer-zh` 在这个思路上扩展到中文场景，重点处理翻译腔、中文节奏、标点排版和长篇非虚构写作中的机械表达。

## 许可证

本仓库采用 [MIT License](./LICENSE)。
