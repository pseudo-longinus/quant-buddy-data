# quant-buddy-data

[中文](README.md) | [English](README.en.md)

<p align="center">
  <img src="assets/banner3.jpg" alt="quant-buddy-data" width="100%" />
</p>

Let Claude Code, Cursor, Codex, GitHub Copilot, Windsurf, and other AI agents query A-share, Hong Kong, and US stock market data, valuation data, and financial data directly.

No API wiring, no giant tables in the prompt, no CSV cleaning. Ask in natural language and get structured financial data back.

Official site: https://www.quantbuddy.cn

> This project is for financial data analysis, quantitative research, strategy validation, and educational use only. It is not investment advice, trading advice, a return guarantee, or an automated trading service.

## Quick Install

If you are familiar with AI agent tools, tell your agent:

> Install this skill for me:

```bash
npx skills add pseudo-longinus/quant-buddy-data -g -a claude-code -s quant-buddy-skill -y
```

For Cursor:

```bash
npx skills add pseudo-longinus/quant-buddy-data -g -a cursor -s quant-buddy-skill -y
```

For OpenClaw:

```bash
npx skills add pseudo-longinus/quant-buddy-data -g -a openclaw -s quant-buddy-skill -y
```

> The first version keeps `quant-buddy-skill` as the skill name for compatibility with the existing tool protocol.

## 30-Second Examples

After installation, ask your AI agent:

```text
Check Kweichow Moutai's latest close, daily return, PE, and PB.
```

```text
Show CATL's latest reported revenue, net profit, and ROE.
```

```text
Compare Apple, Nvidia, and Tesla over the past 20 trading days.
```

```text
Export BYD's close price and turnover for the past 60 trading days.
```

The agent turns your natural-language request into quant-buddy platform queries and returns structured results, time series, or CSV files.

## What It Can Do

| Capability | Coverage | Examples |
|---|---|---|
| Latest market data | A-shares / HK stocks / US stocks / indices | Latest price, close, return, turnover, volume |
| Valuation data | Mainly A-shares; some HK/US fields depending on API support | PE, PB, PS, dividend yield, market cap |
| Financial data | Mainly A-shares; some HK/US fields depending on API support | Revenue, net profit, ROE, total assets, debt ratio |
| Recent N-day series | Single asset or explicit asset lists | 5-day, 20-day, 60-day prices and returns |
| Fixed-period comparison | Multi-asset return comparison | Cumulative return from one date to another |
| CSV export | Query results and history series | Save locally for spreadsheets or downstream analysis |
| Macro one-dimensional series | GDP, CPI, PPI, PMI, M1/M2, social financing, credit, FX reserves, Treasury yields, LPR, OMO, USD/CNH, industrial output, retail sales, trade | Match exact `index_short_title` names such as `中国GDP当季同比`, `中国CPI同比`, `中国PPI同比`, `中采PMI`, `中国新增社融`, and `USDCNH`, then read with `readData` |
| Advanced computation | Mainly A-shares | Formulas, full-market screening, factors, backtests, charts |

## Why Not Just Another Data API

Most data APIs require you to write code, look up field names, handle parameters, and clean returned data.

quant-buddy-data aims for a shorter path: let an AI agent understand the question and call the platform for data retrieval and computation.

```text
You ask in natural language
        ↓
The agent identifies assets, fields, and time ranges
        ↓
quant-buddy queries and computes on the platform side
        ↓
You get structured results, tables, time series, or CSV
```

It is useful when:

- You want your AI coding tool to query financial data directly.
- You do not want thousands of raw rows in the LLM context.
- You need reusable, auditable data-query workflows.
- You want to start with data lookup and later move into screening, factors, or backtesting.

## Common Prompts

### Single Stock

```text
Check Kweichow Moutai's latest close, daily return, turnover, PE, and PB.
```

### Multiple Stocks

```text
Compare CATL, BYD, and Sungrow by latest close and market cap.
```

### Recent N Trading Days

```text
List Tencent's close price and daily return over the past 20 trading days.
```

### Financial Metrics

```text
Check Apple's latest reported revenue, net profit, and gross margin.
```

### Export Data

```text
Export Kweichow Moutai's close price for the past 120 trading days as CSV.
```

### Advanced Analysis

```text
Screen all A-shares for low PE, high ROE, and strong 20-day return.
```

```text
Backtest a low PE + high ROE portfolio and compare it with CSI 300.
```

## Data Coverage

| Market | Market Data | Valuation | Financials | Screening / Backtesting |
|---|---|---|---|---|
| A-shares | Supported | Supported | Supported | Supported |
| Hong Kong stocks | Supported | Partially supported, depending on API response | Partially supported, depending on API response | Data lookup first |
| US stocks | Supported | Partially supported, depending on API response | Partially supported, depending on API response | Data lookup first |
| Major indices | Supported | Partially supported | - | Can be used as benchmarks or comparison assets |
| Macro one-dimensional series | Supported via `confirmDataMulti` + `readData` | - | - | Use `index_short_title` names from the reference list, for example `中国GDP当季同比`, `中国CPI同比`, `中国PPI同比`, `中采PMI`, `中国M1同比`, `中国M2同比`, `中国新增社融`, `中国新增人民币贷款`, `中国外汇储备`, `中国10年国债收益`, `中国1年期LPR`, `中国7天逆回购利率`, and `USDCNH` |

## Installation

New users should install the skill only into the AI agent they actually use. Avoid using `--all` by default.

| Agent | Recommended command |
|---|---|
| Claude Code | `npx skills add pseudo-longinus/quant-buddy-data -g -a claude-code -s quant-buddy-skill -y` |
| Cursor | `npx skills add pseudo-longinus/quant-buddy-data -g -a cursor -s quant-buddy-skill -y` |
| OpenClaw | `npx skills add pseudo-longinus/quant-buddy-data -g -a openclaw -s quant-buddy-skill -y` |

If you use multiple agents, repeat `-a`:

```bash
npx skills add pseudo-longinus/quant-buddy-data -g -s quant-buddy-skill -a claude-code -a cursor -y
```

List the skills in this repository:

```bash
npx skills add pseudo-longinus/quant-buddy-data --list
```

Update an existing installation:

```bash
npx skills update quant-buddy-skill -g -y
```

If Windows users encounter symlink or permission errors, add `--copy`:

```bash
npx skills add pseudo-longinus/quant-buddy-data -g -a claude-code -s quant-buddy-skill -y --copy
```

## Configure API Key

Before first use, configure your quant-buddy API key:

1. Go to https://www.quantbuddy.cn to register and get an API key.
2. Edit `config.json` under the skill directory and fill in the `api_key` field.
3. Or send this to an agent environment that can write local files:

```text
Help me configure APIkey: sk-xxxxxxxx
```

## Runtime Requirements

- Python 3.8+, Python 3.11 recommended.
- Core market data, valuation, financials, series, screening, and backtesting features only depend on the Python standard library.
- Optional dependencies:
  - `python-dateutil`: used by event-study helpers.
  - `Pillow`: used for chart image conversion.
  - `requests`: used by optional event-news search helpers.
- Optional environment variable: `BOCHA_API_KEY`, only used by event-news search helpers.

## Security, Privacy, And Disclaimer

- The quant-buddy API key is only used to request quant-buddy platform APIs.
- The API key is only sent as an HTTP `Authorization` header to declared quant-buddy domains. It is not written to logs and is not forwarded to third-party hosts.
- This project is for financial data analysis, quantitative research, strategy validation, and educational use only. It is not investment advice, trading advice, a return guarantee, or an automated trading service.
- Users should independently verify data definitions, costs, risk exposure, and compliance requirements.

## Troubleshooting

- Environment dependencies: `skills/quant-buddy-skill/references/environment.md`
- Troubleshooting: `skills/quant-buddy-skill/references/troubleshooting.md`
- RU billing: `skills/quant-buddy-skill/references/ru-billing.md`

## Relationship With quant-buddy-skills

`quant-buddy-data` is the low-friction entry point for financial data lookup from AI agents.

It reuses the underlying `quant-buddy-skill`, so advanced features such as full-market screening, formulas, factors, backtests, and charts are still available. The first version simply makes the data-query use case much easier to understand.

## Contact

For data-query examples, integration questions, and AI agent workflows, scan the QR codes below to connect or join the community.

<p align="center">
  <table>
    <tr>
      <td align="center">
        <img src="assets/wechat_qr3.png" width="180" alt="Personal WeChat QR code" />
        <br/>
        <sub>Personal WeChat</sub>
      </td>
      <td align="center">
        <img src="assets/wechat_group_qr6.jpg" width="180" alt="WeChat group QR code" />
        <br/>
        <sub>WeChat Group</sub>
      </td>
      <td align="center">
        <img src="assets/feishu_group_qr2.png" width="180" alt="Feishu group QR code" />
        <br/>
        <sub>Feishu Group</sub>
      </td>
    </tr>
  </table>
</p>

## License

MIT
