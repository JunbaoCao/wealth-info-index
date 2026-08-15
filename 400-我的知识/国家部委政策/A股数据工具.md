---
type: 知识
title: A股数据工具
purpose: 免费A股历史行情数据拉取方案
date: 2026-08-14
owner: 威尔思会计师事务所
tags: [工具, 数据, A股, akshare]
---

# A股数据工具

> 免费 A 股历史行情数据的拉取工具整理（**akshare 类开源方案**）。数据用于行情分析、尽调参考、报告佐证。
> 收录于：[[国家部委政策\_索引]]（数据与工具）、300-我的工具。

## 一、首选方案：akshare（推荐）

- **仓库**：github.com/akfamily/akshare
- **许可**：MIT（免费开源）
- **特点**：无需 token、无需登录、直接 pip 安装；覆盖 A 股/港股/美股/基金/期货/债券/宏观数据
- **A 股历史日线**：
  ```python
  import akshare as ak
  df = ak.stock_zh_a_hist(symbol="600519", period="daily",
                          start_date="20250101", end_date="20260814", adjust="qfq")
  ```
- **前复权/后复权**：`adjust` 参数支持 `qfq`（前复权）/ `hfq`（后复权）/ 空（不复权）
- **全 A 列表**：`ak.stock_zh_a_spot_em()`（实时快照）、`ak.stock_info_a_code_name()`（代码名称）
- 依赖 pandas，数据源为东方财富/新浪等公开接口

## 二、其他可选项（备用）

| 工具 | 仓库 | 是否需 token | 特点 |
|------|------|------------|------|
| akshare | akfamily/akshare | 否 | 最全、最活跃，首选 |
| efinance | Micro-sheep/efinance | 否 | 轻量，`ef.stock_zh_a_hist()` |
| qstock | pypi | 否 | 中文友好 |
| tushare | waditu/tushare | 免费档需 token | 需积分，历史数据深、权威 |
| baostock | baostock | 否 | 纯免费，含复权 |

## 三、数据获取脚本（本工作区可运行）

- 见脚本：`E:\dsh-workspace\0814\scripts\fetch_a股.py`（本 Agent 已创建并实测）
- 用法：
  ```
  python fetch_a股.py 600519 20250101 20260814 qfq        # 自动选可用源
  python fetch_a股.py 600519 20250101 20260814 qfq tx      # 指定腾讯
  python fetch_a股.py 600519 20250101 20260814 qfq sina    # 指定新浪
  ```
- 输出：CSV 到 `data/` 目录 + 打印前 5 行

## 四、数据源实测（2026-08-14 在本机验证）

| 源 | akshare 接口 | 本机实测 |
|----|-------------|---------|
| 东方财富 | `stock_zh_a_hist` | ❌ 被掐断（`RemoteDisconnected`，网络不可达） |
| 新浪 | `stock_zh_a_daily` | ✅ 可用（贵州茅台 600519 拉到 54 日真实行情） |
| 腾讯 | `stock_zh_a_hist_tx` | ✅ 可用（同上 54 日） |
| 全A代码表 | `stock_info_a_code_name` | ✅ 可用（5543 只） |

> 结论：**东方财富接口在本机网络下不可用，脚本默认自动回退到新浪/腾讯源**。数据均已核对真实。

## 五、数据落地规范

- 拉到的数据**只写工作区**（`E:\dsh-workspace\0814\data`），不写原始数据根（见 [[白皮书-v1.3]] §5）。
- 落盘目录：`E:\dsh-workspace\0814\data\`，文件名 `{code}_{start}_{end}_{adjust}_{源}.csv`。

## 六、A股数据与业务结合

- 客户为能源/资源类企业（[[国资-知识]]、[[能源-知识]]），可用 A 股行情做行业对标与估值参考。
- 上市公司财务指标可配合 akshare 的 `stock_financial_*` 接口做同业对比。

---
*end of A股数据工具*