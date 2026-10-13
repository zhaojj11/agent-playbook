# 可选能力规则

profile 是按项目能力选择的规则候选，不是整份复制的第二层提示词。

## 使用方法

1. 先完成 `templates/AGENTS.md` 中的项目事实。
2. 只打开与项目现有能力匹配的 profile。
3. 从中选择能指向具体代码、文档或检查的规则，改成项目里的真实名字后放入根或对应子树 `AGENTS.md`。
4. 没有明确对象和验证方式的规则不要选。

| Profile | 何时使用 |
|---|---|
| `typescript.md` | TypeScript 是主要实现语言 |
| `agent-product.md` | 产品会组装模型输入、调用工具或持久化会话 |
| `monorepo.md` | 多个包或服务共享接口和发布流程 |
| `documentation.md` | 仓库维护成体系的教程、参考或生成文档 |

profile 不是继承机制，工具不会自动合并这些文件。选中的规则必须进入工具实际会读取的 `AGENTS.md` 或 skill。
