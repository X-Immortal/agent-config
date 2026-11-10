---
name: devops-and-config
description: 用于应用配置文件管理、动静态资源映射、环境端口规划、Docker 与 Docker Compose 容器编排、Nginx 反向代理配置或 CI/CD 流水线搭建。提供通用配置与运维精简原则，以及可按需自由组合的基础设施模块（Docker + Nginx、GitHub Actions）。
---

# 配置管理与部署运维规范（核心摘要与技术栈导航）

## 1. 通用配置与运维核心原则

1. **配置集中化与默认值优先**：使用单一主配置文件集中管理公共配置，本地开发覆盖项放入独立的本地配置文件（打包排除），跨环境差异统一通过环境变量注入；当运行时、框架与数据库的默认配置已满足需求（如默认本地时区、默认时间序列化）时，直接沿用默认行为。
2. **服务端口与环境映射解耦**：区分服务监听端口、容器网络端口与宿主机映射端口；应用按实际运行位置连接目标，由环境配置或容器编排管理差异，不固定某个测试端口。
3. **静态资源托管与 API 反向代理分离**：前端静态容器专注于托管前端构建产物，API 反向代理统一由开发环境代理或生产环境入口网关承担。
4. **运行时动态资源外置管理**：用户或管理员动态上传的媒体与附件存放在代码包外的宿主机目录或持久化卷（仅挂载至后端容器），由后端静态资源映射统一提供读取；全局 API 路由前缀（如 `/api`）在全局配置中集中声明一次。
5. **极简容器化与务实 CI/CD**：`Dockerfile` 与 Compose 文件仅保留构建运行必需指令；数据库初始化脚本与字符集配置统一置于 `deploy/` 目录自动挂载；CI/CD 聚焦“编译检查 → 镜像构建推送 → 远端 Compose 更新”核心闭环。

## 2. 按需加载细则与可组合技术栈模块（References）

根据当前任务涉及的配置或部署组件，按需自由组合读取对应文件：

| 适用范围 | 读取文件 |
| :--- | :--- |
| **通用配置管理、端口解耦、动态资源与容器化完整细则** | [references/general-config-and-devops.md](references/general-config-and-devops.md) |
| **Docker Compose & Nginx**（极简 Dockerfile、前后端 Nginx 边界、生产按需编排、Volume 挂载） | [references/stack-docker-and-nginx.md](references/stack-docker-and-nginx.md) |
| **GitHub Actions CI/CD**（版本支持与固定策略、镜像发布与部署闭环、仓库提交约定） | [references/stack-github-actions.md](references/stack-github-actions.md) |
