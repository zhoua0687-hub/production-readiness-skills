# Production Readiness Skills — 中文说明

这是一套按项目实际情况裁剪范围的生产就绪审查技能。它不是要求所有产品完成一张巨大清单，而是先建立项目画像，再选择适用专项，最后根据证据汇总风险。

## 套件组成

- **1 个总控：** `production-readiness-review`
- **10 个专项：** 身份与访问、应用安全、数据可靠性、支付与账单、AI 安全、集成、运营与韧性、质量与可维护性、用户体验、合规与保证
- **3 组双语参考模板：** 项目画像与路由矩阵、证据与严重程度、审查报告

总控和全部专项目录如下：

```text
production-readiness-skills/
├── README.en.md
├── README.zh-CN.md
└── skills/
    ├── production-readiness-review/
    │   ├── SKILL.md
    │   ├── SKILL.zh-CN.md
    │   └── references/
    ├── readiness-identity-access/
    ├── readiness-application-security/
    ├── readiness-data-reliability/
    ├── readiness-payments-billing/
    ├── readiness-ai-safety/
    ├── readiness-integrations/
    ├── readiness-operations/
    ├── readiness-quality-maintainability/
    ├── readiness-user-experience/
    └── readiness-compliance/
```

每个专项目录都包含英文 `SKILL.md` 和中文 `SKILL.zh-CN.md`。

## 核心行为

### 按需审查

总控为每个模块记录以下路由之一：

- `RUN`：有正向证据表明能力或风险存在，或用户明确要求审查。
- `NOT_APPLICABLE`：明确范围证据和技术检查共同支持排除。
- `UNCONFIRMED`：证据不足，不能决定；尽可能进行有限范围的证据缺口检查。

例如，确认产品不含支付或金额数据时，可以跳过支付专项；仅仅没有搜到支付关键词，必须保持 `UNCONFIRMED`。每个模块都会出现在路由矩阵中，不会静默消失。

### 证据优先

- 问题必须有具体风险场景、严重程度、置信度和可复核位置。
- 已有控制也必须有证据，不能只写“看起来安全”。
- 仓库没有备份演练、值班或合规文件，不等于现实中没有执行。
- `UNCONFIRMED` 和 `NOT_REVIEWED` 不算通过，也不会自动算作漏洞。
- 重点问题最多 10 个，不足时不硬凑。

### 默认只读

技能不会修改被审查产品的代码、配置、依赖、基础设施或外部服务，也不会擅自执行破坏性测试、真实支付、外部扫描或模型调用。只有用户要求文档输出时，才允许在指定或新建报告目录写入两份报告。

## 安装

本目录是**源文件套件**，创建后并未自动安装。

项目级安装：

1. 打开 `skills/`。
2. 将其中全部 11 个技能目录复制到目标项目的 `.claude/skills/`。
3. 保留每个目录的名称和内部结构，尤其不要遗漏总控的 `references/`。
4. 按所用 Claude Code 版本的要求重新加载技能，并确认总控和专项出现在可用技能列表中。

如需个人级安装，可将同样 11 个目录复制到个人技能目录。只安装总控而不安装专项，会导致相应模块标记为 `NOT_REVIEWED`，因此建议整套安装。

## 使用

完整生产就绪审查：

```text
/production-readiness-review
```

也可以直接要求某个专项，例如：

```text
/readiness-payments-billing
```

直接调用专项适合明确的局部审查；需要范围裁剪、跨专项去重和统一优先级时，使用总控。

## 双语输出

- 英文技能入口：`SKILL.md`
- 中文技能入口：`SKILL.zh-CN.md`
- 其他英文文档：`*.en.md`
- 其他中文文档：`*.zh-CN.md`
- 总控文件报告：`readiness-report.en.md` 与 `readiness-report.zh-CN.md`
- 专项直接产生文件报告时：使用对应模块名称的 `.en.md` 与 `.zh-CN.md` 成对文件

中英文报告必须使用相同的路由 ID、发现 ID、证据 ID、数量、严重程度、置信度、排序和限制。只翻译说明文字，不翻译路径、代码、配置键、命令和标识符。不能一版完整、另一版只有摘要。

修改任一规则、模板或报告后，必须同步另一语言版本。

## 适用边界

这套技能用于广泛的生产就绪风险审查，不替代：

- 针对单次变更的代码审查
- 由授权人员执行的渗透测试
- 法律、税务、监管或认证结论
- 生产迁移、恢复、 failover、负载或告警演练
- 对私有云配置、供应商控制台和公司流程的直接验证

未实际执行的项目必须明确写为未验证或无法确认。

## 维护检查

修改套件后检查：

1. 所有技能目录都有成对双语入口，frontmatter 名称与目录一致。
2. 总控中的模块名称和路由 ID 与专项目录一致。
3. 所有引用路径有效，英文和中文文档章节及规则等价。
4. 跳过依据、未知项和验证限制没有被省略。
5. 没有将产品修改、依赖安装或外部服务操作变成默认行为。
