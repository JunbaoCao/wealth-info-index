---
type: 工具指针
title: A股数据工具
scope: 中性工具，免费 A 股历史行情拉取
date: 2026-08-14
owner: 威尔思会计师事务所
tags: [工具, 数据, A股, akshare]
---

# A股数据工具（免费）

> 中性工具指针：用 `akshare`（MIT、免费、无需 token）拉取 A 股历史行情。仅工具，不含任何政策内容。

## 用法
- 脚本：`scripts/fetch_a股.py`
  ```
  python fetch_a股.py 600519 20250101 20260814 qfq        # 自动选可用源
  python fetch_a股.py 600519 20250101 20260814 qfq tx      # 指定腾讯
  python fetch_a股.py 600519 20250101 20260814 qfq sina    # 指定新浪
  ```
- 输出：CSV 到 `data/` 目录 + 打印前 5 行

## 数据源实测（本机 2026-08-14）
| 源 | akshare 接口 | 实测 |
|----|-------------|------|
| 东方财富 | `stock_zh_a_hist` | ❌ 被掐断（网络不可达） |
| 新浪 | `stock_zh_a_daily` | ✅ 可用（600519 拉到 54 日真实行情） |
| 腾讯 | `stock_zh_a_hist_tx` | ✅ 可用（同上） |
| 全A代码表 | `stock_info_a_code_name` | ✅ 可用 |

> 东方财富接口在本机不可达，脚本默认自动回退到新浪/腾讯源。

## 工具替代项
- efinance（轻量）、baostock（纯免费）、tushare（需 token）

## 关联
- [[信息索引\_索引]]

---
*end of A股数据工具*