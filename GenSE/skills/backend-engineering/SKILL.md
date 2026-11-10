---
name: backend-engineering
description: 用于后端系统开发、业务模块与分层设计、持久层实现、事务与并发一致性控制或后端重构。提供跨语言的通用后端工程规范（模块边界、关注点分离、强类型枚举、数据访问与并发安全、声明式校验与精简异常处理），以及可按需自由组合的后端技术栈参考（Spring Boot、MyBatis-Plus、MySQL）。
---

# 后端工程规范（核心摘要与技术栈导航）

## 1. 跨语言通用后端核心原则

1. **按业务域内聚分包，内部适度扁平**：顶层按业务领域划分模块，模块内文件较少时直接置于模块根部，同类实现较多时再归入子目录；全局配置统一收敛至 `config` 目录。
2. **单向分层与模块数据所有权**：遵循 `协议适配层（Handler/Controller） → 领域与业务层（Service/UseCase） → 数据访问层（Repository/Mapper）` 单向依赖；每个模块对自身管理的数据表拥有唯一写入权，跨模块通过对方公开的业务接口协作。
3. **全链路强类型枚举与错误码内聚**：状态、角色、类型、排序维度、筛选区间与错误码全面使用强类型枚举或字面量联合类型，贯穿实体、DTO 与持久化；将协议状态码映射等伴随元数据内聚在错误码枚举内部。
4. **持久化分工与并发事务安全**：常规单表 CRUD 与简单动态过滤使用 ORM/查询构建器内置能力，复杂关联聚合与高并发原子条件更新（检查受影响行数）下沉为数据访问层显式查询；同一业务动作的状态变更、资源增减与审计日志在同一本地事务内原子提交，外部网络 I/O（邮件/HTTP）移出事务与锁持有期。
5. **声明式输入校验与扁平异常处理**：使用生态标准的声明式 Schema/注解完成输入校验；通过单一顶层全局异常处理器输出统一错误响应，审计日志持久化封装为独立内部服务。

## 2. 按需加载细则与可组合技术栈模块（References）

根据当前任务涉及的深度与项目实际选用的技术组件，按需自由组合读取对应文件。既有项目优先保持版本兼容；新建工程或获准升级时，查询官方支持状态与组件兼容要求，不将参考文件中的版本范围当作永久默认选型。

| 适用范围 | 读取文件 |
| :--- | :--- |
| **跨语言通用后端工程完整细则与案例** | [references/general-backend.md](references/general-backend.md) |
| **Java 17+ & Spring Boot 3.x**（Jakarta、`application.yml`、Validation、Lombok/Record、Springdoc） | [references/stack-spring-boot.md](references/stack-spring-boot.md) |
| **MyBatis-Plus**（`BaseMapper`、分页插件、`Wrapper` 与 Mapper 显式 SQL 边界） | [references/stack-mybatis-plus.md](references/stack-mybatis-plus.md) |
| **MySQL**（受支持版本选型、`utf8mb4`、初始化脚本、端口映射、原子条件更新与统一锁序） | [references/stack-mysql.md](references/stack-mysql.md) |
