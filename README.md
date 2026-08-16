# wealth-info-index · Wealth Information Index

**English** | [中文](README.zh.md)

**Wealth (Shanxi Wei Er Si Certified Public Accountants (General Partnership))** · an open-source **information index library**.

**License: MIT**

> This is the **information index library** of Shanxi Wei Er Si Certified Public Accountants (General Partnership). It does **not** store any policy, regulatory, or sensitive document content. It keeps only **pointers and links** — telling you *where* a given piece of information lives (official sources, local data areas) and *how to find it*. Everything substantive stays at its authoritative origin; this repo only navigates.

---

## What it is

An **index of where information lives** for the firm. Its job is **navigation**: given a topic, point to the authoritative source and the local archive — never to reproduce the material here.

**Core idea: index the location, not the content.**

- Keeps a **navigation tree** of topic areas and their authoritative sources.
- Keeps a **local data map** of where archived originals live (read-only areas).
- Keeps **tooling pointers** (e.g., free A-share data script) without bundling sensitive data.

---

## Features

- ✅ **Index-only** — links and pointers; no document bodies, no sensitive wording.
- ✅ **Authoritative-source map** — for each topic, the official/home source to consult.
- ✅ **Local-archive map** — where originals are kept (read-only), so the vault never drifts.
- ✅ **Tooling pointer** — a free A-share historical-data script (akshare), neutral tooling.
- ✅ **Obsidian-ready** — `[[ ]]` wikilinks and a MOC index for quick navigation.

---

## Repository structure

```
wealth-info-index/
├── README.md              ← This file (English usage guide)
├── README.zh.md           ← Chinese usage guide
├── 000-主页.md            ← Global entry (navigation home)
├── 我的数据/          ← Local data map + tooling + setup summary
├── 我的工作/          ← Work log, current projects
├── 我的工具/          ← skill + DeepSeek Harness index
├── 我的知识/          ← Knowledge index (pointers only)
│   └── 信息索引/        ← ★ Topic index: authoritative sources + links
│       ├── _索引.md     ←   Navigation home for topic index
│       ├── 审计-知识.md ←   Audit topic → source pointer
│       ├── 会计-知识.md ←   Accounting topic → source pointer
│       ├── 税务-知识.md ←   Tax topic → source pointer
│       ├── 法律-知识.md ←   Law topic → source pointer
│       ├── 合规-知识.md ←   Compliance topic → source pointer
│       ├── 国资-知识.md ←   SOE-assets topic → source pointer
│       ├── 能源-知识.md ←   Energy topic → source pointer
│       └── A股数据工具.md ← Neutral tooling (free A-share data)
├── 我的规范/          ← Working norms / execution rules
└── scripts/             ← Neutral tooling scripts
    ├── fetch_a股.py     ←   Free A-share history (multi-source fallback)
    └── akshare_test.py  ←   Multi-endpoint validation
```

---

## Quick start

### 1) Open as a navigation index (human view)

Open the repository root in **Obsidian**; start at `000-主页.md` and navigate from there. The vault shows *where* information lives, not the information itself.

### 2) Neutral tooling: free A-share data

Requires Python 3 + akshare:

```powershell
pip install akshare pandas
python scripts/fetch_a股.py 600519 20250101 20260814 qfq    # auto-select available source
```

Output CSV to `data/` and print the first 5 rows.

---

## Acknowledgements

The free A-share historical-data script in this repo is built on **akshare** — an excellent MIT-licensed open-source financial-data library by **akfamily**. Many thanks to its maintainers and contributors. https://github.com/akfamily/akshare

## License

**MIT** — free to use, modify, redistribute. This library contains no policy or sensitive content; it only points to authoritative sources.

---

*Crafted by Wealth (Shanxi Wei Er Si Certified Public Accountants (General Partnership)) as a clean information index — navigate the location, never the content.*