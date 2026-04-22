# Orchestration

推荐顺序：

1. 清理 `.codex/tasks/` 根目录中状态已是“已完成”的任务，并移动到 `.codex/tasks/archived/`
2. 若 `.codex/tasks/` 不存在，先在项目内执行 `mkdir -p .codex/tasks/archived` 创建 `.codex/tasks/` 与 `.codex/tasks/archived/`
3. 即使 `.codex/tasks/` 已存在，也必须先做一次项目根目录写入尝试，不能因为“已有骨架”就跳过初始化动作
4. 需求澄清
5. 设计和范围确认
6. 创建任务文件
7. 确认进入实际实现时，将当前主任务状态切换为 `进行中`
8. 分步实现
9. 定向验证
10. Quick review 视角自查
11. 将已完成任务移动到对应 `.codex/tasks/archived/`；若使用了回退目录，则移动到回退目录下的 `archived/`

编排原则：

- 小步推进，不把所有工作压成一个大提交
- 每一步都要能解释“为什么现在做”
- 修改范围失控时，先回到任务文件收敛范围
- 只有用户确认方向后，才进入大改动实现
