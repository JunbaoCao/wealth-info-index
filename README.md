# wealth-obsidian-kb · Enterprise Internal Control & National Policy Knowledge Base

**Wealth (威尔思)** · One-person-firm **Obsidian knowledge base + policy knowledge hub + free A-share data tool**.

**License: MIT**

> This is Wealth's second public repo (the first is `Wealth-device-inspector`). It organizes the **latest national ministry policies** — 审计(300 audit) / 会计(400 accounting) / 税务(500 tax) / 法律(600 law) / 合规(700 compliance) / 国资(800 SOE assets) / 能源(900 energy) — into a queryable Obsidian knowledge base, and bundles a **free, no-token A-share historical-data tool** (akshare). Policy originals are always external-linked to official ministry sites; this repo only keeps **index + key points + execution rules**, so stale/voided clauses never leak into reports.

---

## What it is

An open-source **policy & finance knowledge base** for the Wealth (Wei Er Si) one-person accounting firm. Its job is **keeping the practitioner current on national ministry policy** and **providing a free way to pull A-share historical market data** — so audits, tax work and reports always cite valid, up-to-date regulations.

**Core idea: know the latest policy first, then audit / tax / consult.**

- Tracks 7 ministry lines: **审计 · 会计 · 税务 · 法律 · 合规 · 国资 · 能源**.
- Each line has a knowledge note: official sources → framework → annual tracking list → relevance to our firm → links.
- A companion **execution-rules** note turns policies into auditable operating rules.
- A **free A-share data tool** (akshare) pulls historical quotes with multi-source fallback.

---

## Features

- ✅ **7 ministry lines** — one `XXX-知识.md` each: 审计 / 会计 / 税务 / 法律 / 合规 / 国资 / 能源.
- ✅ **Uniform structure** — official sources + framework + annual tracking + firm relevance + links.
- ✅ **Obsidian-ready** — `[[ ]]` wikilinks, MOC index, relationship graph; open the folder directly in Obsidian.
- ✅ **Execution rules** — `500-我的规范/政策法规规范.md`: 4 citation principles + per-line quick-reference + annual policy check.
- ✅ **Free A-share data** — `akshare` (MIT, no token); one script pulls history with automatic source fallback.
- ✅ **Index-only, never moves files** — policy originals live at official ministry sites; nothing copied into the vault.
- ✅ **Honest & bottom-line** — flags that each clause must be verified for its latest number/status at the official source.

---

## Repository structure

```
wealth-obsidian-kb/
├── README.md                ← This file (English usage guide)
├── README.zh.md             ← Chinese usage guide
├── 000-主页.md              ← Global entry (Wealth 知识中枢)
├── 100-我的数据/            ← File locations, tooling index, setup summary
├── 200-我的工作/            ← Work log, current projects
├── 300-我的工具/            ← skill + DeepSeek Harness index
├── 400-我的知识/            ← Knowledge (RAG graph)
│   └── 国家部委政策/        ← ★ Policy knowledge base
│       ├── _索引.md         ←   Entry + relationship graph + official sources
│       ├── 审计-知识.md     ←   Audit line (审计署 / 财政部)
│       ├── 会计-知识.md     ←   Accounting line (财政部会计司)
│       ├── 税务-知识.md     ←   Tax line (税务总局)
│       ├── 法律-知识.md     ←   Law line (司法部 / 人大)
│       ├── 合规-知识.md     ←   Compliance line (各监管机构)
│       ├── 国资-知识.md     ←   SOE-assets line (国资委)
│       ├── 能源-知识.md     ←   Energy line (能源局 / 发改委)
│       └── A股数据工具.md   ←   Free A-share data tool (akshare)
├── 500-我的规范/            ← Regulations / execution rules
│   ├── 白皮书-v1.3.md       ←   Constitution (source of truth)
│   └── 政策法规规范.md       ←   ★ Policy execution rules + annual check
├── scripts/                 ← A-share data fetch scripts
│   ├── fetch_a股.py         ←   Pull A-share history (auto multi-source)
│   └── akshare_test.py      ←   Multi-endpoint validation
└── data/                    ← ★ Pulled CSVs (git-ignored, not committed)
```

---

## Quick start

### 1) Open the knowledge base (human view)

Open this repository's root folder in **Obsidian**. Start at `000-主页.md`; from there the whole knowledge hub and the national-policy knowledge base are one click away.

### 2) Pull free A-share historical data

Requires Python 3 + akshare:

```powershell
pip install akshare pandas
python scripts/fetch_a股.py 600519 20250101 20260814 qfq    # auto-select available source
python scripts/fetch_a股.py 600519 20250101 20260814 qfq tx   # force Tencent
python scripts/fetch_a股.py 600519 20250101 20260814 qfq sina # force Sina
```

Output CSV to `data/` and print the first 5 rows.

### Source test results (2026-08-14, this machine)

| Source | akshare API | Result |
|--------|-------------|--------|
| East Money (东财) | `stock_zh_a_hist` | ❌ connection dropped (`RemoteDisconnected`) |
| Sina (新浪) | `stock_zh_a_daily` | ✅ 54 days real history for 600519 |
| Tencent (腾讯) | `stock_zh_a_hist_tx` | ✅ 54 days real history |
| All-A code table | `stock_info_a_code_name` | ✅ 5543 stocks |

> East Money is unreachable from this network, so the script automatically falls back to Sina/Tencent.

### Policy lookup workflow

```
need(某税种/某准则) → search official source for latest document number
  → check validity (effective / voided / renewed)
  → extract key points → record into the matching line note
  → if original needed, download & archive under 100-我的数据
```

---

## 铁律 / Iron rules (from 白皮书-v1.3)

1. `wealth数据资产` is read-only; never edit it
2. F drive (USB) is untouchable
3. Only freely-writable area: `E:\dsh-workspace\0814`
4. AI output only goes to the workspace; reports never pollute raw data

---

## License

**MIT** — free to use, modify, redistribute. Policy points are for reference only; authoritative clauses are the official ministry websites.

---

*Crafted by Wealth (威尔思) to keep a one-person firm current on national policy and fluent with free market data.*