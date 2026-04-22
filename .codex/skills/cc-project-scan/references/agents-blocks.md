# AGENTS Blocks

项目级 `AGENTS.md` 建议拆成“手写区 + 自动区”。

手写区适合保留：

- 项目概述
- 核心业务边界
- 高风险区域或禁改约定
- 与 Codex 协作偏好
- 用户补充的历史经验

自动区建议使用以下标记：

```md
<!-- AUTO:tech-stack -->
<!-- /AUTO:tech-stack -->

<!-- AUTO:directory -->
<!-- /AUTO:directory -->

<!-- AUTO:commands -->
<!-- /AUTO:commands -->

<!-- AUTO:api-contract -->
<!-- /AUTO:api-contract -->

<!-- AUTO:risk-areas -->
<!-- /AUTO:risk-areas -->
```

区块内容建议：

- `tech-stack`
  - 语言、框架、数据库、中间件、前端栈、构建工具
- `directory`
  - 核心目录及职责，不展开完整目录树
- `commands`
  - 开发、构建、测试、运行、容器相关命令
- `api-contract`
  - 成功响应包装、分页结构、筛选项结构、错误码约定
  - 不确定时写“待用户确认”
- `risk-areas`
  - 部署、迁移、环境配置、CI/CD、代理或网关配置等敏感位置

更新规则：

- 只替换对应 `AUTO:*` 区块内部内容
- 区块外内容视为用户手写内容，默认保留
- 若首次引入自动区块，应先确认“全量重建”还是“追加自动区块”
