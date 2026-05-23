# IELTS Claude Skills

一套跑在 Claude Code 上的雅思备考 AI 教练系统。8 个 Skill + 数据持久化 + 跨会话追踪。

## Skill 列表

| Skill | 做什么 |
|-------|--------|
| `/ielts` | 教练 · 摸底 + 路由 + 进度总览 |
| `/ielts-diagnose` | 诊断 · 算分策略 + 8 周计划 + 复诊 |
| `/ielts-writing` | 写作 · 四维批改（TR/CC/LR/GRA）+ 改写对比 + 审题 |
| `/ielts-reading` | 阅读 · 错题拆解 + 同义替换 + T/F/NG 三步框架 |
| `/ielts-listening` | 听力 · 8 类错题 + 11 种题型 + 精听计划 |
| `/ielts-speaking` | 口语 · 5 组万能故事 + Part 3 预测 + 表达升级 |
| `/ielts-vocab` | 词汇 · 每日推词 + 间隔重复 + 难词池 |
| `/ielts-grammar` | 语法 · 12 类错误追踪 + 定点练习 + 复测 |

## 设计原则

- **SOUL 人格** — 每个 Skill 有独立人格设定
- **模式系统** — 每个 Skill 分 2-3 种模式，进来先判断
- **数据持久化** — 所有学习数据写入 `~/.ielts/`，跨会话保留
- **跨会话追踪** — 下次批改自动对比上次，看进步
- **双机同步** — Skills 用 Git + symlink，数据用私有 Git 仓库

## 安装

### 前置

- Claude Code 已安装
- Git 已配置 SSH Key

### 自动安装（推荐）

```powershell
# 以管理员身份运行 PowerShell
git clone git@github.com:meiyulin22/ielts-skills.git "C:\Claude Work Space\ielts-skills"

# 创建符号链接到 Claude Code 技能目录
cmd /c mklink /D "%USERPROFILE%\.claude\skills\ielts" "C:\Claude Work Space\ielts-skills\ielts"
cmd /c mklink /D "%USERPROFILE%\.claude\skills\ielts-diagnose" "C:\Claude Work Space\ielts-skills\ielts-diagnose"
cmd /c mklink /D "%USERPROFILE%\.claude\skills\ielts-writing" "C:\Claude Work Space\ielts-skills\ielts-writing"
cmd /c mklink /D "%USERPROFILE%\.claude\skills\ielts-reading" "C:\Claude Work Space\ielts-skills\ielts-reading"
cmd /c mklink /D "%USERPROFILE%\.claude\skills\ielts-listening" "C:\Claude Work Space\ielts-skills\ielts-listening"
cmd /c mklink /D "%USERPROFILE%\.claude\skills\ielts-speaking" "C:\Claude Work Space\ielts-skills\ielts-speaking"
cmd /c mklink /D "%USERPROFILE%\.claude\skills\ielts-vocab" "C:\Claude Work Space\ielts-skills\ielts-vocab"
cmd /c mklink /D "%USERPROFILE%\.claude\skills\ielts-grammar" "C:\Claude Work Space\ielts-skills\ielts-grammar"
```

装完后重启 Claude Code，输入 `/reload-plugins`。

### 手动安装

将每个子目录复制到 `~/.claude/skills/`。

```powershell
cp -r "C:\Claude Work Space\ielts-skills\*" "$env:USERPROFILE\.claude\skills\"
```

## 更新

```bash
cd "C:\Claude Work Space\ielts-skills"
git pull
```

如使用 symlink，Claude Code 自动生效。如使用复制安装，需重新复制。

## 目录结构

```
ielts-skills/
├── ielts/SKILL.md              # 教练
├── ielts-diagnose/SKILL.md     # 诊断
├── ielts-writing/SKILL.md      # 写作
├── ielts-reading/SKILL.md      # 阅读
├── ielts-listening/SKILL.md    # 听力
├── ielts-speaking/SKILL.md     # 口语
├── ielts-vocab/SKILL.md        # 词汇
├── ielts-grammar/SKILL.md      # 语法
├── README.md
└── LICENSE
```

## 数据存储

学习数据存储在私有仓库 `meiyulin22/merlin-ielts-data` 的 `~/.ielts/` 下，与技能代码分离。

```
~/.ielts/
├── profile.md       # 目标分 · 当前水平 · 考试日期
├── listening/       # 每次听力错题分析
├── writing/         # 每篇作文批改
├── reading/         # 每次阅读分析 + 同义替换库
├── speaking/        # 口语素材
├── vocab/           # 词汇进度
├── grammar/         # 语法错误追踪
├── diagnose/        # 诊断报告
└── SCHEMA.md        # 数据格式规范
```

## 开发

每个 Skill 就是一个 `SKILL.md` 文件，包含：

- YAML frontmatter（name / description / version）
- SOUL（人格设定）
- 模式系统（2-3 种模式 + 触发条件）
- 输出模板
- 数据存储规则
- 边界声明

修改后直接生效，无需编译。

## License

MIT
