# 第三方 Skills

## 来源与版本

同步日期：2026-11-11。

| 本地目录 | 上游目录 | 固定提交 | 版本 |
| --- | --- | --- | --- |
| [frontend-design](web-frontend/frontend-design/) | [anthropics/skills · skills/frontend-design](https://github.com/anthropics/skills/tree/2c5958ecac7cee2b583967a2c4981d0f4a75c579/skills/frontend-design) | `2c5958ecac7cee2b583967a2c4981d0f4a75c579` | Skill 未声明版本号 |
| [impeccable](web-frontend/impeccable/) | [pbakaus/impeccable · .agents/skills/impeccable](https://github.com/pbakaus/impeccable/tree/b856e5010f2dd86bd97f9b2d5e38e33f3d5bd992/.agents/skills/impeccable) | `b856e5010f2dd86bd97f9b2d5e38e33f3d5bd992` | Skill `4.8.2`；引擎 `0.1.22` |
| [ui-ux-pro-max](web-frontend/ui-ux-pro-max/) | [nextlevelbuilder/ui-ux-pro-max-skill · .claude/skills/ui-ux-pro-max](https://github.com/nextlevelbuilder/ui-ux-pro-max-skill/tree/6ae86f61f520d6ca229d2f40e070410638c908c5/.claude/skills/ui-ux-pro-max) | `6ae86f61f520d6ca229d2f40e070410638c908c5` | 项目 `skill.json` 声明 `2.15.0` |
| [web-design-guidelines](web-frontend/web-design-guidelines/) | [vercel-labs/agent-skills · skills/web-design-guidelines](https://github.com/vercel-labs/agent-skills/tree/1a2c79d4e6c4a2283dc2c614b6538cbe1ed5ca62/skills/web-design-guidelines) | `1a2c79d4e6c4a2283dc2c614b6538cbe1ed5ca62` | Skill `1.0.0` |

`web-design-guidelines` 执行审查时读取 [web-interface-guidelines 的 command.md](https://github.com/vercel-labs/web-interface-guidelines/blob/main/command.md)，规则随上游更新，不受表中 Skill 提交限制。

## 本地适配与资源

- `ui-ux-pro-max/SKILL.md` 将依赖 `CLAUDE_PLUGIN_ROOT` 的搜索命令改为 `python3 "<skill-base-dir>/scripts/search.py"`，其中 `<skill-base-dir>` 指当前 `SKILL.md` 所在目录。更新上游时需保留这项适配。
- `impeccable` 的启动器、`scripts/VERSION` 和 `scripts/engine-checksums.txt` 配套更新；平台引擎由启动器下载并校验。

## 许可证与署名

| Skill | 文件来源 |
| --- | --- |
| frontend-design | 上游 Skill 目录中的 [LICENSE.txt](web-frontend/frontend-design/LICENSE.txt) |
| impeccable | 上游仓库根目录中的 [LICENSE](web-frontend/impeccable/LICENSE) 和 [NOTICE.md](web-frontend/impeccable/NOTICE.md) |
| ui-ux-pro-max | 上游仓库根目录中的 [LICENSE](web-frontend/ui-ux-pro-max/LICENSE) |
| web-design-guidelines | 所取上游目录及仓库根目录未提供独立许可证文件 |
