# 项目画像与路由矩阵

根据证据填写画像。信息不可用时写 `Unknown`，不能用猜测补齐。

## 审查背景

| 字段 | 内容 | 证据或限制 |
|---|---|---|
| 项目和审查问题 |  |  |
| 项目根目录和可用组件 |  |  |
| 审查日期和审查者 |  |  |
| 用户限制和明确要求审查的模块 |  |  |
| 产品类型和支持平台 |  |  |
| 运行时和入口 |  |  |
| 用户、角色、组织和租户 |  |  |
| 存储或处理的数据，包括敏感数据 |  |  |
| 收费、金额、订阅或发票 |  |  |
| AI 模型、提示词、Agent 或模型供应商 |  |  |
| 外部 API、Webhook、邮件和 OAuth |  |  |
| 部署、托管、CI/CD 和环境 |  |  |
| 合同、地区、监管义务 |  |  |
| 仓库外的运营证据 |  |  |
| 已检查路径和搜索范围 |  |  |
| 不可用组件和访问限制 |  |  |
| 已执行或未执行的动态验证 |  |  |

## 路由规则

- `RUN`：存在正向信号，或者用户明确要求审查该模块。
- `NOT_APPLICABLE`：明确范围证据和技术检查共同支持排除。
- `UNCONFIRMED`：现有证据不足，记录缺口，并尽可能只执行有限范围的证据缺口检查。
- 执行状态单独记录为 `PENDING`、`COMPLETE` 或 `NOT_REVIEWED`。

## 路由矩阵

保留所有行和 ID。引用证据 ID，不粘贴敏感值。

| 路由 ID | 模块 | 决定 | 正向信号和已检查证据 | 缺失证据 | 理由 | 执行状态 |
|---|---|---|---|---|---|---|
| R-01 | `readiness-identity-access` |  |  |  |  | PENDING |
| R-02 | `readiness-application-security` |  |  |  |  | PENDING |
| R-03 | `readiness-data-reliability` |  |  |  |  | PENDING |
| R-04 | `readiness-payments-billing` |  |  |  |  | PENDING |
| R-05 | `readiness-ai-safety` |  |  |  |  | PENDING |
| R-06 | `readiness-integrations` |  |  |  |  | PENDING |
| R-07 | `readiness-operations` |  |  |  |  | PENDING |
| R-08 | `readiness-quality-maintainability` |  |  |  |  | PENDING |
| R-09 | `readiness-user-experience` |  |  |  |  | PENDING |
| R-10 | `readiness-compliance` |  |  |  |  | PENDING |

## 范围示例

- 对完整、本地、单用户产品，如果明确范围说明不含支付和 AI，并且源码、依赖、配置检查相互印证，可以将 R-04 和 R-05 判为 `NOT_APPLICABLE`。
- 仅仅没有搜到支付关键词，应判为 `UNCONFIRMED`，不是 `NOT_APPLICABLE`。
- 仓库缺少部署证据时，仍可能支持 R-07 的代码级检查，但外部备份、告警和值班实践仍为 `UNCONFIRMED`。
- 用户明确要求支付审查时，即使没有看到供应商集成，也应为 `RUN`；报告范围不一致，不能静默拒绝用户要求的范围。
