# Business-Unit-for-Gaokao Repository Map

本文记录 `Business-Unit-for-Gaokao` 当前仓库用途、边界和维护原则。仓库清单基于 GitHub API 于 2026-07-01 回读确认，当前组织共 40 个仓库；其中爬虫仓库按“学职、阳光高考、掌上高考”三条主线收敛，JSON 数据统一归档到 `gaokao-data-json`。

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

## 数据采集、爬虫与数据仓库

### 当前保留主仓库

| Repository | Visibility | Role | Purpose / Notes |
| --- | --- | --- | --- |
| `xuezhi-platform-crawler` | public | 学职平台爬虫 | 学职平台独立爬虫主仓库；只面向 `xz.chsi.com.cn` 的专业与职业数据采集 |
| `sunshine-gaokao-scraper` | public | 阳光高考爬虫 | 阳光高考 / CHSI 专业、院校、开设院校等数据采集主仓库 |
| `gaokao-crawler` | public | 掌上高考爬虫 | 掌上高考统一爬虫入口；承接招生计划、分数线、专业、就业、院系、强基、院校分数等采集逻辑 |
| `gaokao-data-json` | private | JSON 数据仓库 | 集中归档从历史爬虫仓库迁出的 JSON、schema、manifest、清洗后结果和数据说明；不放爬虫逻辑 |

### 删除前需迁移 JSON 数据的仓库

| Repository | Visibility | Target | Notes |
| --- | --- | --- | --- |
| `gaokao-plans-crawler` | public | `gaokao-data-json` + `gaokao-crawler` | 掌上高考招生计划数据；JSON 迁入数据仓库，采集逻辑并入掌上高考主爬虫 |
| `gaokao-scores-crawler` | public | `gaokao-data-json` + `gaokao-crawler` | 掌上高考分数线数据；JSON 迁入数据仓库，采集逻辑并入掌上高考主爬虫 |
| `gaokao-jobs-crawler` | public | `gaokao-data-json` + `gaokao-crawler` | 掌上高考就业 / 职业数据；JSON 迁入数据仓库，采集逻辑并入掌上高考主爬虫 |
| `gaokao-special-crawler` | public | `gaokao-data-json` + `gaokao-crawler` | 掌上高考专业 / special 数据；JSON 迁入数据仓库，采集逻辑并入掌上高考主爬虫 |
| `gaokao-department-crawler` | public | `gaokao-data-json` + `gaokao-crawler` | 掌上高考院系 / 专业组数据；JSON 迁入数据仓库，采集逻辑并入掌上高考主爬虫 |
| `gaokao-qiangji-crawler` | public | `gaokao-data-json` + `gaokao-crawler` | 掌上高考强基计划数据；JSON 迁入数据仓库，采集逻辑并入掌上高考主爬虫 |
| `gaokao-school-scores-crawler` | public | `gaokao-data-json` + `gaokao-crawler` | 掌上高考院校分数数据；JSON 迁入数据仓库，采集逻辑并入掌上高考主爬虫 |
| `gaokao-xuezhi-crawler` | public | `gaokao-data-json` + 三个主爬虫 | 历史混合仓库，包含阳光高考 / CHSI、学职平台等内容；数据迁出后删除 |
| `xuezhi-gaokao-crawler` | public | `gaokao-data-json` + `xuezhi-platform-crawler` / `sunshine-gaokao-scraper` | Legacy CHSI / 学职相关仓库；数据迁出后删除 |
| `clawer` | public | `gaokao-data-json` + `xuezhi-platform-crawler` / `sunshine-gaokao-scraper` | 历史爬虫框架，包含 CHSI 和学职数据；数据迁出后删除 |
| `gaokao-collection` | public | `gaokao-data-json` / 业务工具仓库 | 高考信息收集脚本；若只剩 seeds/config 数据则归档后删除 |
| `gaokao-crawler-factory` | public | 三个主爬虫 / Platform 工具 | 爬虫工厂管理项目；如无继续生成需求，删除或迁出通用能力 |
| `ai-gaokao-jobs-china` | public | `gaokao-data-json` | 高考专业 AI 工作替代率数据与静态输出；JSON/派生结果迁入 `derived/` 后删除 |
| `gaokao-salary` | public | `gaokao-data-json` | 专业薪资 JSON / 静态输出；数据迁入 `derived/` 后删除 |
| `gaokao-universities-data` | private | `gaokao-data-json` | 高校基础库、专业库、详情结果等 JSON 数据；迁入 `universities/` 后删除 |

## 第三方 / 参考项目

| Repository | Visibility | Purpose / Notes |
| --- | --- | --- |
| `Zhangxuefeng-AI-gaokao` | public | 基于本地知识库、Qdrant 和大模型的开源高考志愿咨询系统参考项目 |

## 已删除 / 不再维护

| Repository | Status | Notes |
| --- | --- | --- |
| - | - | 当前尚未实际删除；上方“删除前需迁移 JSON 数据的仓库”是待清理清单。 |

## 删除执行原则

1. 先把待删仓库中的 `.json`、`.jsonl`、schema、manifest、必要 README 数据说明迁入 `gaokao-data-json`。
2. 再把仍需运行的采集逻辑分别并入三个主爬虫：`xuezhi-platform-crawler`、`sunshine-gaokao-scraper`、`gaokao-crawler`。
3. 验证数据可读、JSON 可解析、主爬虫入口存在后，再删除历史仓库。
4. 删除完成后再次回读 GitHub live inventory，并把本文“待清理清单”移动到“已删除 / 不再维护”。

## 维护流程

1. 更新前先用 GitHub API 回读组织当前仓库清单。
2. 仓库删除、迁移、改名后，同步更新本文和 `profile/README.md`。
3. 对只改 README/docs 的轻量更新，可以直接维护 `main`。
4. 代码、部署、CI、架构性变更优先走分支和 PR。
5. 不提交 token、密码、SSH key、服务器凭据、客户隐私和未授权数据。
