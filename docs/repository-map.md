# Business-Unit-for-Gaokao Repository Map

本文记录 `Business-Unit-for-Gaokao` 当前 live 仓库用途、边界和维护原则。仓库清单基于 GitHub API 于 2026-07-03 回读确认，当前组织共 **31** 个 live 仓库（private 21 / public 10）。已删除、迁移或合并后的历史仓库不再列入当前库存，也不在组织 Project 中保留卡片。

## 组织边界

`Business-Unit-for-Gaokao` 承载高考志愿填报、数据采集、知识库、咨询交付、线上服务和相关部署编排。

- 具体业务代码、业务数据资产、业务专属知识库：留在本组织。
- 业务需求、MVP、工作流、运营策略和未决问题：统一进入 [`requirements`](https://github.com/Business-Unit-for-Gaokao/requirements)。
- 部署、域名、CI/CD、环境映射和运维说明：进入标准 [`deploy`](https://github.com/Business-Unit-for-Gaokao/deploy)，既有部署资产可继续由 [`future-deploy`](https://github.com/Business-Unit-for-Gaokao/future-deploy) 承接。
- 通用平台底座、跨 BU clone-bot 和通用 codegen 能力：归 `Business-Unit-for-Platform`。
- 集团级战略、组合管理、制度和跨 BU 治理：归 `President-Office`。

## 开发 / 部署分离原则

- 应用开发仓库只负责：源代码、构建、测试、打包、开发说明。
- 部署仓库或独立部署流程负责：服务器发布、Nginx、域名、证书、DNS、Pages、Cloudflare、生产环境编排。
- 不要把生产发布逻辑塞进业务开发仓库；需要发布时由部署仓库消费构建产物或明确版本。
- 部署默认走 GitHub Actions/CI，不手动 SSH；密钥只放 GitHub Actions secrets，不写入仓库。

## 仓库合并状态

- `gaokao` 已合并进 [`requirements`](https://github.com/Business-Unit-for-Gaokao/requirements)，`requirements` 是高考业务需求、运营策略和 legacy strategy/operating notes 的 live source of truth。
- 组织 Project 只跟踪当前 live 仓库；已删除或不在组织内的历史仓库不保留卡片。

## 当前三条代表爬虫线

| Repository | Role |
| --- | --- |
| [`xuezhipingtai`](https://github.com/Business-Unit-for-Gaokao/xuezhipingtai) | 学职平台 / `xz.chsi.com.cn` 代表爬虫仓库。 |
| [`sunshinegaokao`](https://github.com/Business-Unit-for-Gaokao/sunshinegaokao) | 阳光高考 / CHSI 代表爬虫仓库。 |
| [`zhangshanggaokao`](https://github.com/Business-Unit-for-Gaokao/zhangshanggaokao) | 掌上高考 / `gaokao.cn` 代表爬虫仓库。 |

## 需求与治理入口

| Repository | Visibility | Language | Updated | Purpose / Notes |
| --- | --- | --- | --- | --- |
| [`requirements`](https://github.com/Business-Unit-for-Gaokao/requirements) | private | - | 2026-07-03 | Business-Unit-for-Gaokao business/product requirements |
| [`.github`](https://github.com/Business-Unit-for-Gaokao/.github) | public | - | 2026-07-03 | Business-Unit-for-Gaokao organization profile and repository map |

## 部署与运维

| Repository | Visibility | Language | Updated | Purpose / Notes |
| --- | --- | --- | --- | --- |
| [`deploy`](https://github.com/Business-Unit-for-Gaokao/deploy) | private | - | 2026-07-01 | Business-Unit-for-Gaokao deployment and operations |
| [`future-deploy`](https://github.com/Business-Unit-for-Gaokao/future-deploy) | private | Shell | 2026-07-01 | 自动化部署项目：Docker Compose 编排 Redis、MySQL 及前后端服务部署 |

## 数据、知识库与运营资料

| Repository | Visibility | Language | Updated | Purpose / Notes |
| --- | --- | --- | --- | --- |
| [`gaokao-data-json`](https://github.com/Business-Unit-for-Gaokao/gaokao-data-json) | private | - | 2026-07-01 | Gaokao JSON data snapshots consolidated from crawler repositories |
| [`gaokao-knowledge-base`](https://github.com/Business-Unit-for-Gaokao/gaokao-knowledge-base) | private | Python | 2026-07-03 | 高考志愿咨询 Obsidian 知识库 |
| [`infromation`](https://github.com/Business-Unit-for-Gaokao/infromation) | private | Python | 2026-07-03 | 无描述 |

## 核心业务应用

| Repository | Visibility | Language | Updated | Purpose / Notes |
| --- | --- | --- | --- | --- |
| [`multi-services-platform`](https://github.com/Business-Unit-for-Gaokao/multi-services-platform) | private | Java | 2026-07-01 | FutureTechJava后端 |
| [`future-exam-uniapp`](https://github.com/Business-Unit-for-Gaokao/future-exam-uniapp) | private | Vue | 2026-06-27 | FutureTech线上考试uniapp端 |
| [`uni-app-gaokao`](https://github.com/Business-Unit-for-Gaokao/uni-app-gaokao) | private | Vue | 2026-06-09 | FutureTech高考uniapp端 |
| [`gaokao-volunteer-bot`](https://github.com/Business-Unit-for-Gaokao/gaokao-volunteer-bot) | private | JavaScript | 2026-06-25 | Gaokao volunteer application chatbot with Playwright data collection |
| [`gaokao-zhiyuan-consulting-system-open`](https://github.com/Business-Unit-for-Gaokao/gaokao-zhiyuan-consulting-system-open) | private | JavaScript | 2026-06-08 | 高考志愿咨询系统开源版 |
| [`Zhangxuefeng-AI-gaokao`](https://github.com/Business-Unit-for-Gaokao/Zhangxuefeng-AI-gaokao) | public | - | 2026-06-08 | 本项目是一个基于“本地知识库 + 向量引擎(Qdrant) + 大语言模型”构建的开源高考志愿咨询系统。为打破技术壁垒，让完全不懂代码的电脑小白也能享受到 AI 的时代红利，项目在最新版本中独家加入了【傻瓜式一键配置脚手架】。用户告别了极其繁琐的环境配置，只需点击一次，电脑就会自动下载和部署包含数据库在内的全部环境。 |
| [`zhonggaokao`](https://github.com/Business-Unit-for-Gaokao/zhonggaokao) | private | HTML | 2026-06-19 | 无描述 |
| [`gaokao-teacher-package`](https://github.com/Business-Unit-for-Gaokao/gaokao-teacher-package) | private | HTML | 2026-06-24 | 无描述 |
| [`gaokao-landing`](https://github.com/Business-Unit-for-Gaokao/gaokao-landing) | private | HTML | 2026-06-10 | 高考宣传页 |
| [`invite`](https://github.com/Business-Unit-for-Gaokao/invite) | private | CSS | 2026-06-20 | 高考志愿填报邀请码 H5 |
| [`pay`](https://github.com/Business-Unit-for-Gaokao/pay) | private | JavaScript | 2026-06-15 | 无描述 |

## 爬虫、工具、数据产品与辅助仓库

| Repository | Visibility | Language | Updated | Purpose / Notes |
| --- | --- | --- | --- | --- |
| [`xuezhipingtai`](https://github.com/Business-Unit-for-Gaokao/xuezhipingtai) | public | HTML | 2026-07-01 | 学职平台独立爬虫：专业与职业数据采集 |
| [`sunshinegaokao`](https://github.com/Business-Unit-for-Gaokao/sunshinegaokao) | public | Python | 2026-07-01 | 阳光高考 / CHSI crawler |
| [`zhangshanggaokao`](https://github.com/Business-Unit-for-Gaokao/zhangshanggaokao) | public | Python | 2026-07-01 | 掌上高考 crawler factory |
| [`codegen-bot`](https://github.com/Business-Unit-for-Gaokao/codegen-bot) | public | Java | 2026-07-01 | Code generation helper scripts for gaokao projects |
| [`gaokao-plans-crawler`](https://github.com/Business-Unit-for-Gaokao/gaokao-plans-crawler) | public | Python | 2026-07-01 | Generated crawler repo for plans |
| [`gaokao-scheduler`](https://github.com/Business-Unit-for-Gaokao/gaokao-scheduler) | private | Python | 2026-06-09 | 无描述 |
| [`gaokao-tool`](https://github.com/Business-Unit-for-Gaokao/gaokao-tool) | private | Python | 2026-06-10 | 无描述 |
| [`gaokao-universities-data`](https://github.com/Business-Unit-for-Gaokao/gaokao-universities-data) | private | Shell | 2026-06-10 | 全国2919所高校基础数据库 + 详情采集器 + 小红书内容生成器 |
| [`gaokao-salary`](https://github.com/Business-Unit-for-Gaokao/gaokao-salary) | public | JavaScript | 2026-06-09 | 高考专业薪资 |
| [`ai-gaokao-jobs-china`](https://github.com/Business-Unit-for-Gaokao/ai-gaokao-jobs-china) | public | Python | 2026-06-16 | 高考专业AI工作替代率 |
| [`Front_Node_Code`](https://github.com/Business-Unit-for-Gaokao/Front_Node_Code) | private | TypeScript | 2026-06-28 | 无描述 |
| [`python_for_gaokao`](https://github.com/Business-Unit-for-Gaokao/python_for_gaokao) | private | - | 2026-06-09 | 无描述 |
| [`yangguanggaokao`](https://github.com/Business-Unit-for-Gaokao/yangguanggaokao) | public | HTML | 2026-07-01 | 阳光高考专业信息爬虫 - 爬取高校专业目录、详细介绍、开设院校等数据 |

## 其他 live 仓库

_当前无 live 仓库。_

## Live 仓库完整清单

| Repository | Visibility | Language | Updated | Purpose / Notes |
| --- | --- | --- | --- | --- |
| [`.github`](https://github.com/Business-Unit-for-Gaokao/.github) | public | - | 2026-07-03 | Business-Unit-for-Gaokao organization profile and repository map |
| [`ai-gaokao-jobs-china`](https://github.com/Business-Unit-for-Gaokao/ai-gaokao-jobs-china) | public | Python | 2026-06-16 | 高考专业AI工作替代率 |
| [`codegen-bot`](https://github.com/Business-Unit-for-Gaokao/codegen-bot) | public | Java | 2026-07-01 | Code generation helper scripts for gaokao projects |
| [`deploy`](https://github.com/Business-Unit-for-Gaokao/deploy) | private | - | 2026-07-01 | Business-Unit-for-Gaokao deployment and operations |
| [`Front_Node_Code`](https://github.com/Business-Unit-for-Gaokao/Front_Node_Code) | private | TypeScript | 2026-06-28 | 无描述 |
| [`future-deploy`](https://github.com/Business-Unit-for-Gaokao/future-deploy) | private | Shell | 2026-07-01 | 自动化部署项目：Docker Compose 编排 Redis、MySQL 及前后端服务部署 |
| [`future-exam-uniapp`](https://github.com/Business-Unit-for-Gaokao/future-exam-uniapp) | private | Vue | 2026-06-27 | FutureTech线上考试uniapp端 |
| [`gaokao-data-json`](https://github.com/Business-Unit-for-Gaokao/gaokao-data-json) | private | - | 2026-07-01 | Gaokao JSON data snapshots consolidated from crawler repositories |
| [`gaokao-knowledge-base`](https://github.com/Business-Unit-for-Gaokao/gaokao-knowledge-base) | private | Python | 2026-07-03 | 高考志愿咨询 Obsidian 知识库 |
| [`gaokao-landing`](https://github.com/Business-Unit-for-Gaokao/gaokao-landing) | private | HTML | 2026-06-10 | 高考宣传页 |
| [`gaokao-plans-crawler`](https://github.com/Business-Unit-for-Gaokao/gaokao-plans-crawler) | public | Python | 2026-07-01 | Generated crawler repo for plans |
| [`gaokao-salary`](https://github.com/Business-Unit-for-Gaokao/gaokao-salary) | public | JavaScript | 2026-06-09 | 高考专业薪资 |
| [`gaokao-scheduler`](https://github.com/Business-Unit-for-Gaokao/gaokao-scheduler) | private | Python | 2026-06-09 | 无描述 |
| [`gaokao-teacher-package`](https://github.com/Business-Unit-for-Gaokao/gaokao-teacher-package) | private | HTML | 2026-06-24 | 无描述 |
| [`gaokao-tool`](https://github.com/Business-Unit-for-Gaokao/gaokao-tool) | private | Python | 2026-06-10 | 无描述 |
| [`gaokao-universities-data`](https://github.com/Business-Unit-for-Gaokao/gaokao-universities-data) | private | Shell | 2026-06-10 | 全国2919所高校基础数据库 + 详情采集器 + 小红书内容生成器 |
| [`gaokao-volunteer-bot`](https://github.com/Business-Unit-for-Gaokao/gaokao-volunteer-bot) | private | JavaScript | 2026-06-25 | Gaokao volunteer application chatbot with Playwright data collection |
| [`gaokao-zhiyuan-consulting-system-open`](https://github.com/Business-Unit-for-Gaokao/gaokao-zhiyuan-consulting-system-open) | private | JavaScript | 2026-06-08 | 高考志愿咨询系统开源版 |
| [`infromation`](https://github.com/Business-Unit-for-Gaokao/infromation) | private | Python | 2026-07-03 | 无描述 |
| [`invite`](https://github.com/Business-Unit-for-Gaokao/invite) | private | CSS | 2026-06-20 | 高考志愿填报邀请码 H5 |
| [`multi-services-platform`](https://github.com/Business-Unit-for-Gaokao/multi-services-platform) | private | Java | 2026-07-01 | FutureTechJava后端 |
| [`pay`](https://github.com/Business-Unit-for-Gaokao/pay) | private | JavaScript | 2026-06-15 | 无描述 |
| [`python_for_gaokao`](https://github.com/Business-Unit-for-Gaokao/python_for_gaokao) | private | - | 2026-06-09 | 无描述 |
| [`requirements`](https://github.com/Business-Unit-for-Gaokao/requirements) | private | - | 2026-07-03 | Business-Unit-for-Gaokao business/product requirements |
| [`sunshinegaokao`](https://github.com/Business-Unit-for-Gaokao/sunshinegaokao) | public | Python | 2026-07-01 | 阳光高考 / CHSI crawler |
| [`uni-app-gaokao`](https://github.com/Business-Unit-for-Gaokao/uni-app-gaokao) | private | Vue | 2026-06-09 | FutureTech高考uniapp端 |
| [`xuezhipingtai`](https://github.com/Business-Unit-for-Gaokao/xuezhipingtai) | public | HTML | 2026-07-01 | 学职平台独立爬虫：专业与职业数据采集 |
| [`yangguanggaokao`](https://github.com/Business-Unit-for-Gaokao/yangguanggaokao) | public | HTML | 2026-07-01 | 阳光高考专业信息爬虫 - 爬取高校专业目录、详细介绍、开设院校等数据 |
| [`zhangshanggaokao`](https://github.com/Business-Unit-for-Gaokao/zhangshanggaokao) | public | Python | 2026-07-01 | 掌上高考 crawler factory |
| [`Zhangxuefeng-AI-gaokao`](https://github.com/Business-Unit-for-Gaokao/Zhangxuefeng-AI-gaokao) | public | - | 2026-06-08 | 本项目是一个基于“本地知识库 + 向量引擎(Qdrant) + 大语言模型”构建的开源高考志愿咨询系统。为打破技术壁垒，让完全不懂代码的电脑小白也能享受到 AI 的时代红利，项目在最新版本中独家加入了【傻瓜式一键配置脚手架】。用户告别了极其繁琐的环境配置，只需点击一次，电脑就会自动下载和部署包含数据库在内的全部环境。 |
| [`zhonggaokao`](https://github.com/Business-Unit-for-Gaokao/zhonggaokao) | private | HTML | 2026-06-19 | 无描述 |

---

_Last updated: 2026-07-03; live inventory: 31 repositories._
