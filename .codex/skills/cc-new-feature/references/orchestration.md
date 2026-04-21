# Orchestration

推荐顺序：

1. 清理 `.codex/tasks/` 根目录中状态已是“已完成”的任务，并移动到 `.codex/tasks/archived/`
2. 若 `.codex/tasks/` 不存在，先在项目内执行 `mkdir -p .codex/tasks/archived` 创建 `.codex/tasks/` 与 `.codex/tasks/archived/`
3. 需求澄清
4. 设计和范围确认
5. 创建任务文件
6. 分步实现
7. 定向验证
8. Quick review 视角自查
9. 将已完成任务移动到对应 `.codex/tasks/archived/`；若使用了回退目录，则移动到回退目录下的 `archived/`

编排原则：

- 小步推进，不把所有工作压成一个大提交
- 每一步都要能解释“为什么现在做”
- 修改范围失控时，先回到任务文件收敛范围
- 只有用户确认方向后，才进入大改动实现
