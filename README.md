# Agent 配置与资源

集中管理可复用的 Agent 配置与资源。

## 内容导航

| 位置 | 内容与用途 |
| --- | --- |
| [AGENTS.md](AGENTS.md) | 通用开发约定 |
| [GenSE/guidelines](GenSE/guidelines/) | 工程执行与行为准则 |
| [GenSE/skills](GenSE/skills/) | 生成式软件工程工作流，以及前端、后端、配置与运维技能 |
| [writing/guidelines](writing/guidelines/) | 对话表达规范 |
| [writing/skills](writing/skills/) | 持久化文字规范与简洁风 PDF 生成规范 |
| [third-party](third-party/README.md) | 第三方技能、上游来源、固定提交、许可证与本地适配说明 |

## 推荐部署方式

Skill 推荐按整个目录链接到 Agent 的技能目录，使 `SKILL.md` 和附带资源保持在一起，修改仓库即可更新已安装的内容。不支持链接的工具可复制完整目录。

### Windows：为 Skill 建立目录链接

使用目录联接（junction），以下以 `backend-engineering` 为例，替换两处路径后执行：

```powershell
$repoRoot = (Resolve-Path -LiteralPath '<仓库绝对路径>').Path
$skillRoot = '<Agent 技能目录的绝对路径>'
$source = Join-Path $repoRoot 'GenSE/skills/backend-engineering'
$destination = Join-Path $skillRoot 'backend-engineering'

New-Item -ItemType Directory -Path $skillRoot -Force | Out-Null
if (Get-Item -LiteralPath $destination -Force -ErrorAction SilentlyContinue) {
    throw "目标位置已存在：$destination"
}
New-Item -ItemType Junction -Path $destination -Target $source
```

### Linux / macOS：为 Skill 建立符号链接

同样以 `backend-engineering` 为例，替换两处绝对路径后执行：

```bash
repo_root='/absolute/path/to/agent-config'
skill_root='/absolute/path/to/agent/skills'
source_dir="$repo_root/GenSE/skills/backend-engineering"
target_dir="$skill_root/backend-engineering"

mkdir -p "$skill_root"
if [ -e "$target_dir" ] || [ -L "$target_dir" ]; then
    printf '目标位置已存在：%s\n' "$target_dir" >&2
else
    ln -s "$source_dir" "$target_dir"
fi
```

### 选用规则

从 [AGENTS.md](AGENTS.md) 中挑选需要的条目，加入自己的全局或项目规则文件。需要使用 guideline 时，可以加入对应的读取要求：

```text
处理功能开发、架构调整或代码重构前，读取：
<仓库绝对路径>/GenSE/guidelines/engineering-discipline.md

处理工程任务的对话交流前，读取：
<仓库绝对路径>/writing/guidelines/conversation-writing.md
```

## 路径与运行依赖

- 文档中的相对文件链接以所在文档为基准；Skill 内的资源路径及 `<skill-base-dir>` 以该 Skill 的 `SKILL.md` 所在目录为基准。
- 执行脚本时使用解析后的路径，输出目录指向正在处理的项目。
- `ui-ux-pro-max` 需要 Python 3；`impeccable` 由启动器下载并校验平台引擎；PDF 生成需要相应的生成与渲染工具。
- 移动仓库后，需更新安装链接和外部引用。

## 版本维护

链接部署使用当前工作区内容，未提交修改和分支切换也会影响已安装的 Skill。需要固定版本时，可让链接指向指定提交的独立 checkout 或 worktree。

第三方资源的上游提交、本地适配与更新方法见 [第三方 Skills 说明](third-party/README.md)。
