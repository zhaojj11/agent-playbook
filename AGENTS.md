# AGENTS.md

本仓库提供可组合的编码代理规则、能力 profile、skills 和决策记录模板。修改模板前先读 `reference/layering.md`。

## 布局

```text
reference/           分层和设计原则
templates/AGENTS.md  公共内核与项目事实槽位
templates/profiles/  可选能力规则，不整份复制
templates/skills/    按需任务流程
templates/notes/     决策记录模板
checklists/          审查和自动化候选
```

## 检查

本仓库没有构建步骤。文档改动至少运行：

```sh
git diff --check
rg -n '<[^>]+>' templates
```

第二条会找到模板中预期存在的占位符；人工确认新增命中属于明确的项目填写项。

## 规则

- 公共模板不能假设项目使用特定语言、框架、monorepo、Agent 产品、双语文档或决策记录。
- 能力相关规则放在 `templates/profiles/`；项目特有名字、命令和数值只出现在示例或占位符里。
- profile 是候选规则，不是自动加载的继承层。每条都说明适用条件和不该照搬的部分。
- 模板不能强制引用一个采用步骤没有要求复制的可选文件。
- 修改目录结构、采用流程或归属关系时，同步更新 README、采用指南和分层说明。
- 只报告实际运行过的检查，不把人工审阅写成自动验证。
