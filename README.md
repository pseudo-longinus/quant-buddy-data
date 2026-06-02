# quant-buddy-data

[中文](README.md) | [English](README.en.md)

<p align="center">
  <img src="assets/banner.jpg" alt="quant-buddy-data" width="100%" />
</p>

让 Claude Code、Cursor、Codex、GitHub Copilot、Windsurf 等 AI Agent 直接查询 A 股、港股、美股行情、估值和财务数据。

不用写 API，不用搬大表，不用清洗 CSV。用自然语言让 AI Agent 获取结构化金融数据。

官网：https://www.quantbuddy.cn

> 本项目用于金融数据分析、量化研究、策略验证和教育用途，不构成投资建议、交易建议、收益承诺或自动交易服务。

## 3 秒快速安装

如果你熟悉 Agent 工具，可以直接对 AI Agent 说：

> 帮我安装这个 skill：

```bash
npx skills add pseudo-longinus/quant-buddy-data -g -a claude-code -s quant-buddy-skill -y
```

如果你使用 Cursor：

```bash
npx skills add pseudo-longinus/quant-buddy-data -g -a cursor -s quant-buddy-skill -y
```

如果你使用 OpenClaw：

```bash
npx skills add pseudo-longinus/quant-buddy-data -g -a openclaw -s quant-buddy-skill -y
```

> 首版沿用 `quant-buddy-skill` 作为 skill 名称，确保和现有工具协议兼容。

## 30 秒示例

安装后，你可以直接对 AI Agent 说：

```text
查贵州茅台最新收盘价、涨跌幅、PE、PB。
```

```text
查宁德时代最近报告期营收、净利润、ROE。
```

```text
对比苹果、英伟达、特斯拉最近 20 个交易日涨跌幅。
```

```text
导出比亚迪最近 60 个交易日的收盘价和成交额。
```

AI Agent 会把自然语言问题转成 quant-buddy 平台可执行的数据查询，并返回结构化结果、时间序列或 CSV 文件。

## 能做什么

| 能力 | 支持范围 | 示例 |
|---|---|---|
| 最新行情 | A 股 / 港股 / 美股 / 指数 | 最新价、收盘价、涨跌幅、成交额、成交量 |
| 估值数据 | A 股为主，部分港美股字段以接口返回为准 | PE、PB、PS、股息率、市值 |
| 财务数据 | A 股为主，部分港美股字段以接口返回为准 | 营收、净利润、ROE、总资产、资产负债率 |
| 最近 N 日序列 | 单资产或明确资产列表 | 最近 5 日、20 日、60 日价格和涨跌幅 |
| 固定区间对比 | 多资产区间收益 | 从某日到某日累计涨跌幅 |
| CSV 导出 | 查询结果、历史序列 | 保存到本地，供表格或后续分析使用 |
| 进阶计算 | A 股为主 | 公式、全市场筛选、因子、回测、图表 |

## 为什么不是普通数据 API

普通数据 API 通常要求你先写代码、查字段、处理接口参数、清洗返回结果。

quant-buddy-data 的目标更简单：让 AI Agent 直接理解你的问题，并调用平台完成数据获取和必要计算。

```text
你说一句自然语言
        ↓
Agent 识别资产、字段和时间范围
        ↓
quant-buddy 平台查询和计算
        ↓
返回结构化结果、表格、序列或 CSV
```

它尤其适合这些场景：

- 你想让 AI 编程工具直接查金融数据。
- 你不想把几千行原始数据塞进 LLM 上下文。
- 你需要可复用、可审计的数据查询流程。
- 你先从简单查数开始，之后可能继续做筛选、因子或回测。

## 常见用法

### 查单只股票

```text
查贵州茅台最新收盘价、涨跌幅、成交额、PE、PB。
```

### 查多只股票

```text
对比宁德时代、比亚迪、阳光电源最新收盘价和市值。
```

### 查最近 N 日

```text
列出腾讯控股最近 20 个交易日收盘价和涨跌幅。
```

### 查财务指标

```text
查苹果最近报告期营收、净利润、毛利率。
```

### 导出数据

```text
把贵州茅台最近 120 个交易日收盘价导出成 CSV。
```

### 进阶：继续做量化分析

```text
筛选全 A 股中低 PE、高 ROE、近 20 日涨幅靠前的股票。
```

```text
回测低 PE + 高 ROE 组合，相对沪深 300 画净值曲线。
```

## 数据覆盖

| 市场 | 行情 | 估值 | 财务 | 筛选 / 回测 |
|---|---|---|---|---|
| A 股 | 支持 | 支持 | 支持 | 支持 |
| 港股 | 支持 | 部分支持，以接口返回为准 | 部分支持，以接口返回为准 | 暂以数据查询为主 |
| 美股 | 支持 | 部分支持，以接口返回为准 | 部分支持，以接口返回为准 | 暂以数据查询为主 |
| 主要宽基指数 | 支持 | 部分支持 | - | 可作为基准或对比对象 |

## 安装

建议新用户只安装到自己正在使用的 AI Agent，不要默认使用 `--all`。

| 你使用的 Agent | 推荐命令 |
|---|---|
| Claude Code | `npx skills add pseudo-longinus/quant-buddy-data -g -a claude-code -s quant-buddy-skill -y` |
| Cursor | `npx skills add pseudo-longinus/quant-buddy-data -g -a cursor -s quant-buddy-skill -y` |
| OpenClaw | `npx skills add pseudo-longinus/quant-buddy-data -g -a openclaw -s quant-buddy-skill -y` |

如果你同时使用多个 Agent，可以重复指定 `-a`：

```bash
npx skills add pseudo-longinus/quant-buddy-data -g -s quant-buddy-skill -a claude-code -a cursor -y
```

先查看仓库里有哪些 skill：

```bash
npx skills add pseudo-longinus/quant-buddy-data --list
```

已安装用户更新：

```bash
npx skills update quant-buddy-skill -g -y
```

Windows 用户如果遇到 symlink 或权限错误，可以追加 `--copy`：

```bash
npx skills add pseudo-longinus/quant-buddy-data -g -a claude-code -s quant-buddy-skill -y --copy
```

## 配置 API Key

首次使用前需要配置 quant-buddy API Key：

1. 前往 https://www.quantbuddy.cn 注册并获取 API Key。
2. 编辑 skill 目录下的 `config.json`，将 `api_key` 字段填入你的 Key。
3. 或在支持写入本地文件的 AI Agent 对话中发送：

```text
帮我配置 APIkey：sk-xxxxxxxx
```

## 运行环境

- Python 3.8+，推荐 Python 3.11。
- 核心行情、估值、财务、序列、筛选和回测能力仅依赖 Python 标准库。
- 可选依赖：
  - `python-dateutil`：事件研究辅助功能使用。
  - `Pillow`：图表图片格式转换时使用。
  - `requests`：事件新闻搜索辅助功能使用。
- 可选环境变量：`BOCHA_API_KEY`，仅事件新闻搜索辅助功能使用。

## 安全、隐私与免责声明

- quant-buddy API Key 仅用于请求 quant-buddy 平台接口。
- API Key 只作为 HTTP `Authorization` 头发送到 quant-buddy 声明域名，不写入日志，不转发给第三方主机。
- 本项目用于金融数据分析、量化研究、策略验证和教育用途，不构成投资建议、交易建议、收益承诺或自动交易服务。
- 用户应自行核验数据口径、交易成本、风险暴露和合规要求。

## 故障排查

- 环境依赖：`skills/quant-buddy-skill/references/environment.md`
- 故障排查：`skills/quant-buddy-skill/references/troubleshooting.md`
- RU 计费：`skills/quant-buddy-skill/references/ru-billing.md`

## 和 quant-buddy-skills 的关系

`quant-buddy-data` 是面向“AI Agent 查金融数据”的低门槛入口。

底层能力复用 `quant-buddy-skill`，因此除了快速查数，也保留全市场筛选、公式计算、因子、回测和图表等进阶能力。首版重点先把“让 Agent 查数据”这件事讲清楚。

## 联系作者

想看更多数据查询案例、接入问题和 AI Agent 工作流，欢迎添加微信或加入交流群。

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
