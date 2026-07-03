# Business-Unit-for-Gaokao `.github`

本仓库维护 `Business-Unit-for-Gaokao` 的组织 profile、仓库地图和轻量治理说明。

## 文件

- `profile/README.md`：GitHub 组织首页展示内容。
- `docs/repository-map.md`：当前 live 仓库清单、用途、边界和维护原则。

## 当前状态

- 最近同步：2026-07-03
- 当前 live 仓库数：31（private 21 / public 10）
- 组织 Project：[`高考项目总览`](https://github.com/orgs/Business-Unit-for-Gaokao/projects/1)
- `gaokao` 已合并进 `requirements`；`requirements` 是业务需求、运营策略和 legacy notes 的标准入口。

## 维护原则

- 先回读 GitHub 当前仓库状态，再更新文档。
- 仓库删除、迁移、改名、合并后，同步更新 `docs/repository-map.md`、`profile/README.md` 和组织 Project。
- 当前代表爬虫线：`xuezhipingtai`、`sunshinegaokao`、`zhangshanggaokao`；历史 JSON 集中到 `gaokao-data-json`。
- `requirements` 是高考业务需求标准入口；`deploy` 是部署与运维标准入口。
- 开发和部署必须分开：应用仓库只负责开发、构建、测试、打包；部署、域名、证书、DNS、Pages、Cloudflare、服务器发布放独立部署仓库或部署流程。
- 简单 README/docs 更新可以直接维护 `main`；代码、部署、CI、架构性变更优先走 PR。
- 不提交 token、密码、SSH key、服务器凭据、客户隐私和未授权数据。
