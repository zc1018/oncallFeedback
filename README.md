# Oncall Feedback Router

把值班期间收到的「反馈内容 + 所在群」快速转成可执行处理建议：是否由值班人承接、是否建 TAPD、是否升级、怎么回复反馈人、以及如何记录闭环。

## 适用场景

- 值班群里有人反馈线上/线下业务问题，不确定该不该处理。
- 需要判断问题走工单机器人、手工 TAPD、云教室 400，还是业务侧权限处理。
- 需要一段可直接发到群里的回复话术。
- 需要整理 `值班日技术工单list` 的记录要点。

## 文件结构

```text
.
├── oncall-feedback-router.skill
└── oncall-feedback-router/
    ├── SKILL.md
    └── references/
        └── oncall-rules.md
```

- `oncall-feedback-router.skill`: 可分发/安装的 skill 包。
- `oncall-feedback-router/SKILL.md`: skill 入口说明、触发描述、输出格式。
- `oncall-feedback-router/references/oncall-rules.md`: 值班分流规则、SLA、闭环清单和示例。

## 安装

将 `oncall-feedback-router.skill` 导入支持 skills 的 Agent/Claude/Codex 环境即可。也可以直接使用 `oncall-feedback-router/` 目录作为源码版本进行维护。

## 使用方式

给出两个信息：

```text
所在群：线下需求沟通问题处理群
反馈内容：老师说考研 App 词测图片上传失败，重试也不行。
```

期望得到的输出结构：

```text
处理结论：
- 这个要由值班人承接，走手工 TAPD。按 App 反馈类记录，工单标题或标签里补 APP反馈。

马上做：
1. 先在群里确认影响范围。
2. 收集截图、账号、操作路径、失败提示。
3. 手工录入 TAPD，指派给对应负责人，并把工单链接同步回群。

回复话术：
> 收到，我先记录为 App 反馈问题。麻烦补一下失败截图、操作账号、出现时间，以及是否所有图片都上传失败。我会同步建 TAPD 跟进，建好后把工单链接发群里。

工单/记录要点：
- 来源群：
- 问题现象：
- 影响范围：
- 处理动作：
- owner / 下一步：
- 是否已同步反馈人：

需要补充的信息：
- 失败截图、账号、时间、影响范围
```

## 当前规则基线

规则来源于钉钉文档《产研值班机制》，基线日期为 `2026-06-17`。如果遇到政策敏感、值班表字段变化、群配置变化、或需要确认最新负责人时，应先刷新源文档再判断。

## 维护

更新规则时优先改：

```text
oncall-feedback-router/references/oncall-rules.md
```

如果触发描述、输入要求、输出模板变化，再同步更新：

```text
oncall-feedback-router/SKILL.md
```

修改后重新打包生成 `.skill` 文件，确保源码和包文件保持一致。
