# Business-Unit-for-Gaokao `.github`

本仓库维护 `Business-Unit-for-Gaokao` 的组织 profile、仓库地图和轻量治理说明。

## 文件

- `profile/README.md`：GitHub 组织首页展示内容。
- `docs/repository-map.md`：当前仓库清单、用途、边界和维护原则。

## 维护原则

- 先回读 GitHub 当前仓库状态，再更新文档。
- 仓库删除、迁移、改名后，同步更新 `docs/repository-map.md`。
- 开发和部署必须分开：应用仓库只负责开发、构建、测试、打包；部署、域名、证书、DNS、Pages、Cloudflare、服务器发布放独立部署仓库或部署流程。
- 简单 README/docs 更新可以直接维护 `main`；代码、部署、CI、架构性变更优先走 PR。
- 不提交 token、密码、SSH key、服务器凭据、客户隐私和未授权数据。
