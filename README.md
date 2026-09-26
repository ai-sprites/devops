# devops

发布运维角色与三个独立阶段 Skill：准备真实发布路径，完成已授权执行，并验证失败后的恢复结果。

## Skill 能力

| Skill | 负责什么 | 产出 |
| --- | --- | --- |
| [sprite-devops-release](skills/sprite-devops-release/SKILL.md) | 总流程、阶段选择与执行标准 | 明确当前阶段和完成条件 |
| [sprite-devops-prepare](skills/sprite-devops-prepare/SKILL.md) | 核对真实配置、发布和恢复条件 | 可执行发布手册与具体缺口 |
| [sprite-devops-execute](skills/sprite-devops-execute/SKILL.md) | 已授权构建、发布及健康监控 | 真实操作与验证记录 |
| [sprite-devops-recover](skills/sprite-devops-recover/SKILL.md) | 核对失败状态、按授权恢复并检查 | 恢复结果、证据和剩余影响 |

```text
skills/
├── sprite-devops-release/
│   ├── SKILL.md
│   ├── references/        完整工作方法、模板与交付规则
│   └── assets/templates/  完整发布手册模板
├── sprite-devops-prepare/
│   └── SKILL.md
├── sprite-devops-execute/
│   └── SKILL.md
└── sprite-devops-recover/
    └── SKILL.md
```

默认安装总流程与三个阶段，保持四个同级目录。每个阶段都有输入、实质步骤、输出和完成检查，共用 `sprite-devops-release/references/` 与 `assets/`，不要求开发或测试角色先安装。

## 工作顺序

```text
请求 / 版本 / 构建部署配置 / 测试证据
        │
PREPARE sprite-devops-prepare  → 发布手册与恢复安排
        │ 已有明确授权且条件满足
EXECUTE sprite-devops-execute  → 实际发布、健康与监控证据
        ├─ 成功 → 交付
        └─ 失败
RECOVER sprite-devops-recover  → 核对状态、恢复并验证
```

已有有效手册直接执行，已有故障直接恢复，只补受影响的准备。准备完成不等于已经上线，恢复命令存在不等于经过演练；已有明确执行授权沿用，不重复问，只暂停依赖缺失决定的操作。

## 直接使用

> 用 `$sprite-devops-release` 检查项目真实发布方式，准备发布与恢复步骤，按当前已有授权执行并核对结果。

> 用 `$sprite-devops-prepare` 为这个版本准备可执行发布手册。

> 用 `$sprite-devops-execute` 按手册和已有授权发布，完成健康检查与监控观察。

> 用 `$sprite-devops-recover` 先查清这次失败的真实状态，再按已有授权恢复并验证。

客户端不支持 `$` 调用时，让 AI 读取保存的同名 `SKILL.md`；也可直接使用 [发布运维角色](templates/agent.md)。读取说明、保存资源、实际加载、启动原生子代理和执行任务分别按真实结果判断。

## 接入当前项目

```text
请读取 https://github.com/ai-sprites/devops 的 README 和接入手册，将 sprite-devops 角色及 sprite-devops-release、sprite-devops-prepare、sprite-devops-execute、sprite-devops-recover 四个完整 Skill 接入当前项目。
固定同一明确版本，原样复制角色、全部 SKILL.md、参考与模板，保持四个同级目录、名称和内部相对引用；只适配当前客户端目录、元数据和入口。保留项目规则、自定义和未选资源，不合并阶段、不用摘要替代原文。
沿用项目已有目录和资料连接；实际任务通过现有 Jira、文档、代码或 CI MCP 按需读取资料，也可使用本地和用户材料。文档、记录及证据原位维护，无约定时可用 docs/devops/。
完成后核对实际文件、引用、采用版本和加载状态。旧版按手册保护自定义并补齐阶段；只有聊天权限时明确未写入项目，读取不到原文就说明缺项。
```

[接入手册](docs/installation.md) 说明完整安装、升级和加载检查，用户无需执行安装命令。角色可以自由组合，也可只安装所需阶段及其依赖。

## 产物与交接

发布准备维护可执行手册，包含本次适用的前提、执行顺序、健康/观察窗口和未决项，以及回滚、不可逆影响和恢复验证；实际执行后在同一手册追加结果。小型答疑不强建空文档，不编造命令、阈值、负责人、批准或执行证据。

手册、执行记录和证据沿用项目已有位置，无约定时可用 `docs/devops/`。历史文档原位维护，日志与 CI 证据可直接链接；产品代码、测试、CI/CD、IaC、部署配置和构建产物保留工程原目录。详见 [模板与交付](skills/sprite-devops-release/references/delivery.md) 和 [产物交接](docs/artifact-handoff.md)。

通过现有 Jira、文档、代码或 CI MCP 按需获取发布范围、版本和测试证据；本地及用户材料同样可用，不要求集中资料仓库。更新、追加和移除只处理指定范围，保护自定义，见 [维护规则](docs/installation.md#已有内容与后续维护)。

## 完整资源

<details>
<summary>角色、阶段、共享参考与模板清单</summary>

清单对应当前页面或 checkout 版本。接入固定完整 Git 提交后读取同批资源；历史 **v0.2.0** 可明确选用，以该标签内容为准。安装资源不等于生成全部业务文档。

| 资源 | 用途 | 接入范围 |
| --- | --- | --- |
| [templates/agent.md](templates/agent.md) | 职责、任务路由与边界 | 随角色默认完整接入 |
| [skills/sprite-devops-execute/SKILL.md](skills/sprite-devops-execute/SKILL.md) | 独立 Skill 入口 | 随角色默认完整接入 |
| [skills/sprite-devops-prepare/SKILL.md](skills/sprite-devops-prepare/SKILL.md) | 独立 Skill 入口 | 随角色默认完整接入 |
| [skills/sprite-devops-recover/SKILL.md](skills/sprite-devops-recover/SKILL.md) | 独立 Skill 入口 | 随角色默认完整接入 |
| [skills/sprite-devops-release/SKILL.md](skills/sprite-devops-release/SKILL.md) | 独立 Skill 入口 | 随角色默认完整接入 |
| [skills/sprite-devops-release/assets/templates/release-runbook.md](skills/sprite-devops-release/assets/templates/release-runbook.md) | 完整产物模板 | 随角色默认完整接入 |
| [skills/sprite-devops-release/references/delivery.md](skills/sprite-devops-release/references/delivery.md) | 工作方法与专业参考 | 随角色默认完整接入 |
| [skills/sprite-devops-release/references/workflow.md](skills/sprite-devops-release/references/workflow.md) | 工作方法与专业参考 | 随角色默认完整接入 |

</details>
