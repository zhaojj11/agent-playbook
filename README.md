# Agent Playbook 使用说明

从 [DeepSeek Harness](https://github.com/deepseek-ai/deepseek-harness) 的 `AGENTS.md`、`.agents/` 和 agent-experience 提炼的可复用手册。

这不是那个仓库的拷贝。原文版权归原作者；这里只保留能搬到别的项目里的原则、模板和检查清单。

## 在项目里按需采用

这是一份独立参考包。先读 [公共与差异的分层](reference/layering.md)，再按 [采用步骤](adoption-guide.md) 组合公共内核、项目事实和可选能力规则。不要直接覆盖已有的 `AGENTS.md`、`~/.agents` 或其他全局配置。

## 三层组合

1. **公共内核**：修改范围、事实归属、失败、凭证和验证等跨项目规则。
2. **项目事实**：仓库身份、目录、命令、架构入口和项目不变量，必须现场填写。
3. **能力规则**：TypeScript、Agent 产品、monorepo、文档集等 profile，项目具备该能力时才选择。

任务步骤继续放 skill，取舍放决策记录，可机械判断的不变量放检查；它们不是根 `AGENTS.md` 的附录。

## 目录

| 路径 | 用途 |
|---|---|
| [`adoption-guide.md`](adoption-guide.md) | 把公共内核和项目差异组合进一个仓库 |
| [`reference/layering.md`](reference/layering.md) | 判断一条规则是公共、能力相关还是项目特有 |
| [`reference/principles.md`](reference/principles.md) | 为什么这样分，以及不该照搬什么 |
| [`templates/AGENTS.md`](templates/AGENTS.md) | 只含公共内核和项目事实槽位的根模板 |
| [`templates/profiles/`](templates/profiles/README.md) | 按项目能力选择的规则候选 |
| [`templates/docs/AGENTS.md`](templates/docs/AGENTS.md) | 子树指令示例 |
| [`templates/notes/`](templates/notes/README.md) | 决策记录的规则和骨架 |
| [`templates/skills/`](templates/skills/) | 按需加载的任务流程和判断标准 |
| [`checklists/automated-checks.md`](checklists/automated-checks.md) | 值得做成自动检查的规则 |
| [`checklists/writing-checklist.md`](checklists/writing-checklist.md) | 审文档和提示词时的废话清单 |

## 四条先记住

1. 每次会话都加载的文件只放「违反了就会做错」的规则，每条链到唯一归属。
2. 流程放 skill，理由放决策记录，契约放代码和文档。三者不互相复述。
3. 给模型的说明：关键限制出现在动作之前，输出有界，一句话只说一次。
4. 真正在乎的规则做成会失败的检查。模型读过 `AGENTS.md` 不算遵守。
