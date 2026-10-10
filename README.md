# Agent Playbook 使用说明

从 [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) 的 `AGENTS.md`、`.agents/` 和 agent-experience 提炼的可复用手册。

这不是那个仓库的拷贝。原文版权归原作者；这里只保留能搬到别的项目里的原则、模板和检查清单。

## 在项目里按需采用

这是一份独立参考包。按 [采用步骤](adoption-guide.md) 将需要的模板复制进目标项目，再按项目修改；不要直接覆盖已有的 `~/.agents` 或其他全局配置。仓库根目录的 `AGENTS.md` 含占位符和特定场景的规则，不能原样用于所有新项目。

## 目录

| 路径 | 用途 |
|---|---|
| `adoption-guide.md` | 30 分钟内落到一个仓库 |
| `reference/principles.md` | 为什么这样分，以及不该照搬什么 |
| `templates/AGENTS.md` | 仓库根常驻指令，复制后按项目删改 |
| `templates/docs/AGENTS.md` | 子树指令示例 |
| `templates/notes/README.md` | 决策记录怎么放、何时写 |
| `templates/notes/decision-record-template.md` | 一篇决策记录的骨架 |
| `templates/skills/context-and-tools/SKILL.md` | 模型看见什么、工具说明怎么写 |
| `templates/skills/prose/SKILL.md` | 注释和文档写到哪为止 |
| `templates/skills/error-handling/SKILL.md` | 失败、恢复、对用户怎么说 |
| `templates/skills/pre-change-checks/SKILL.md` | 提交前跑哪些检查、不跑哪些 |
| `checklists/automated-checks.md` | 值得做成自动检查的规则 |
| `checklists/writing-checklist.md` | 审文档和提示词时的废话清单 |

## 四条先记住

1. 每次会话都加载的文件只放「违反了就会做错」的规则，每条链到唯一归属。
2. 流程放 skill，理由放决策记录，契约放代码和文档。三者不互相复述。
3. 给模型的说明：关键限制出现在动作之前，输出有界，一句话只说一次。
4. 真正在乎的规则做成会失败的检查。模型读过 `AGENTS.md` 不算遵守。
