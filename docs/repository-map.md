# Business-Unit-for-Gaokao Repository Map

本文记录 `Business-Unit-for-Gaokao` 当前仓库用途、边界和维护原则。仓库清单基于 GitHub API 于 2026-07-01 回读确认，当前组织共 **33** 个仓库。已删除的历史爬虫仓库不再列入当前库存；保留的爬虫能力收敛到“学职平台、阳光高考、掌上高考”三条主线，JSON 数据统一归档到 `gaokao-data-json`。

## 组织边界

`Business-Unit-for-Gaokao` 承载高考志愿填报、数据采集、知识库、咨询交付、线上服务和相关部署编排。

- 具体业务代码、业务数据资产、业务专属知识库：留在本组织。
- 业务需求、MVP、工作流和未决问题：进入 `requirements`。
- 部署、域名、CI/CD、环境映射和运维说明：进入标准 `deploy`，既有部署资产可继续由 `future-deploy` 承接。
- 通用平台底座、跨 BU clone-bot 和通用 codegen 能力：归 `Business-Unit-for-Platform`。
- 集团级战略、组合管理、制度和跨 BU 治理：归 `President-Office`。

## 开发 / 部署分离原则

- 应用开发仓库只负责：源代码、构建、测试、打包、开发说明。
- 部署仓库或独立部署流程负责：服务器发布、Nginx、域名、证书、DNS、Pages、Cloudflare、生产环境编排。
- 不要把生产发布逻辑塞进业务开发仓库；需要发布时由部署仓库消费构建产物或明确版本。
- 部署默认走 GitHub Actions/CI，不手动 SSH；密钥只放 GitHub Actions secrets，不写入仓库。

## 当前三条代表爬虫线

| Repository | Visibility | Language | Purpose / Notes |
| --- | --- | --- | --- |
| [`xuezhipingtai`](https://github.com/Business-Unit-for-Gaokao/xuezhipingtai) | public | HTML | 学职平台 / XZ 代表爬虫仓库，面向 `xz.chsi.com.cn` 的专业与职业数据采集。 |
| [`sunshinegaokao`](https://github.com/Business-Unit-for-Gaokao/sunshinegaokao) | public | Python | 阳光高考 / CHSI 代表爬虫仓库。 |
| [`zhangshanggaokao`](https://github.com/Business-Unit-for-Gaokao/zhangshanggaokao) | public | Python | 掌上高考 / gaokao.cn 代表爬虫仓库；已合并 department、jobs、special、qiangji 等爬虫源码，并记录 scores/provinceline 后续归并计划。 |

## JSON 数据仓库

| Repository | Visibility | Language | Purpose / Notes |
| --- | --- | --- | --- |
| [`gaokao-data-json`](https://github.com/Business-Unit-for-Gaokao/gaokao-data-json) | private | - | 从历史爬虫仓库集中迁移出的 JSON、schema、manifest、清洗后结果和数据说明；不放爬虫业务逻辑。 |

## 仍在组织内、需要后续判断/归并的爬虫或重复仓库

这些仓库当前仍存在于组织内。清理前应先确认是否还有独特源码；历史 JSON 不重复搬入代表爬虫仓库，应归档在 `gaokao-data-json`。

| Repository | Visibility | Language | Purpose / Notes |
| --- | --- | --- | --- |
| [`gaokao-plans-crawler`](https://github.com/Business-Unit-for-Gaokao/gaokao-plans-crawler) | public | Python | 仍在组织内的掌上高考招生计划历史/生成爬虫仓库；清理前需确认源码是否已归并到 `zhangshanggaokao`，历史 JSON 归档在 `gaokao-data-json`。 |
| [`yangguang-gaokao-scraper`](https://github.com/Business-Unit-for-Gaokao/yangguang-gaokao-scraper) | public | HTML | 仍在组织内的阳光高考旧/重复 scraper；清理前需确认是否有独特源码需要并入 `sunshinegaokao`。 |
| [`zhangshang-gaokao-crawler`](https://github.com/Business-Unit-for-Gaokao/zhangshang-gaokao-crawler) | public | Python | 仍在组织内的掌上高考旧/重复 crawler；清理前需确认是否有独特源码需要并入 `zhangshanggaokao`。 |

## 核心业务应用

| Repository | Visibility | Language | Purpose / Notes |
| --- | --- | --- | --- |
| [`multi-services-platform`](https://github.com/Business-Unit-for-Gaokao/multi-services-platform) | private | Java | 高考业务 Java 后端 / 多服务平台。 |
| [`future-exam-uniapp`](https://github.com/Business-Unit-for-Gaokao/future-exam-uniapp) | private | Vue | FutureTech 线上考试 / 高考业务 UniApp 端。 |
| [`uni-app-gaokao`](https://github.com/Business-Unit-for-Gaokao/uni-app-gaokao) | private | Vue | FutureTech 高考 UniApp 端。 |
| [`gaokao-volunteer-bot`](https://github.com/Business-Unit-for-Gaokao/gaokao-volunteer-bot) | private | JavaScript | 高考志愿填报 AI 机器人。 |
| [`gaokao-zhiyuan-consulting-system-open`](https://github.com/Business-Unit-for-Gaokao/gaokao-zhiyuan-consulting-system-open) | private | JavaScript | 高考志愿咨询系统相关资产。 |
| [`zhonggaokao`](https://github.com/Business-Unit-for-Gaokao/zhonggaokao) | private | HTML | 中高考相关 AI / 知识库资产。 |

## 部署、调度与开发工具

| Repository | Visibility | Language | Purpose / Notes |
| --- | --- | --- | --- |
| [`deploy`](https://github.com/Business-Unit-for-Gaokao/deploy) | private | - | 标准部署与运维入口；记录部署编排、域名、CI/CD、环境映射和运维说明。 |
| [`future-deploy`](https://github.com/Business-Unit-for-Gaokao/future-deploy) | private | Shell | 高考业务既有独立部署仓库；承载部署、域名、服务器发布等运维逻辑。 |
| [`gaokao-scheduler`](https://github.com/Business-Unit-for-Gaokao/gaokao-scheduler) | private | Python | 高考业务调度相关服务。 |
| [`codegen-bot`](https://github.com/Business-Unit-for-Gaokao/codegen-bot) | public | Java | 高考业务代码生成辅助脚本。 |

## 数据、知识库与运营资料

| Repository | Visibility | Language | Purpose / Notes |
| --- | --- | --- | --- |
| [`requirements`](https://github.com/Business-Unit-for-Gaokao/requirements) | private | - | 高考业务需求、MVP、工作流、未决问题标准入口。 |
| [`gaokao`](https://github.com/Business-Unit-for-Gaokao/gaokao) | private | - | 高考运营信息。 |
| [`gaokao-knowledge-base`](https://github.com/Business-Unit-for-Gaokao/gaokao-knowledge-base) | private | Python | 高考志愿咨询 Obsidian 知识库。 |
| [`gaokao-data-json`](https://github.com/Business-Unit-for-Gaokao/gaokao-data-json) | private | - | 从历史爬虫仓库集中迁移出的 JSON 数据快照仓库。 |
| [`gaokao-universities-data`](https://github.com/Business-Unit-for-Gaokao/gaokao-universities-data) | private | Shell | 高校基础数据库、详情采集器和内容生成相关资产。 |
| [`infromation`](https://github.com/Business-Unit-for-Gaokao/infromation) | private | Python | 高考业务信息资料仓库（现有仓库名保留）。 |
| [`python_for_gaokao`](https://github.com/Business-Unit-for-Gaokao/python_for_gaokao) | private | - | 高考 Python 工具 / 脚本资产。 |

## Pages、宣传页、交付与参考项目

| Repository | Visibility | Language | Purpose / Notes |
| --- | --- | --- | --- |
| [`gaokao-salary`](https://github.com/Business-Unit-for-Gaokao/gaokao-salary) | public | JavaScript | 高考专业薪资 Pages / 静态展示资产，保留。 |
| [`ai-gaokao-jobs-china`](https://github.com/Business-Unit-for-Gaokao/ai-gaokao-jobs-china) | public | Python | 高考专业 AI 工作替代率 Pages / 静态展示资产，保留。 |
| [`gaokao-landing`](https://github.com/Business-Unit-for-Gaokao/gaokao-landing) | private | HTML | 高考宣传页。 |
| [`gaokao-teacher-package`](https://github.com/Business-Unit-for-Gaokao/gaokao-teacher-package) | private | HTML | 高考老师 / 交付资料包相关资产。 |
| [`invite`](https://github.com/Business-Unit-for-Gaokao/invite) | private | CSS | 高考志愿填报邀请码 H5。 |
| [`pay`](https://github.com/Business-Unit-for-Gaokao/pay) | private | JavaScript | 高考业务支付相关服务。 |
| [`Front_Node_Code`](https://github.com/Business-Unit-for-Gaokao/Front_Node_Code) | private | TypeScript | 前端 / Node 相关遗留或辅助资产。 |
| [`gaokao-tool`](https://github.com/Business-Unit-for-Gaokao/gaokao-tool) | private | Python | 高考工具类仓库。 |
| [`Zhangxuefeng-AI-gaokao`](https://github.com/Business-Unit-for-Gaokao/Zhangxuefeng-AI-gaokao) | public | - | 基于本地知识库、Qdrant 和大模型的开源高考志愿咨询系统参考项目。 |

## 当前完整实时库存

| Repository | Visibility | Archived | Language | Pushed at | Description |
| --- | --- | --- | --- | --- | --- |
| [`.github`](https://github.com/Business-Unit-for-Gaokao/.github) | public | false | - | 2026-07-01T10:49:31Z | Business-Unit-for-Gaokao organization profile and repository map |
| [`ai-gaokao-jobs-china`](https://github.com/Business-Unit-for-Gaokao/ai-gaokao-jobs-china) | public | false | Python | 2026-06-16T23:09:56Z | 高考专业AI工作替代率 |
| [`codegen-bot`](https://github.com/Business-Unit-for-Gaokao/codegen-bot) | public | false | Java | 2026-07-01T02:27:51Z | Code generation helper scripts for gaokao projects |
| [`deploy`](https://github.com/Business-Unit-for-Gaokao/deploy) | private | false | - | 2026-07-01T10:49:42Z | Business-Unit-for-Gaokao deployment and operations |
| [`Front_Node_Code`](https://github.com/Business-Unit-for-Gaokao/Front_Node_Code) | private | false | TypeScript | 2026-06-28T02:02:14Z |  |
| [`future-deploy`](https://github.com/Business-Unit-for-Gaokao/future-deploy) | private | false | Shell | 2026-07-01T02:03:42Z | 自动化部署项目：Docker Compose 编排 Redis、MySQL 及前后端服务部署 |
| [`future-exam-uniapp`](https://github.com/Business-Unit-for-Gaokao/future-exam-uniapp) | private | false | Vue | 2026-06-27T15:22:42Z | FutureTech线上考试uniapp端 |
| [`gaokao`](https://github.com/Business-Unit-for-Gaokao/gaokao) | private | false | - | 2026-06-27T11:31:43Z | 高考运营信息 |
| [`gaokao-data-json`](https://github.com/Business-Unit-for-Gaokao/gaokao-data-json) | private | false | - | 2026-07-01T06:04:52Z | Gaokao JSON data snapshots consolidated from crawler repositories |
| [`gaokao-knowledge-base`](https://github.com/Business-Unit-for-Gaokao/gaokao-knowledge-base) | private | false | Python | 2026-07-01T04:16:34Z | 高考志愿咨询 Obsidian 知识库 |
| [`gaokao-landing`](https://github.com/Business-Unit-for-Gaokao/gaokao-landing) | private | false | HTML | 2026-06-10T09:07:51Z | 高考宣传页 |
| [`gaokao-plans-crawler`](https://github.com/Business-Unit-for-Gaokao/gaokao-plans-crawler) | public | false | Python | 2026-07-01T02:03:41Z | Generated crawler repo for plans |
| [`gaokao-salary`](https://github.com/Business-Unit-for-Gaokao/gaokao-salary) | public | false | JavaScript | 2026-04-12T16:50:54Z | 高考专业薪资 |
| [`gaokao-scheduler`](https://github.com/Business-Unit-for-Gaokao/gaokao-scheduler) | private | false | Python | 2026-06-02T22:12:05Z |  |
| [`gaokao-teacher-package`](https://github.com/Business-Unit-for-Gaokao/gaokao-teacher-package) | private | false | HTML | 2026-06-29T09:09:13Z |  |
| [`gaokao-tool`](https://github.com/Business-Unit-for-Gaokao/gaokao-tool) | private | false | Python | 2026-06-10T13:10:03Z |  |
| [`gaokao-universities-data`](https://github.com/Business-Unit-for-Gaokao/gaokao-universities-data) | private | false | Shell | 2026-06-10T15:51:04Z | 全国2919所高校基础数据库 + 详情采集器 + 小红书内容生成器 |
| [`gaokao-volunteer-bot`](https://github.com/Business-Unit-for-Gaokao/gaokao-volunteer-bot) | private | false | JavaScript | 2026-06-25T05:15:16Z | Gaokao volunteer application chatbot with Playwright data collection |
| [`gaokao-zhiyuan-consulting-system-open`](https://github.com/Business-Unit-for-Gaokao/gaokao-zhiyuan-consulting-system-open) | private | false | JavaScript | 2026-06-06T13:32:56Z | 高考志愿咨询系统开源版 |
| [`infromation`](https://github.com/Business-Unit-for-Gaokao/infromation) | private | false | Python | 2026-07-01T06:44:43Z |  |
| [`invite`](https://github.com/Business-Unit-for-Gaokao/invite) | private | false | CSS | 2026-06-11T09:40:48Z | 高考志愿填报邀请码 H5 |
| [`multi-services-platform`](https://github.com/Business-Unit-for-Gaokao/multi-services-platform) | private | false | Java | 2026-07-01T05:39:05Z | FutureTechJava后端 |
| [`pay`](https://github.com/Business-Unit-for-Gaokao/pay) | private | false | JavaScript | 2026-06-15T09:55:17Z |  |
| [`python_for_gaokao`](https://github.com/Business-Unit-for-Gaokao/python_for_gaokao) | private | false | - | 2026-06-01T00:26:29Z |  |
| [`requirements`](https://github.com/Business-Unit-for-Gaokao/requirements) | private | false | - | 2026-07-01T10:49:39Z | Business-Unit-for-Gaokao business/product requirements |
| [`sunshinegaokao`](https://github.com/Business-Unit-for-Gaokao/sunshinegaokao) | public | false | Python | 2026-06-07T12:37:09Z | 阳光高考 / CHSI crawler |
| [`uni-app-gaokao`](https://github.com/Business-Unit-for-Gaokao/uni-app-gaokao) | private | false | Vue | 2026-06-09T03:22:10Z | FutureTech高考uniapp端 |
| [`xuezhipingtai`](https://github.com/Business-Unit-for-Gaokao/xuezhipingtai) | public | false | HTML | 2026-07-01T03:20:17Z | 学职平台独立爬虫：专业与职业数据采集 |
| [`yangguang-gaokao-scraper`](https://github.com/Business-Unit-for-Gaokao/yangguang-gaokao-scraper) | public | false | HTML | 2026-06-09T03:46:04Z | 阳光高考专业信息爬虫 - 爬取高校专业目录、详细介绍、开设院校等数据 |
| [`zhangshang-gaokao-crawler`](https://github.com/Business-Unit-for-Gaokao/zhangshang-gaokao-crawler) | public | false | Python | 2026-06-09T03:45:46Z | 高考数据爬取 |
| [`zhangshanggaokao`](https://github.com/Business-Unit-for-Gaokao/zhangshanggaokao) | public | false | Python | 2026-07-01T10:59:11Z | 掌上高考 crawler factory |
| [`Zhangxuefeng-AI-gaokao`](https://github.com/Business-Unit-for-Gaokao/Zhangxuefeng-AI-gaokao) | public | false | - | 2026-04-23T07:21:35Z | 本项目是一个基于“本地知识库 + 向量引擎(Qdrant) + 大语言模型”构建的开源高考志愿咨询系统。为打破技术壁垒，让完全不懂代码的电脑小白也能享受到 AI 的时代红利，项目在最新版本中独家加入了【傻瓜式一键配置脚手架】。用户告别了极其繁琐的环境配置，只需点击一次，电脑就会自动下载和部署包含数据库在内的全部环境。 |
| [`zhonggaokao`](https://github.com/Business-Unit-for-Gaokao/zhonggaokao) | private | false | HTML | 2026-06-27T15:48:04Z |  |

## 已删除 / 当前不在组织库存中的历史仓库

以下仓库名基于本次 GitHub API 实时库存确认，当前不在 `Business-Unit-for-Gaokao` 组织仓库列表中。

| Repository | Current status | Notes |
| --- | --- | --- |
| `gaokao-collection` | absent from live inventory | 历史信息采集脚手架/清理对象；如需恢复，请从代表仓库或 GitHub 删除恢复流程确认来源。 |
| `gaokao-department-crawler` | absent from live inventory | 源码已并入 `zhangshanggaokao`，历史 JSON 位于 `gaokao-data-json`。 |
| `gaokao-jobs-crawler` | absent from live inventory | 源码已并入 `zhangshanggaokao`，历史 JSON 位于 `gaokao-data-json`。 |
| `gaokao-special-crawler` | absent from live inventory | 源码已并入 `zhangshanggaokao`，历史 JSON 位于 `gaokao-data-json`。 |
| `gaokao-qiangji-crawler` | absent from live inventory | 源码已并入 `zhangshanggaokao`，历史 JSON 位于 `gaokao-data-json` 的 `zsgk/gaokao-qiangji-crawler/data/qiangji/`。 |
| `gaokao-scores-crawler` | absent from live inventory | 不再作为独立仓库保留；`zhangshanggaokao` README 已记录 scores/provinceline 后续归并计划，历史 JSON 位于 `gaokao-data-json`。 |
| `gaokao-school-scores-crawler` | absent from live inventory | 历史爬虫/清理对象；如需恢复，请从 `gaokao-data-json`、代表爬虫仓库或 GitHub 删除恢复流程确认来源。 |
| `xuezhi-platform-crawler` | absent from live inventory | 历史学职平台仓库名；最终代表仓库是 `xuezhipingtai`。 |
| `xuezhi-gaokao-crawler` | absent from live inventory | 历史 CHSI/XZ 混合仓库；最终代表仓库为 `sunshinegaokao` / `xuezhipingtai`。 |
| `gaokao-xuezhi-crawler` | absent from live inventory | 历史混合仓库；最终代表仓库为三条爬虫线。 |
| `clawer` | absent from live inventory | 历史爬虫框架/清理对象。 |
| `gaokao-crawler-factory` | absent from live inventory | 历史爬虫工厂/清理对象。 |

## 维护流程

1. 更新前先用 GitHub API 回读组织当前仓库清单。
2. 仓库删除、迁移、改名后，同步更新本文和 `profile/README.md`。
3. 对只改 README/docs 的轻量更新，可以直接维护 `main`。
4. 代码、部署、CI、架构性变更优先走分支和 PR。
5. 不提交 token、密码、SSH key、服务器凭据、客户隐私和未授权数据。
