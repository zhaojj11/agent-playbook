# 采用步骤

目标：把跨项目公共规则、当前仓库事实和可选能力规则分开，再组合成一份薄的常驻指令。先读 [分层抽象](reference/layering.md)。

## 1. 先选一个仓库

不要先改 `~/.agents`。全局指令会影响所有项目。先在一个仓库试。

远端仓库有内容后，可以把手册克隆到新项目的同级目录，再从手册目录复制所需文件：

```sh
git clone https://github.com/zhaojj11/agent-playbook.git ../agent-playbook
cp ../agent-playbook/templates/AGENTS.md ./AGENTS.md
```

这会复制模板，不会自动适配项目。继续完成下面的占位符、命令、规则和技能选择；如果同级目录已有同名目录，改用别的克隆路径。

## 2. 填项目事实

把 `templates/AGENTS.md` 复制到仓库根（如果第 1 步已经复制，直接编辑根目录的 `AGENTS.md`）。先只填写下面这些不能从模板获得的事实：

- 项目身份、主要用户和核心产物
- 架构或模块说明入口
- 代理容易走错的目录、生成文件和边界
- 实际存在的安装、测试、检查、构建和冒烟命令
- 三到七条项目特有不变量

改掉所有尖括号占位符。项目不存在某个命令、文档或机制时，删除对应行，不要留下空壳或悬空链接。

## 3. 选择能力 profile

查看 `templates/profiles/README.md`。只选择项目已经具备的能力：

- TypeScript：`templates/profiles/typescript.md`
- 模型、工具或会话产品：`templates/profiles/agent-product.md`
- 多包或多服务仓库：`templates/profiles/monorepo.md`
- 成体系的教程、参考或生成文档：`templates/profiles/documentation.md`

profile 是规则候选，不会被工具自动加载。只把能指向项目中具体对象和验证方式的条目改写进根或子树 `AGENTS.md`；不要整份复制。

## 4. 决定是否需要兼容文件

只有另一个工具的指令语义与 `AGENTS.md` 一致，而且目标平台和提交方式支持符号链接时，才共享同一份正文：

```sh
ln -s AGENTS.md CLAUDE.md
```

已有 `CLAUDE.md` 时先比较内容，不要覆盖。Windows、压缩包分发或不跟随符号链接的工具，应使用一个明确的生成或同步检查，而不是假设链接可用。

子目录只在规则真的不同时再加一份 `AGENTS.md`。子文件不重复根文件已经写过的仓库级规则。示例见 `templates/docs/AGENTS.md`。

## 5. 按需放 skill

只复制接下来两周会用到的 skill，放到仓库的 `.agents/skills/<name>/`：

- 在写工具、系统提示、多步工作流：`context-and-tools`
- 在改注释、README、对用户的文案：`prose`
- 在设计失败和重试：`error-handling`
- 在提交前不知道该跑什么：`pre-change-checks`
- 在审查提交、分支或 Pull Request：`code-review`
- 在排查并发、时钟和共享资源导致的测试波动：`test-reliability`
- 在修改公开接口、配置或持久化格式：`upgrade-guide`

skill 的 `description` 决定它会不会被加载。写成「什么时候用」，不要写成功能口号。复制 skill 后再在 `AGENTS.md` 中引用；没有复制时不要预留链接。

## 6. 决策才写笔记

把 `templates/notes/` 复制到 `.agents/notes/`。机械改名、局部界面调整、没有取舍的修改不要写笔记。

一篇笔记必须回答：问题是什么、决定是什么、还考虑过什么、代价是什么。

## 7. 给最重要的规则加检查

从 `checklists/automated-checks.md` 里挑一到三条会反复违反、又能客观判断的规则，做成脚本或 CI。例如：

- 根 `AGENTS.md` 超过约定字数就失败
- 文档里的本地链接目标不存在就失败
- 禁止新增某种已经决定封掉的写法

检查要快，并且只覆盖这次改动相关的部分。全量套件留给 CI。人会关掉拖慢自己的检查；关掉的检查比没有检查更糟，因为它看起来还在。

## 8. 做一次采用验收

采用完成时确认：

- `AGENTS.md` 没有尖括号占位符；
- 文件中引用的路径和命令真实存在；
- 每条 profile 规则都能指出项目里的适用对象；
- 子树文件没有重复根规则；
- 实际运行过至少一条与当前改动相关的检查。

## 9. 两周后删

删掉没被用到的 skill 和没人再引用的规则。常驻文件变长时，先把内容搬回它的归属文档，只留一行链接。
