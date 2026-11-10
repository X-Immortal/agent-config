# 技术栈模块：MyBatis-Plus

本文件为可自由组合的**独立技术栈模块**，适用于持久层采用 MyBatis-Plus 的 Java 后端项目。

## 1. 基础配置与样板消除

1. **充分发挥内置 CRUD 与分页能力**
   - 注册 MyBatis-Plus 分页插件（`PaginationInnerInterceptor`），实体 Mapper 统一继承 `BaseMapper<T>`。
   - 单表增删改查、常规字段过滤与分页查询直接使用 `BaseMapper` 内置方法及 `LambdaQueryWrapper` / `LambdaUpdateWrapper`。
2. **枚举映射**
   - 实体中的业务状态、类型等有限集合字段直接使用枚举类型，配合 MyBatis-Plus 标准枚举映射持久化稳定编码。

## 2. Wrapper 与 Mapper 显式 SQL 的分工边界

1. **Service 层使用简洁 Wrapper**
   - 当动态过滤或条件更新可用 Wrapper 在数行内简短清晰地表达、且不在多处重复时，直接在 Service 层构造 Wrapper。
2. **复杂查询与并发原子更新下沉至 Mapper SQL**
   - 当查询涉及多表关联聚合、复杂动态条件组合（导致在 Service 方法中大段拼接 SQL 片段），或涉及高并发原子条件更新（如在 `UPDATE` 的 `WHERE` 子句中校验库存/配额余量并原子递增占用量）时，将其下沉至 Mapper 中编写清晰的显式 SQL，并检查受影响行数。
