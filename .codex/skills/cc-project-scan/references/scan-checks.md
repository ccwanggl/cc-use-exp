# Scan Checks

优先扫描：

1. 仓库根目录 `AGENTS.md`
2. `README.md`
3. `.claude/CLAUDE.md`
4. `go.mod`
5. `pom.xml`
6. `build.gradle`
7. `package.json`
8. `pyproject.toml`
9. `Makefile`
10. `docker-compose.yml`
11. `Dockerfile`
12. `restart.sh`
13. `cmd/`、`internal/`、`pkg/`、`src/`、`app/`
14. `web/`、`frontend/`、`ui/`
15. `scripts/`、`deploy/`、`.github/`
16. 数据库迁移目录，如 `migrations/`、`sql/`

识别内容：

- 项目名称：优先取目录名，再结合 `README.md` 标题或构建文件补充
- 技术栈：语言、框架、ORM、数据库、中间件、前端框架、构建工具
- 常用命令：开发、构建、测试、部署、本地运行
- 目录职责：只总结核心目录，不输出超长树
- 高风险区域：部署脚本、迁移目录、CI/CD、环境配置、网关或代理配置
- API 契约线索：统一响应包装、分页结构、筛选项结构、错误码约定

判断原则：

- 能从文件直接确定的，记为“扫描识别”
- 只能从目录或命名习惯推断的，记为“推断，待确认”
- 无法可靠判断的，纳入提问，不要在 `AGENTS.md` 中伪造结论

推荐提问：

1. 用一句话描述项目目标或核心业务
2. 哪些目录、脚本或配置改动前必须先确认
3. API 返回、分页、筛选是否有统一契约
4. 是否存在 Codex 不应主动改动的模式、脚手架或历史约定
5. 若现有 `AGENTS.md` 无自动区块，是否接受首次全量重建
