# quant-buddy-data

<p align="center">
  <img src="assets/banner4.jpg" alt="quant-buddy-data" width="100%" />
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
  <img alt="Market" src="https://img.shields.io/badge/A%E8%82%A1%20%7C%20%E6%B8%AF%E8%82%A1%20%7C%20%E7%BE%8E%E8%82%A1-data-orange">
</p>

> **只想下载金融数据？先用 `fast_query`。**  
> 它把资产识别、字段识别、数据读取和结果整理合成一次调用，覆盖 A 股、港股、美股和主要指数的大部分日常行情、估值、财务与历史序列需求；宏观数据（GDP、CPI 等）可先用 `confirmDataMulti` 搜一下找到对应的数据名，再用 `readData` 读取。

如果你的需求是资产行情、估值、财务或历史序列下载，答案通常就是：**`fast_query`**；宏观数据走 `confirmDataMulti` + `readData`。

---

## 适合什么需求

把下面这些问题交给 Agent，或直接调用 `fast_query`：

```text
下载贵州茅台、宁德时代最近一年每日收盘价和成交额。
```

```text
查苹果、英伟达、特斯拉最新收盘价、涨跌幅、PE、PB、股息率。
```

```text
导出沪深300成分里 100 只股票最近 250 个交易日的收盘价，数据量大就给 CSV 链接。
```

```text
查贵州茅台最近报告期营业收入、净利润、ROE、总资产和资产负债率。
```

`fast_query` 适合：

| 场景 | 用法 | 结果 |
|---|---|---|
| 最新行情 / 估值 | `query_type="snapshot"` | 最新价、涨跌幅、成交额、PE、PB、市值等 |
| 历史序列 | `query_type="window"` | 最近 N 日或指定区间的价格、成交额、涨跌幅等序列 |
| 财务报告期 | `query_type="report"` | 营收、净利润、ROE、总资产、资产负债率等 |
| 批量下载 | `assets` 一次最多 1000 个 | 小结果直接 JSON，大结果自动返回 CSV 下载链接 |

需要全市场选股、复杂公式、回测、行业聚合或 K 线图时，再使用进阶工具；只是查数、下表、导出序列，先走 `fast_query` 就能覆盖绝大多数场景。

---

## 数据覆盖范围

quant-buddy 面向日常下载和查数场景，覆盖常见资产、常见字段和常见时间范围。资产类行情、估值、财务优先用 `fast_query`；宏观数据先用 `confirmDataMulti` 搜一下找到对应的数据名。

| 市场 / 资产 | 覆盖内容 | 典型用法 |
|---|---|---|
| A 股 | 沪深主板、创业板、科创板、北交所个股，以及主要宽基指数 | 下载个股历史行情、最新估值、报告期财务、A 股批量序列 |
| 港股 | 港股个股，支持行情与常用估值，部分财务字段以接口实际返回为准 | 查港股最新价格、PE/PB/股息率、历史收盘价 |
| 美股 | 美股个股及部分境外 ETF，支持行情与常用估值，部分财务字段以接口实际返回为准 | 查苹果、英伟达、特斯拉等美股行情、估值和历史序列 |
| 指数 | 沪深300、中证500、万得全A等主要指数 | 下载基准指数序列、做区间对比或看板展示 |
| 商品期货 | 约 60 个商品期货品种（螺纹钢、沪银、黄金、原油等），含期货行情、现货价格、库存 | 查期货收盘价、现货价、商品库存序列；单位按品种（元/吨、元/千克等），仅 A 股期货品种 |
| 宏观一维序列 | GDP、CPI、PPI、PMI、M1/M2、社融、信贷、外汇储备、国债收益率、LPR、OMO 利率、汇率等 | 先用 `confirmDataMulti` 搜一下找到想要的数据名，如 `中国GDP当季同比`、`中国CPI同比`、`USDCNH`，再用 `readData` 读取；具体以接口实际返回为准 |

| 数据类型 | 常用字段 | 说明 |
|---|---|---|
| 行情 | 收盘价、开盘价、最高价、最低价、涨跌幅、成交额、成交量 | `snapshot` 查最新，`window` 查历史序列；最新行情会自动使用日内刷新 |
| 估值 | PE、PE_TTM、PB、PS_TTM、股息率、PCF、总市值 | A/港/美常用估值字段均可查；流通市值、换手率主要支持 A 股 |
| 财务 | 营业收入、净利润、归母净利润、营业成本、总资产、净资产、ROE、净利率、毛利率、经营现金流、投资活动现金流、筹资活动现金流 | `report` 查最近报告期；A/港/美统一返回单季数据，具体字段以接口实际返回为准 |
| 资金流向 / 南北向 | 主力资金净额/净占比、超大单/大单/中单/小单净额、北向持股比例/市值、南向持股比例/市值 | `snapshot` 查最新、`window` 查日频序列；主力资金与北向持股仅 A 股，南向持股仅港股 |
| 派生字段 | 资产负债率 | 服务端可由总资产、净资产自动计算 |
| 宏观 | GDP、CPI、PPI、PMI、M1/M2、社融、信贷、外汇储备、国债收益率、LPR、OMO 利率、汇率等 | 多为时间序列，用 `confirmDataMulti` 搜一下找到数据名后读取，适合宏观看板、策略背景变量、区间对比和本地建模 |
| 下载格式 | JSON / CSV | 小结果直接返回 JSON；数据点超过 500 时自动切换 CSV 模式，返回 `csv_url` 下载链接 |

常用限制：单次最多 1000 个资产，窗口序列最多 2500 个交易日（约 10 年），历史数据可回溯至 2005-01-04，单次最多 200,000 个数据点；每日最多 1,000,000 个数据点、50 次 CSV 下载。日常个人研究、课程实验、看板取数和轻量批量下载通常够用。

常用宏观数据示例包括：`中国GDP当季同比`、`中国CPI同比`、`中国PPI同比`、`中采PMI`、`中国M1同比`、`中国M2同比`、`中国新增社融`、`中国社融存量`、`中国新增人民币贷款`、`中国外汇储备`、`中国1年国债收益`、`中国5年国债收益`、`中国10年国债收益`、`中国1年期LPR`、`中国5年期LPR`、`中国7天逆回购利率`、`USDCNH`、`中国工业增加值同比`、`中国社会零售总额`、`中国进出口总额`。

---

## 30 秒开始

如果你使用 Claude Code、Cursor、Codex、GitHub Copilot、Windsurf 等 Agent 工具，可以直接安装 skill：

```bash
npx skills add pseudo-longinus/quant-buddy-data -g -a claude-code -s quant-buddy-skill -y
```

如果你的 Agent 不是 Claude Code，把 `-a claude-code` 替换成对应名称，或按你的 skills 工具说明安装。

注册并获取 API Key：<https://www.quantbuddy.cn/login>

配置方式推荐用环境变量，避免把 Key 写进代码仓库：

```bash
QUANT_BUDDY_API_KEY=sk-xxxxxxxx
QUANT_BUDDY_ENDPOINT=https://www.quantbuddy.cn/skill
```

也可以让 Agent 帮你配置：

```text
帮我配置 quant-buddy API Key：sk-xxxxxxxx
```

---

## 怎么调用 `fast_query`

### 1. 让 Agent 直接调用

最简单的方式是把需求说清楚：

```text
用 quant-buddy 的 fast_query 下载贵州茅台、宁德时代最近 250 个交易日的收盘价、涨跌幅和成交额。
如果返回 CSV 模式，请把 csv_url 和字段摘要列出来。
```

Agent 会先建立 session，再调用 `fast_query`，并按结果给你 JSON 表格或 CSV 下载链接。

### 2. 本地命令行调试

在 Windows PowerShell 中：

```powershell
cd skills/quant-buddy-skill
$env:QUANT_BUDDY_API_KEY="sk-xxxxxxxx"
$env:GZQ_PARAMS='{"user_query":"下载贵州茅台最近一年收盘价"}'
python -X utf8 scripts/call.py newSession
$env:GZQ_PARAMS='{"assets":["贵州茅台"],"query_type":"window","fields":["收盘价"],"window_days":250,"user_query":"下载贵州茅台最近一年收盘价"}'
python -X utf8 scripts/call.py fast_query
```

### 3. HTTP API 调用

工具名是 `fast_query`，HTTP 路径是 `POST /skill/fastQuery`：

```bash
curl -X POST "https://www.quantbuddy.cn/skill/fastQuery" \
  -H "Authorization: Bearer $QUANT_BUDDY_API_KEY" \
  -H "Content-Type: application/json; charset=utf-8" \
  -d '{
    "assets": ["贵州茅台", "宁德时代"],
    "query_type": "window",
    "fields": ["收盘价", "涨跌幅", "成交额"],
    "window_days": 250
  }'
```

自建网站或 App 时，API Key 必须放在服务端环境变量里，不要写进浏览器 JavaScript、HTML、日志或公开仓库。

---

## 参数速查

| 参数 | 必填 | 说明 |
|---|---|---|
| `assets` | 是 | 资产数组，中文名或代码均可，最多 1000 个 |
| `query_type` | 是 | `snapshot` 最新数据；`window` 历史序列；`report` 最近报告期财务 |
| `fields` | 是 | 字段数组，如 `收盘价`、`涨跌幅`、`PE_TTM`、`PB`、`营业收入` |
| `window_days` | 否 | `window` 模式使用，最近 N 个交易日，最多 2500 |
| `start_date` / `end_date` | 否 | 固定日期区间，格式 `YYYYMMDD` 或 `YYYY-MM-DD` |
| `result_mode` | 否 | `value` 返回区间最后有效值；`series` 返回完整序列 |

三个最常见请求：

```json
{
  "assets": ["贵州茅台", "宁德时代", "AAPL.N"],
  "query_type": "snapshot",
  "fields": ["收盘价", "涨跌幅", "PE_TTM", "PB", "股息率"]
}
```

```json
{
  "assets": ["贵州茅台", "宁德时代"],
  "query_type": "window",
  "fields": ["收盘价", "成交额"],
  "start_date": "2025-01-01",
  "end_date": "2025-12-31"
}
```

```json
{
  "assets": ["贵州茅台", "苹果"],
  "query_type": "report",
  "fields": ["营业收入", "净利润", "ROE", "资产负债率"]
}
```

---

## 返回结果怎么看

小结果默认返回紧凑 JSON：

```json
{
  "success": true,
  "query_type": "snapshot",
  "fields_meta": {
    "收盘价": { "unit": "元", "date_type": "trade_date" },
    "PE_TTM": { "unit": "倍", "date_type": "trade_date" }
  },
  "dates": { "trade_date": "2026-06-03" },
  "results": {
    "贵州茅台": {
      "ticker": "SH600519",
      "收盘价": 1520.5,
      "PE_TTM": 23.4
    }
  }
}
```

数据点超过 500 时，服务端会自动切到 CSV 模式：

```json
{
  "success": true,
  "mode": "csv",
  "summary": {
    "total_data_points": 156468,
    "csv_count": 5
  },
  "csv_fields": [
    {
      "intent": "收盘价",
      "csv_url": "https://...",
      "csv_expires_at": "2026-06-03T18:00:00+08:00"
    }
  ]
}
```

也就是说，你不需要自己把几十万行数据塞进对话上下文；直接下载 CSV 即可。

---

## 数据质量与稳定性

- 自建数据管道，统一交易日、股票代码、复权、报告期和字段口径。
- 常用字段有白名单直连路径，命中后无需额外字段解析，查询更快、更稳定。
- `snapshot` 查询最新行情时自动使用日内刷新；历史区间仍使用日线口径。
- 返回中包含 `fields_meta`，会说明字段单位和日期类型，方便后续程序处理。
- 默认允许部分成功：个别资产或字段失败时，会在 `asset_errors` / `field_errors` 中说明，其余结果继续返回。
- 港股、美股部分估值和财务字段以接口实际返回为准；涉及正式交易或研究报告时，请自行核验数据口径和更新时间。

---

## 价格

`fast_query` 不只是把数据拉出来，也把维护、质量、速度和 Agent 体验一起做掉：

- 专人维护数据管道和接口稳定性，持续处理字段、交易日、复权、报告期和资产代码变化，不会因为无人维护而突然无法使用。
- 多源核对与异常检查，减少错数、缺数、字段口径漂移带来的返工。
- 优化下载速度与带宽，大结果自动走 CSV 链接，避免在对话里刷出大段原始数据。
- 优化返回结构，`fields_meta` 只声明一次，结果按 compact JSON / CSV 返回，提高 token efficiency，降低 Agent 调用时的上下文负担。

**低至 1 元/月，即可满足大部分个人查数、课程实验、轻量研究和看板取数需求。学生与个人研究者友好，现在注册立即送积分，可以先试用再决定。**

实际消耗会随资产数量、字段数量、日期跨度和返回模式变化，以平台账户页和接口返回为准。

---

## 什么时候不用 `fast_query`

| 需求 | 推荐工具 |
|---|---|
| 单纯查行情、估值、财务、历史序列 | `fast_query` |
| 宏观数据，如 GDP/CPI/PPI/PMI/社融/利率/汇率 | `confirmDataMulti` 搜到对应的数据名，再用 `readData` 读取 |
| 已经有 `data_id`，要保存一维时序 CSV | `downloadData` |
| 全市场选股、复杂公式、因子、回测 | `runMultiFormulaBatchStream` + `readData` |
| K 线或图表渲染 | `renderKLine` / `renderChart` |

先从 `fast_query` 开始；当它不够用时，再升级到公式和图表工具。

---

## 进阶：公式任务包（注册公式 → 对外取数，无需 API Key）

`fast_query` 解决「我自己要一份数据」；**公式任务包（Formula Package）**解决「我把一组算好的指标定下来，让一个网页/看板/第三方反复来取最新值」。

你只需把一批公式注册一次，拿到一对凭证（`package_id` + `signature`）；之后任何页面或程序凭这对凭证就能取到**永远最新**的结果——底层数据一更新，服务端自动重算，你不用重跑公式、不用搭后端、也不用把 API Key 放进前端。

**典型场景**

- **自己做日报 / 数据看板**：把每天要看的指标（涨跌幅、估值分位、资金流向、自定义因子打分……）写成一批公式注册成一个包，用一个静态 HTML 页面 `fetch` 取数渲染。每天打开页面就是当日最新数据，**无需后端、无需每天手动跑公式**。
- **给团队 / 客户一个只读数据页**：发出去的是 `package_id` + `signature` 凭证，而不是 API Key；对方只能取这个包里固定的产出，改不了公式、也拿不到你的账号权限。撤销随时生效。
- **嵌进已有网站 / Notion / 飞书 / 大屏**：任何能跑 `fetch` 的地方都能直接读数渲染，把 quant-buddy 的数据接进你自己的页面。
- **第三方 / 轻量集成**：把一个算好的指标包交给合作方只读对接，计费始终走你（包所有者）的配额，对方零配置接入。

两段式用法：

1. **注册**（需 API Key）：提交一组公式和每个产出的读取模式，服务端执行校验后返回 `package_id` + `signature`。
2. **取数**（**无需 API Key**）：凭 `package_id` + `signature` 拉数据，结果以 SSE 流式返回。底层数据更新后服务端会**自动重算**，取数永远拿最新结果，绝不返回过期数据。

> `signature` 是访问凭证，仅在注册响应里**明文返回一次**，请妥善保存（脚本会自动落盘到 `output/formula_packages/<package_id>.json`）。取数方无需 API Key，费用计入**包所有者**的配额池。

### 用本地脚本调用

```powershell
cd skills/quant-buddy-skill

# 1. 注册：params.json 里写 formulas + reads（中文公式用 @file 传，避免编码截断）
python scripts/formula_package.py register @params.json

# 2. 取数：只需 package_id，signature 可由本地凭证自动补全
$env:FP_PARAMS='{"package_id":"pkg_xxx"}'
python scripts/formula_package.py query

# 管理：列表 / 撤销 / 刷新（轮换签名）
python scripts/formula_package.py list    '{"page":1,"page_size":20}'
python scripts/formula_package.py revoke  '{"package_id":"pkg_xxx"}'
python scripts/formula_package.py refresh '{"package_id":"pkg_xxx","rotate_signature":true}'
```

注册用的 `params.json` 示例：

```json
{
  "formulas": [
    "T_px = \"全市场每日收盘价\" * 1",
    "T_ma5 = 平均(\"T_px\", 5)",
    "T_ratio = \"T_px\" / \"T_ma5\""
  ],
  "reads": [
    { "output": "T_px",    "read_mode": "range_data", "mode_params": { "start_date": 20240601, "end_date": 20240630 } },
    { "output": "T_ratio", "read_mode": "last_day_stats" }
  ],
  "ttl_days": 365
}
```

- 未列入 `reads` 的公式（如上例 `T_ma5`）只作中间变量参与计算、不对外返回。
- 同一个包里不同产出可用**不同读取模式**：`range_data`（区间完整序列）/ `last_day_stats`（最新截面统计）/ `last_valid_per_asset`（每个资产最后一个有效值）。
- 单包最多 100 条公式、20 个对外产出，默认有效期 365 天（注册时可用 `ttl_days` 指定）。

### 前端 / 第三方直接取数（无需 API Key）

下面这段就是「自己的日报页面」的核心：把它放进一个静态 HTML 里，凭凭证取数后把 `outputs` 渲染成表格 / 图表即可，每次打开都是当日最新数据。取数接口走 SSE，浏览器用 `fetch` 读流（签名放 body，不进 URL，不要用 `EventSource`）：

```js
const resp = await fetch('https://www.quantbuddy.cn/skill/queryFormulaPackage', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ package_id, signature }),
})
const reader = resp.body.getReader()
const decoder = new TextDecoder()
const outputs = {}
let buf = ''
for (;;) {
  const { value, done } = await reader.read()
  if (done) break
  buf += decoder.decode(value, { stream: true })
  const blocks = buf.split('\n\n'); buf = blocks.pop()
  for (const block of blocks) {
    const ev = (block.match(/event:\s*(.*)/) || [])[1]
    const dt = JSON.parse((block.match(/data:\s*([\s\S]*)/) || [])[1])
    if (ev === 'result') outputs[dt.output] = dt        // outputs["T_px"].data ...
    else if (ev === 'error') throw new Error(`${dt.code}: ${dt.message}`)
  }
}
```

curl 快速验证：

```bash
curl -N -X POST https://www.quantbuddy.cn/skill/queryFormulaPackage \
  -H 'Content-Type: application/json' \
  -d '{"package_id":"pkg_xxx","signature":"a1b2c3..."}'
```

> 注册 / 列表 / 撤销 / 刷新需 API Key，**必须放在服务端**；只有取数接口（`queryFormulaPackage`）可暴露给浏览器。完整参数、读取模式结构与错误码见 `skills/quant-buddy-skill/tools/formula_package.md`，端到端用法见 `recipes/formula-package.md`。

---

## 安全与免责声明

- API Key 仅用于请求 quant-buddy 平台接口。
- 自建服务时，API Key 必须放在服务端，不要放在浏览器代码中。
- 本项目用于金融数据分析、量化研究、策略验证和教育用途，不构成投资建议、交易建议、收益承诺或自动交易服务。
- 回测、筛选、因子和历史数据不代表未来收益。

## License

MIT