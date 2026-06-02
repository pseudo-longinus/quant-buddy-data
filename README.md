# quant-buddy-data

<p align="center">
  <img src="assets/banner2.jpg" alt="quant-buddy-data" width="100%" />
</p>

<p align="center">
  <a href="README.md">中文</a> ·
  <a href="README.en.md">English</a> ·
  <a href="https://www.quantbuddy.cn">官网</a> ·
  <a href="https://tcn8bvcbyokw.feishu.cn/wiki/E1zswck3oiiJjJkP07QcmSG3nle?from=from_copylink">新手教程</a>
</p>

<p align="center">
  <a href="https://github.com/pseudo-longinus/quant-buddy-data/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/pseudo-longinus/quant-buddy-data?style=social"></a>
  <a href="https://github.com/pseudo-longinus/quant-buddy-data/blob/main/LICENSE"><img alt="License" src="https://img.shields.io/github/license/pseudo-longinus/quant-buddy-data"></a>
  <img alt="Python" src="https://img.shields.io/badge/Python-3.8%2B-blue">
  <img alt="Agent Skill" src="https://img.shields.io/badge/AI%20Agent-ready-brightgreen">
  <img alt="Market" src="https://img.shields.io/badge/A%E8%82%A1%20%7C%20%E6%B8%AF%E8%82%A1%20%7C%20%E7%BE%8E%E8%82%A1-data-orange">
</p>

> **给 AI Agent 的金融数据与云端投研计算层。**  
> 让 Claude Code、Cursor、Codex、GitHub Copilot、Windsurf 等 Agent 直接查询 A 股、港股、美股行情、估值、财务与历史序列，并在云端完成全市场公式、选股、因子、回测和图表计算。

**一句话：把你的 AI Agent 从“会写量化伪代码”升级成“能查真实金融数据、跑全市场计算、输出可复用投研任务”的工作流。**

不用写行情接口，不用清洗 CSV，不用把几千只股票的大表塞进 LLM 上下文。你用自然语言描述目标，Agent 负责理解与组织公式，quant-buddy 负责稳定取数、云端计算和返回结构化结果。

> 本项目用于金融数据分析、量化研究、策略验证和教育用途，不构成投资建议、交易建议、收益承诺或自动交易服务。

---

## 为什么是 quant-buddy-data

| 特点 | 为什么重要 |
|---|---|
| **稳定** | 自建数据管道，多源交叉比对，统一交易日、复权、代码、报告期和字段口径。适合每天重复运行的研究任务，而不是一次性网页抓取。 |
| **经济** | Agent 不需要吞下几千只股票的大表。云端先完成计算，只返回 TopN、序列、图表或统计值，日常查询和轻量筛选消耗更可控。新用户注册送 Token 包，个人研究、课程实验和策略验证都能低成本起步。 |
| **低硬件要求** | 不需要自己维护行情库、财务库、因子库、计算集群或 GPU。全市场矩阵、窗口统计、排序、回测和图表渲染在云端完成，本地只负责提出问题和接收结果。 |
| **可生产化** | 自然语言探索不是终点。Agent 确认后的公式可以沉淀为固定任务，接入个人 Python、Node.js 后端、HTML 看板、定时脚本或团队机器人。 |

quant-buddy-data 把“数据 + 计算”从 LLM 上下文里拿出来，交给专门的云端投研引擎，让 Agent 专心理解问题、组织公式和解释结果。

---

## 30 秒看懂它能干什么

把下面任意一句复制给你的 Agent：

```text
查贵州茅台最新收盘价、涨跌幅、PE、PB。
```

```text
对比苹果、英伟达、特斯拉最近 20 个交易日涨跌幅，画一张净值对比图。
```

```text
筛选全 A 股中低 PE、高 ROE、近 20 日涨幅靠前的股票，返回前 30 名。
```

```text
今天 14:30 刷新一次全 A 股，找出突破 60 日新高且成交额超过 20 日均值 2 倍的前 30 只。
```

```text
把刚才验证通过的选股逻辑整理成可复用 JSON，我要放进自己的 Python 定时任务里。
```

Agent 不需要把全市场原始大表读进上下文。大规模计算在 quant-buddy 云端完成，最后只把 TopN、序列、统计值、CSV 或图表返回给你。

---

## 3 秒快速安装

如果你已经在使用 Claude Code、Cursor、Codex、GitHub Copilot、Windsurf、OpenClaw 等 Agent 工具，可以直接对 Agent 说：

```text
帮我安装这个 skill：
```

```bash
npx skills add pseudo-longinus/quant-buddy-data -g -a claude-code -s quant-buddy-skill -y
```

如果你的工具不是 Claude Code，把 `-a claude-code` 替换成对应 Agent 名称，或按你的 skills 工具说明安装。

不熟悉 Agent 和 skill 的用户，可以按[小白图文教程](https://tcn8bvcbyokw.feishu.cn/wiki/E1zswck3oiiJjJkP07QcmSG3nle?from=from_copylink)一步步展开。

首次使用前配置 API Key：

```text
帮我配置 APIkey：sk-xxxxxxxx
```

自建 Python、Node.js 或网站后端调用时，推荐使用环境变量，不要把 Key 写进代码仓库或浏览器：

```bash
QUANT_BUDDY_API_KEY=sk-xxxxxxxx
QUANT_BUDDY_ENDPOINT=https://www.quantbuddy.cn/skill
```

---

## 谁最适合 Star 这个项目

| 你是谁 | 你现在的痛点 | quant-buddy-data 给你的结果 |
|---|---|---|
| **AI Agent 重度用户** | Claude/Cursor/Codex 能写代码，但拿不到稳定金融数据，只会写伪代码 | 给 Agent 装一个可复用的金融数据后端，直接查数、筛选、画图 |
| **A 股量化研究员 / 个人研究者** | 字段、复权、交易日、报告期、股票代码、全市场矩阵都要自己处理 | 用自然语言生成公式，在云端跑全 A 筛选、因子和回测 |
| **投研自动化开发者** | 盘中筛选、盘后复盘、个人看板每天都要重复跑 | 把验证过的公式固化成 JSON，接入 Python、Node 后端、cron、GitHub Actions |
| **金融数据分析师 / 内容创作者** | 做表格和图表要反复找网页、复制数据、清洗格式 | 快速生成涨跌幅对比、行业聚合、创新高股票池、净值曲线 |
| **学生 / 教师 / 课程实验** | 不想为课程作业、论文探索、因子实验搭行情库和财务库 | 用低硬件门槛完成数据查询、策略验证和可视化 |
| **小团队 / 社群运营者** | 每天想自动发选股列表、复盘表、图表到群里 | 将固定公式接入飞书、企业微信、内部网页或团队机器人 |

不适合：期待自动下单、收益承诺、个性化投资建议，或需要完全自建底层行情/财务数据管道的用户。

---

## 为什么不是“又一个行情 API”

普通行情 API 解决的是“把数据拉出来”。真实投研里更麻烦的是：

- 字段名、报告期、复权、交易日、股票代码和市场口径怎么统一？
- 几千只股票的 20 日收益、60 日高点、成交额均值、行业聚合、TopN 排序在哪里算？
- Agent 能不能只拿最终结果，而不是把全市场大表塞进上下文？
- 今天调好的选股逻辑，明天 14:30 能不能自动再跑一遍？
- 验证后的公式，能不能放进 Python、网页后端或团队机器人？

quant-buddy-data 的定位是：

```text
AI Agent 负责理解目标和组织公式
quant-buddy 负责稳定数据、云端计算和结构化返回
你的程序只读取最终结果
```

| 维度 | 传统数据 API | 手工 CSV / 网页复制 | quant-buddy-data |
|---|---|---|---|
| 输入方式 | 记接口和字段 | 手动搜索、下载、整理 | 自然语言交给 Agent |
| 全市场计算 | 本地自己写 | 基本不可重复 | 云端公式、筛选、排序、回测 |
| LLM 上下文消耗 | 容易塞大表 | 高且混乱 | 只返回 TopN、序列、图表或统计值 |
| 复用方式 | 自己封装任务 | 难以自动化 | 公式包、后端 registry、定时任务 |
| 最佳场景 | 拉原始数据 | 一次性查表 | Agent 投研、选股、因子、复盘、看板 |

---

## 核心能力

| 能力 | 你可以问什么 |
|---|---|
| 最新行情 | 最新价、收盘价、涨跌幅、成交额、成交量、换手率 |
| 估值数据 | PE、PB、PS、股息率、市值 |
| 财务数据 | 营收、净利润、归母净利润、ROE、总资产、资产负债率 |
| 时间序列 | 最近 N 个交易日价格、收益、成交额、窗口最高价/最低价 |
| 区间对比 | 多资产固定区间累计涨跌幅、相对强弱、净值对比 |
| 全市场筛选 | 条件筛选、TopN 排序、掩码过滤、行业聚合 |
| 公式计算 | 均线、涨跌幅、窗口统计、复合因子、事件窗口 |
| 策略回测 | 组合信号、基准比较、净值曲线、持仓期对比 |
| CSV 导出 | 将历史序列、筛选结果或计算结果保存到本地 |
| 图表渲染 | K 线、折线、净值、柱状、策略对比图 |

## 数据覆盖

| 市场 | 行情 | 估值 | 财务 | 进阶分析 |
|---|---|---|---|---|
| A 股 | 支持 | 支持 | 支持 | 支持 |
| 港股 | 支持 | 部分支持 | 部分支持 | 以数据查询为主 |
| 美股 | 支持 | 部分支持 | 部分支持 | 以数据查询为主 |
| 指数 | 支持 | 部分支持 | - | 可作为基准或对比对象 |

港股、美股的估值和财务字段以接口实际返回为准。涉及交易决策前，请自行核验数据口径、更新时点、风险暴露、交易成本、滑点和合规要求。

---

## 真实场景：从一句话到每天自动运行

| 场景 | 一句话需求 | 最终产出 |
|---|---|---|
| 日常快速查数 | “查宁德时代最近报告期营收、净利润、ROE、资产负债率” | 结构化表格 |
| 盘中选股刷新 | “14:30 找突破 60 日新高且成交额放量的前 30 只” | TopN 股票池 |
| 盘后复盘 | “输出今日强势股、行业分布、成交额和涨跌幅图表” | 表格 + 图表 |
| 策略想法验证 | “低 PE + 高 ROE + 动量改善，回测相对沪深 300” | 净值曲线 + 回测指标 |
| 个人投研看板 | “把这个筛选条件做成网站后端 API” | 后端接口 + 前端展示 |
| 内容创作 | “生成近 20 日苹果/英伟达/特斯拉涨跌幅对比图” | 图表 + 简短解读 |

---

## Agent 工作流：探索、验证、固化、生产

推荐把投研过程分成四步：

| 阶段 | 你做什么 | Agent 和 quant-buddy 做什么 |
|---|---|---|
| 探索 | 用自然语言描述想法 | Agent 确认字段口径，生成公式，quant-buddy 云端计算 |
| 验证 | 追问、改条件、看结果 | Agent 调整参数，比较筛选、回测和图表结果 |
| 固化 | 要求 Agent 输出公式包 | 得到 `formula_id`、`output_name`、`formulas`、`begin_date` 等配置 |
| 生产 | 放进 Python、Node 后端、网站或定时任务 | 每天自动运行同一套公式，只读取最终结果 |

你可以直接把这段发给 Agent：

```text
请把刚才验证通过的选股逻辑整理成可复用公式包，输出 JSON。

要求：
1. 字段包括 formula_id、description、output_name、formulas、begin_date、use_minute_data、force_reusable_array。
2. 只把最终要读取的输出变量写进 force_reusable_array。
3. 不要让后续程序读取中间变量或全市场原始大矩阵。
4. 同时给出一个 Python/Node 后端调用建议，API Key 必须放在服务端环境变量。
```

公式包示例：

```json
{
  "formula_id": "volume_breakout_60d_intraday",
  "description": "14:30 盘中放量突破 60 日新高选股",
  "output_name": "放量突破Top10",
  "params": {
    "formulas": [
      "A股池 = 板块(万得全A) * 缺失填零(\"非ST股\")",
      "60日高基准 = 昨天(最大(\"全市场每日最高价\", 60))",
      "放量基准 = 昨天(平均(\"全市场每日成交额\", 20))",
      "突破60日新高 = (\"全市场每日最高价\" > \"60日高基准\") * \"A股池\"",
      "成交额放量 = (\"全市场每日成交额\" > 2 * \"放量基准\") * \"A股池\"",
      "排序值 = \"突破60日新高\" * \"成交额放量\" * 涨跌幅(\"全市场每日收盘价\")",
      "放量突破Top10 = 取前(\"排序值\", 10, 返回数值)"
    ],
    "begin_date": 20260101,
    "include_description": true,
    "use_minute_data": true,
    "force_reusable_array": ["放量突破Top10"]
  }
}
```

---

## 接入自己的 Python / 网站 / 自动化任务

探索阶段让 Agent 使用 skill；公式稳定后，把公式注册到自己的后端或脚本里。

推荐结构：

```text
formula registry -> runMultiFormulaBatchStream -> extract data_id -> readData -> rows/chart/cache
```

个人网站不要让浏览器直接请求 quant-buddy，也不要把 API Key 写进 HTML/JavaScript。正确结构是：

```text
浏览器 HTML -> 你的后端 /api/quant/run-screen -> quant-buddy API
```

可以把下面这段复制给 Claude Code、Cursor、Codex 或其他 Agent：

```text
请在当前网站项目中实现 POST /api/quant/run-screen。

要求：
1. 前端只允许提交 formula_id、top_n、use_minute_data。
2. 公式必须保存在后端白名单 registry，不允许浏览器提交任意公式。
3. API Key 只能从 QUANT_BUDDY_API_KEY 环境变量读取，不能出现在浏览器代码、HTML、日志或响应中。
4. 后端调用 https://www.quantbuddy.cn/skill/runMultiFormulaBatchStream，解析完成事件，找到 output_name 对应的 data_id。
5. 再调用 https://www.quantbuddy.cn/skill/readData，参数为 {"ids":[data_id],"mode":"last_column_full"}。
6. 返回给前端精简 JSON：formula_id、date、rows，rows 至少包含 code、name、value 或 return_pct。
7. top_n 限制在 1 到 100；formula_id 不存在返回 404；上游错误返回 502。
```

---

## 为什么值得 Star

如果你也遇到过这些问题，Star 这个仓库会很值：

- 想让 AI Agent 查真实金融数据，而不是只会写伪代码。
- 不想把 CSV、网页表格和几千行数据塞进模型上下文。
- 需要每天重复运行的盘中筛选、盘后复盘或个人研究看板。
- 想先用自然语言探索，再把稳定公式变成可运行的 Python、后端接口和定时任务。
- 希望看到更多 A 股、港股、美股在 AI Agent 工作流里的真实案例。

**如果这正是你想给 Agent 补上的能力，欢迎点一个 Star。** 也欢迎在 Issue 里提交你想看的数据字段、选股公式、回测模板或网站接入案例。

---

## 更新

```bash
npx skills update quant-buddy-skill -g -y
```

查看安装位置：

```bash
npx skills list -g --json
```

## 运行环境

- Python 3.8+，推荐 Python 3.11。
- 核心能力仅依赖 Python 标准库。
- 可选依赖：`python-dateutil`、`Pillow`、`requests`。

## 和 quant-buddy-skill 的关系

`quant-buddy-data` 是面向“AI Agent 查金融数据”的低门槛入口，底层复用成熟的 `quant-buddy-skill`。除了快速查数，也保留全市场筛选、公式、因子、回测、CSV 导出和图表渲染等进阶能力。

安装后的本地 skill 名可以继续叫 `quant-buddy-skill`，这样 Claude Code、Cursor、Codex、GitHub Copilot、Windsurf 等 Agent 中已有的调用习惯不需要大改。

## 安全与免责声明

- API Key 仅用于请求 quant-buddy 平台接口。
- API Key 只作为 HTTP `Authorization` 头发送到 quant-buddy 声明域名，不写入日志，不转发给第三方主机。
- 自建 HTML 或网站时，API Key 必须放在后端，不能放在浏览器 JavaScript 里。
- 本项目不提供投资建议、交易建议、收益承诺或自动交易服务。
- 回测、筛选和因子结果不代表未来收益，用户应自行核验数据口径、风险暴露、交易成本、滑点和合规要求。
- 费用消耗与请求规模、数据范围、读取模式有关，具体以平台实际返回为准。

## 联系作者

想看更多数据查询案例、接入问题和 AI Agent 工作流，欢迎访问官网或加入交流群。

官网：https://www.quantbuddy.cn

<p align="center">
  <table>
    <tr>
      <td align="center">
        <img src="assets/wechat_qr3.png" width="180" alt="个人微信二维码" />
        <br/>
        <sub>个人微信</sub>
      </td>
      <td align="center">
        <img src="assets/wechat_group_qr6.jpg" width="180" alt="微信群二维码" />
        <br/>
        <sub>微信群</sub>
      </td>
      <td align="center">
        <img src="assets/feishu_group_qr2.png" width="180" alt="飞书群二维码" />
        <br/>
        <sub>飞书群</sub>
      </td>
    </tr>
  </table>
</p>

## License

MIT
