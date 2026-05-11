# OpenSpec Schemas

**OpenSpec** 的可复用 Schema 定义。OpenSpec 是一个规格驱动的开发框架，通过分阶段工作流将功能想法转化为结构化、可验证的交付物。

[English](README.md) | 简体中文

## 包含的 Schema

| Schema | 说明 |
|--------|------|
| **super-spec-driven** | 完整生命周期工作流：brainstorm → proposal → specs/design → plan → tasks → apply。集成 **Superpowers** 技能实现 AI 辅助执行。 |

更多 Schema 持续更新中。

## super-spec-driven 工作流

```
brainstorm → proposal → specs / design → plan → tasks → apply → verify → archive
   (🤖)        (🤖)      (🤖)   (🤖)     (🤖)    (🤖)    (🤖)      (🤖)
```

| 阶段 | 产物 | 说明 |
|------|------|------|
| `brainstorm` | `brainstorm.md` | 使用 Superpowers 头脑风暴进行协作式设计探索 |
| `proposal` | `proposal.md` | 变更动机与受影响的能力 |
| `specs` | `specs/**/*.md` | 带有 WHEN/THEN 场景的可测试需求 |
| `design` | `design.md` | 技术决策、架构与风险 |
| `plan` | `plan.md` | 微任务拆分（2–5 分钟步骤，TDD 风格） |
| `tasks` | `tasks.md` | 从计划中提取的待办清单 |
| `apply` | — | 通过子代理驱动或内联方式执行任务 |
| `verify` | — | 检查完整性、正确性与一致性 |
| `archive` | — | 归档已完成的变更 |

每个阶段产出具体产物，下一阶段基于此构建——环环相扣，不留遗漏。

### 快速示例

```
1. /opsx:new my-feature --schema super-spec-driven
2. /opsx:continue   → brainstorm (superpowers:brainstorming)
3. /opsx:continue   → proposal
4. /opsx:continue   → specs + design（并行产出）
5. /opsx:continue   → plan (superpowers:writing-plans)
6. /opsx:continue   → tasks
7. /opsx:apply      → 实现（子代理驱动或内联执行）
8. /opsx:verify     → 完整性检查
9. /opsx:archive    → 归档变更
```

## 快速开始

### 前置条件

- 已安装并配置 **OpenSpec**
- 已安装 **Superpowers** 技能（`super-spec-driven` schema 需要）

### 安装

将 schema 文件夹复制到项目的 OpenSpec 目录：

```bash
## project-level schema
mkdir -p your-project/openspec/schemas/
cp -r openspec-schemas/schemas/super-spec-driven your-project/openspec/schemas/
## user-level schema
mkdir -p ~/.local/share/openspec/schemas/
cp -r openspec-schemas/schemas/super-spec-driven ~/.local/share/openspec/schemas/
```

安装后项目结构如下：

```
your-project/
├── openspec/
│   ├── config.yaml        # 项目配置
│   ├── schemas/           # 自定义 Schema 存放于此
│   │   └── super-spec-driven/
│   │       ├── schema.yaml
│   │       └── templates/
│   └── changes/           # 变更记录
└── src/
```

#### Schema 解析顺序

OpenSpec 按以下顺序查找 schema：

1. **CLI 参数** — `--schema <name>`
2. **变更元数据** — 变更文件夹中的 `.openspec.yaml`
3. **项目配置** — `openspec/config.yaml`
4. **默认值** — `spec-driven`

#### 配置为默认 Schema

编辑 `openspec/config.yaml` 设置 schema 和各产物的规则：

```yaml
schema: super-spec-driven

context: |
  Tech stack: TypeScript, React, Node.js
  We use conventional commits
  Domain: e-commerce platform

rules:
  proposal:
    - May include non-functional requirements (NFRs)
    - Include SLO targets (latency, concurrency, quality) when relevant
    - Include Capabilities section mapping to spec folder names
  specs:
    - Use Given/When/Then (Gherkin) format for all Scenarios
    - Every Requirement must include Priority (P0/P1/P2) and Rationale
    - Prefer existing specs over creating new ones.
  design:
    - Include designs for performance, availability, security, consistency, etc. (if applicable)
    - Include architecture diagrams (Mermaid or ASCII), sequence diagrams for complex flows
    - Avoid code implementation
```

## 参与贡献

欢迎贡献！添加新 Schema 的步骤：

1. 在 `schemas/<schema-name>/` 下创建文件夹
2. 添加 `schema.yaml` 定义工作流阶段
3. 在 `schemas/<schema-name>/templates/` 下添加模板
4. 提交 Pull Request

重大变更请先开 Issue 讨论。

## 致谢

灵感来源于 [JiangWay/openspec-schemas](https://github.com/JiangWay/openspec-schemas)。

## 许可证

[MIT](LICENSE)
