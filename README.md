# ScamSense（拆招）

AI 多角色求职反诈模拟训练系统。用户在同一聊天界面中分别与林悦、陈浩和王宇交流，通过提问、核实与决策练习识别招聘风险，并获得有行为证据的复盘报告。

当前处于**架构设计阶段**，尚未创建业务工程或部署应用。

## 设计文档

- [架构设计 v1.1](docs/architecture.md)：项目定位、固定角色与岗位、S0–S6 状态机、模块与数据模型、REST/SSE 契约、评分、安全、部署、备份恢复、测试及 P0–P5 规划。
- [角色卡与剧情设计 v1.0（原文）](docs/scenario/characters-and-story-v1.0.md)：保留已有角色与剧情设计输入；未提供的 E01–E16 事件定义在架构文档中逐项标记 TODO。
- [.env.example](.env.example)：公开前端变量与后端配置的占位清单；只将 `VITE_API_BASE_URL` 用于前端，密钥只能配置在后端受保护环境中。

## 已确定方案

前端使用 Vue 3、TypeScript、Vite、Element Plus、Vue Router 和 Pinia，构建为静态资源并发布到 Qoder Sites。后端使用 Python、FastAPI、Pydantic、SQLAlchemy 2.x、SQLite 和 Alembic，在腾讯云 CVM 上由 Nginx、Uvicorn 和 systemd 运行。普通请求使用 HTTPS REST，角色回复使用 SSE；模型通过后端统一调用 OpenAI 兼容 API。

剧情状态由规则引擎控制，三个角色使用独立 Prompt 和独立上下文。评估基于实际行为和可追溯证据，四维权重为风险识别 25%、主动核实 30%、决策合理性 25%、证据分析 20%。

## 下一步与待确认事项

先进行 P0：补齐并评审 E01–E16、角色可见信息矩阵、资料字段与线索清单，再冻结评分规则、状态机、意图及 API 契约。服务器规格、域名、证书、模型服务和 Qoder Sites 实际发布配置均为 TODO，详见架构文档的确认清单。

本文档交付不包含业务代码、依赖安装或部署；功能测试与部署验收尚未执行。比赛公开应用地址：**TODO，完成实际部署验收后填写**。
