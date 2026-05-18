# 企业级通用多Agent数字员工平台

本仓库用于保存“企业级通用多Agent数字员工平台”的可行性方案、需求规格和后续落地资产。

## 当前内容

- `企业级通用多Agent系统可行性及落地方案.docx`: 原始方案文档
- `generate_multi_agent_plan.js`: 生成方案文档的脚本
- `specs/001-enterprise-agent-platform/spec.md`: 从方案文档提取的 Spec Kit 需求规格
- `specs/001-enterprise-agent-platform/checklists/requirements.md`: 需求规格质量检查清单
- `specs/001-enterprise-agent-platform/plan.md`: 技术实施计划
- `specs/001-enterprise-agent-platform/research.md`: 技术决策研究记录
- `specs/001-enterprise-agent-platform/data-model.md`: 领域数据模型
- `specs/001-enterprise-agent-platform/contracts/openapi.yaml`: 一期 REST API 契约
- `specs/001-enterprise-agent-platform/quickstart.md`: 计划产物校验与交接说明
- `specs/001-enterprise-agent-platform/tasks.md`: 细粒度、按用户故事组织的实现任务清单

## 需求主线

一期目标是建设通用数字员工平台最小闭环，覆盖数字员工目录、角色配置、任务提交、多Agent协同、知识与工具接入、人工审核、审计追溯和运营评测。

首批验证场景：

- 采购流程样例
- 企业知识检索样例
- 项目周报样例

## 建议下一步

按 Speckit 日常流程继续推进：

```text
speckit-analyze -> speckit-implement
```
