# 技术栈模块：Java 17+ & Spring Boot 3.x

本文件为可自由组合的**独立技术栈模块**，适用于采用 Java 17+ 与 Spring Boot 3.x（含 Spring MVC、Spring Security、Jakarta Validation、Lombok、Springdoc）的后端项目。

## 1. 包结构与组件组织

1. **模块分包与实现收敛**
   - 按业务模块划分包结构；模块内包含多个 Service 实现类时，统一收敛至模块下的 `impl` 子包。
   - 全局 `@Configuration` 配置类（如静态资源映射、安全配置、OpenAPI 配置）统一放入顶层或公共 `config` 包。
2. **Jakarta 标准命名空间**
   - Spring Boot 3.x 全链路使用 `jakarta.*` 包（如 `jakarta.validation.*`、`jakarta.servlet.*`、`jakarta.annotation.*`）。
3. **全局路由前缀与外部动态资源映射**
   - 公共路由前缀（如 `/api`）在 `application.yml` 中集中配置，各 `@RestController` 直接声明业务子路径。
   - 运行时动态上传的本地目录通过 `WebMvcConfigurer#addResourceHandlers` 映射对外访问路径，与 `src/main/resources` 打包资源分离。

## 2. 配置文件组织（`application.yml`）

1. **主配置集中与本地覆盖隔离**
   - 使用 `src/main/resources/application.yml` 集中管理所有公共配置，跨环境参数通过 `${ENV_VAR:default}` 注入。
   - 本地开发专属覆盖项放入 `src/main/resources/application-local.yml`，并在 `pom.xml` 中配置打包排除规则。
2. **沿用默认时区与时间序列化**
   - 统一使用本地标准时区（如北京时间）时，直接沿用 JVM 默认时区与 Spring Boot 默认的 `LocalDateTime` 序列化格式。

## 3. 声明式校验、Lombok 与异常处理

1. **Jakarta Validation 入参校验**
   - 请求 DTO 使用 `@NotBlank`、`@NotNull`、`@Min`、`@Size` 等注解配合 Controller 参数上的 `@Valid` 完成校验。
   - 在 `@RestControllerAdvice` 中直接从 `MethodArgumentNotValidException` / `BindException` 提取标准字段错误信息构造错误响应。
2. **Lombok 与 Java Record**
   - Entity、可变对象与 Service 实现类使用 `@Getter`、`@Setter`、`@RequiredArgsConstructor` 简化样板代码；不可变请求/响应 DTO 优先使用 Java `record`。
3. **精简的全局异常与安全响应**
   - 使用单一 `@RestControllerAdvice` 统一处理业务异常与参数校验异常。
   - 接入 Spring Security 时，通过 `AuthenticationEntryPoint` 与 `AccessDeniedHandler` 直接写入统一格式的认证/授权失败 JSON 响应。

## 4. Springdoc OpenAPI 导出

- 在 Controller、DTO 与枚举上使用 `@Tag`、`@Operation`、`@Schema`（如集合去重 `@Schema(uniqueItems = true)`）声明契约元数据，直接导出单一的 `openapi.yaml` 规范文件。
