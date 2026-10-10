# 采用步骤

目标：让一个仓库的编码代理有薄的常驻规则、按需流程和可追溯的决策，而不是一份越来越长的提示词。

## 1. 先选一个仓库

不要先改 `~/.agents`。全局指令会影响所有项目。先在一个仓库试。

远端仓库有内容后，可以把手册克隆到新项目的同级目录，再从手册目录复制所需文件：

```sh
git clone https://github.com/zhaojj11/agent-playbook.git ../agent-playbook
cp ../agent-playbook/templates/AGENTS.md ./AGENTS.md
```

这会复制模板，不会自动适配项目。继续完成下面的占位符、命令、规则和技能选择；如果同级目录已有同名目录，改用别的克隆路径。

## 2. 放常驻指令

把 `templates/AGENTS.md` 复制到仓库根（如果第 1 步已经复制，直接编辑根目录的 `AGENTS.md`），改掉尖括号里的占位符。删掉这个仓库用不到的条，尤其是与项目语言或运行方式无关的规则和命令。

如果某个工具只认 `CLAUDE.md`，用符号链接，不要维护第二份正文：

```sh
ln -s AGENTS.md CLAUDE.md
```

子目录只在规则真的不同时再加一份 `AGENTS.md`。子文件不重复根文件已经写过的仓库级规则。示例见 `templates/docs/AGENTS.md`。

## 3. 按需放 skill

只复制接下来两周会用到的 skill，放到仓库的 `.agents/skills/<name>/`：

- 在写工具、系统提示、多步工作流：`context-and-tools`
- 在改注释、README、对用户的文案：`prose`
- 在设计失败和重试：`error-handling`
- 在提交前不知道该跑什么：`pre-change-checks`

skill 的 `description` 决定它会不会被加载。写成「什么时候用」，不要写成功能口号。

## 4. 决策才写笔记

把 `templates/notes/` 复制到 `.agents/notes/`。机械改名、局部界面调整、没有取舍的修改不要写笔记。

一篇笔记必须回答：问题是什么、决定是什么、还考虑过什么、代价是什么。

## 5. 给最重要的三条加检查

从 `checklists/automated-checks.md` 里先挑三条会反复违反的，做成脚本或 CI。例如：

- 根 `AGENTS.md` 超过约定字数就失败
- 文档里的本地链接目标不存在就失败
- 禁止新增某种已经决定封掉的写法

检查要快，并且只覆盖这次改动相关的部分。全量套件留给 CI。人会关掉拖慢自己的检查；关掉的检查比没有检查更糟，因为它看起来还在。

## 6. 两周后删

删掉没被用到的 skill 和没人再引用的规则。常驻文件变长时，先把内容搬回它的归属文档，只留一行链接。
