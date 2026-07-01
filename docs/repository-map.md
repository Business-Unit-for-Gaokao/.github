# Business-Unit-for-Gaokao Repository Map

本文记录 `Business-Unit-for-Gaokao` 当前仓库用途、边界和维护原则。仓库清单基于 GitHub API 于 2026-07-01 回读确认，当前组织共 38 个仓库。

## 组织边界

`Business-Unit-for-Gaokao` 承载高考志愿填报、数据采集、知识库、咨询交付、线上服务和相关部署编排。

- 具体业务代码、业务数据资产、业务专属知识库：留在本组织。
- 通用平台底座、跨 BU clone-bot 和通用 codegen 能力：归 `Business-Unit-for-Platform`。
- 高考业务专用工具和脚本：留在本组织；若未来抽象为通用平台能力，再迁移到 `Business-Unit-for-Platform`。
- 集团级战略、组合管理、制度和跨 BU 治理：归 `President-Office`。

## 开发 / 部署分离原则

- 应用开发仓库只负责：源代码、构建、测试、打包、开发说明。
- 部署仓库或独立部署流程负责：服务器发布、Nginx、域名、证书、DNS、Pages、Cloudflare、生产环境编排。
- 不要把生产发布逻辑塞进业务开发仓库；需要发布时由部署仓库消费构建产物或明确版本。
- 部署默认走 GitHub Actions/CI，不手动 SSH；密钥只放 GitHub Actions secrets，不写入仓库。

## 关键仓库

| Repository | Visibility | Purpose / Notes |
| --- | --- | --- |
| `.github` | public | 组织 profile 和仓库地图 |
| `multi-services-platform` | private | 高考业务 Java 后端 |
| `future-exam-uniapp` | private | FutureTech 线上考试 / 高考业务 UniApp 端 |
| `uni-app-gaokao` | private | FutureTech 高考 UniApp 端 |
| `gaokao` | private | 高考运营信息 |
| `gaokao-knowledge-base` | private | 高考志愿咨询 Obsidian 知识库 |
| `gaokao-volunteer-bot` | private | 高考志愿填报 AI 机器人 |
| `future-deploy` | private | 高考业务独立部署仓库；承载部署、域名、服务器发布等运维逻辑 |
| `zhonggaokao` | private | 中高考相关 AI / 知识库资产 |
| `gaokao-scheduler` | private | 高考业务调度相关服务 |
| `gaokao-teacher-package` | private | 高考老师 / 交付资料包相关资产 |
| `gaokao-landing` | private | 高考宣传页 |
| `invite` | private | 高考志愿填报邀请码 H5 |
| `pay` | private | 高考业务支付相关服务 |
| `infromation` | private | 高考业务信息资料仓库（现有仓库名保留） |
| `gaokao-tool` | private | 高考工具类仓库 |
| `codegen-bot` | public | 高考业务代码生成辅助脚本 |
| `gaokao-zhiyuan-consulting-system-open` | private | 高考志愿咨询系统开源版相关资产 |
| `python_for_gaokao` | private | 高考 Python 工具 / 脚本资产 |
| `Front_Node_Code` | private | 前端 / Node 相关遗留或辅助资产 |

## 数据采集与爬虫仓库

| Repository | Visibility | Purpose / Notes |
| --- | --- | --- |
| `gaokao-crawler` | public | 高考数据爬取 |
| `gaokao-crawler-factory` | public | 爬虫工厂 |
| `gaokao-universities-data` | private | 全国高校基础数据库、详情采集器、小红书内容生成器 |
| `sunshine-gaokao-scraper` | public | 阳光高考专业信息爬虫 |
| `gaokao-xuezhi-crawler` | public | 学职 / 相关数据爬取 |
| `xuezhi-gaokao-crawler` | public | Legacy CHSI 学职爬虫；从 `FutureTechQuant` 迁移 |
| `gaokao-collection` | public | 高考信息收集脚本 |
| `ai-gaokao-jobs-china` | public | 高考专业 AI 工作替代率 |
| `gaokao-salary` | public | 高考专业薪资 |
| `gaokao-plans-crawler` | public | 招生计划相关爬虫 |
| `gaokao-scores-crawler` | public | 分数线相关爬虫 |
| `gaokao-jobs-crawler` | public | 就业 / 职业相关爬虫 |
| `gaokao-special-crawler` | public | 专项数据爬虫 |
| `gaokao-department-crawler` | public | 院系 / 专业组相关爬虫 |
| `gaokao-qiangji-crawler` | public | 强基计划相关爬虫 |
| `gaokao-school-scores-crawler` | public | 院校分数相关爬虫 |
| `clawer` | public | 爬虫相关历史仓库 |

## 第三方 / 参考项目

| Repository | Visibility | Purpose / Notes |
| --- | --- | --- |
| `Zhangxuefeng-AI-gaokao` | public | 基于本地知识库、Qdrant 和大模型的开源高考志愿咨询系统参考项目 |

## 已删除 / 不再维护

| Repository | Status | Notes |
| --- | --- | --- |
| - | - | 当前无需要在仓库地图中保留的已删除仓库记录。 |

## 维护流程

1. 更新前先用 GitHub API 回读组织当前仓库清单。
2. 仓库删除、迁移、改名后，同步更新本文和 `profile/README.md`。
3. 对只改 README/docs 的轻量更新，可以直接维护 `main`。
4. 代码、部署、CI、架构性变更优先走分支和 PR。
5. 不提交 token、密码、SSH key、服务器凭据、客户隐私和未授权数据。
