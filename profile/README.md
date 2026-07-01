# Business-Unit-for-Gaokao

高考志愿填报、数据采集、知识库、咨询交付和线上服务相关业务组织。

本组织承载高考业务线的应用代码、数据资产、运营知识、专用工具和部署编排；集团级战略和跨 BU 治理归 `President-Office`，通用平台底座、跨 BU clone-bot 和通用 codegen 能力归 `Business-Unit-for-Platform`。

## 核心边界

- **业务应用开发**：前端、后端、机器人、咨询系统、数据采集器等，放在对应业务/应用仓库。
- **部署运维**：服务器部署、域名、Nginx、证书、DNS、Pages、Cloudflare 等，放到独立部署仓库或部署流程；开发仓库不内置生产发布逻辑。
- **数据与知识**：业务数据、知识库、运营资料留在高考 BU 内，避免混入总裁办或平台底座仓库。
- **工具边界**：高考专用脚本留在本组织；可复用脚手架、clone-bot、通用 codegen、平台基础设施归 `Business-Unit-for-Platform`。

## 关键仓库

- [`multi-services-platform`](https://github.com/Business-Unit-for-Gaokao/multi-services-platform)：高考业务 Java 后端。
- [`future-exam-uniapp`](https://github.com/Business-Unit-for-Gaokao/future-exam-uniapp)：线上考试 / 高考业务 UniApp 端。
- [`gaokao`](https://github.com/Business-Unit-for-Gaokao/gaokao)：高考运营信息。
- [`gaokao-knowledge-base`](https://github.com/Business-Unit-for-Gaokao/gaokao-knowledge-base)：高考志愿咨询 Obsidian 知识库。
- [`gaokao-volunteer-bot`](https://github.com/Business-Unit-for-Gaokao/gaokao-volunteer-bot)：高考志愿填报 AI 机器人。
- [`future-deploy`](https://github.com/Business-Unit-for-Gaokao/future-deploy)：高考业务独立部署仓库。
- [`xuezhi-platform-crawler`](https://github.com/Business-Unit-for-Gaokao/xuezhi-platform-crawler)：学职平台独立爬虫，采集专业与职业数据。
- [`gaokao-xuezhi-crawler`](https://github.com/Business-Unit-for-Gaokao/gaokao-xuezhi-crawler)：高考 / 学职混合采集历史仓库。
- [`xuezhi-gaokao-crawler`](https://github.com/Business-Unit-for-Gaokao/xuezhi-gaokao-crawler)：Legacy CHSI 学职爬虫迁移仓库。

完整仓库清单见 [`docs/repository-map.md`](https://github.com/Business-Unit-for-Gaokao/.github/blob/main/docs/repository-map.md)。

## 治理原则

- 开发和部署必须分开：应用仓库只负责开发、构建、测试、打包；生产部署、域名、服务器发布进入独立部署仓库/流程。
- GitHub Actions 用于 CI/CD，不手动 SSH 到服务器操作生产发布。
- 不在仓库中保存 token、密码、服务器凭据、客户隐私或未授权数据。
- 仓库删除、迁移、合并后，要同步更新本组织 profile 和仓库地图。

---

_Last updated: 2026-07-01_
