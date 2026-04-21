# Resume Policy

恢复优先级：

1. 用户显式要求 `--resume` 或“继续上次任务”
2. `.codex/tasks/` 中存在明显未完成任务（忽略 `archived/`）
3. 两者都没有时，开始新任务

处理原则：

- 每次运行先确保项目内 `.codex/tasks/` 与 `.codex/tasks/archived/` 存在；必须先尝试 `mkdir -p .codex/tasks/archived`，若可创建则不把“目录缺失”视为不可写
- 每次运行先扫描 `.codex/tasks/` 根目录；状态已是“已完成”的任务直接移到 `.codex/tasks/archived/`
- 未完成任务只有一个时，直接询问是否继续
- 有多个未完成任务时，列出名称和更新时间，让用户选
- 用户拒绝恢复时，把旧任务移到 `.codex/tasks/archived/` 后再开始新任务
- 已完成任务不留在 `.codex/tasks/` 根目录，完成后移动到 `.codex/tasks/archived/`
- 仅当项目目录在目录已创建后仍确认不可写时，才允许回退到 `~/.codex/tasks/`；并在输出中明确说明原因与影响
- 不要静默覆盖旧任务文件
