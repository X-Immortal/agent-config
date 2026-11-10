# 技术栈模块：Vue 3 + TypeScript + Vite

本文件为可自由组合的**独立技术栈模块**，适用于采用 Vue 3、TypeScript 与 Vite 的前端项目。Vue Router、Pinia 与 Axios 按实际需求及仓库已有选型使用，不因采用 Vue 而全部引入。

## 1. 工程结构与路由隔离

1. **视图、布局与路由模块化**
   - 按功能域组织视图、组件与请求模块；使用路由时可设置 `views/`、`router/`、`components/` 与 `api/` 等目录。根组件 `App.vue` 保持轻量，已采用 Vue Router 时负责顶层路由出口（`<router-view />`）与全局容器。
   - 若不同角色界面的访问边界或布局明显不同，通过独立的 `Layout` 组件与路由分支隔离；相同布局可以复用。
2. **按导航语义实现返回**
   - 需要返回上一应用内访问位置时使用 `vue-router` 的 `router.back()`，并处理缺少应用内历史的情况；“返回列表”等明确目标操作使用对应路由。

## 2. TypeScript 类型对齐与状态管理

1. **严格的接口与枚举类型定义**
   - 为 API 请求参数、响应结构与业务枚举定义明确的 TypeScript `interface` / `type` / `enum`，与后端接口契约保持一致。
2. **统一请求封装与轻量共享状态**
   - 沿用项目的请求机制，如原生 `fetch` 或 Axios；采用 Axios 时可通过实例与拦截器管理公共配置及认证，不重复展示调用方已处理的错误。
   - 页面局部状态使用 `ref` / `reactive` 就近管理；根据共享范围与维护需要选择 composable、`provide/inject` 或 Pinia。已采用 Pinia 时，Store 仅维护必要的共享状态，避免与局部状态重复持有同一数据。
