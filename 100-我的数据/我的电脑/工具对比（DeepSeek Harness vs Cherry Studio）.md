---
tags:
  - 电脑
  - 工具
  - DeepSeek Harness
  - Cherry Studio
  - 对比
created: 2026-08-14
---

# 🛠️ 工具对比：DeepSeek Harness vs Cherry Studio

> 这台电脑上两个 AI 工作台的**全面对比**：各自是什么、装在哪、能力差异、skill/mcp 机制。返回：[[我的电脑-索引]]

---

## 一、先搞清楚它俩是什么

| | **DeepSeek Harness (DSH)** | **Cherry Studio** |
|--|--|--|
| **本质** | 一个 AI **开发框架/运行环境**（开源，跑在你本地），我（当前 Agent）就跑在这个环境里 | 一个**桌面 AI 助手应用**（图形界面软件），你日常和 AI 聊天、用 AI 干活的主要入口 |
| **形态** | 命令行/后端为主，配一个 Web 界面 | 桌面窗口软件（类似微信/QQ 那种装好的应用） |
| **安装位置** | `E:\dsh-workspace\deepseek-harness`（源码仓库） | 配置在 `C:\Users\HP\AppData\Roaming\CherryStudio` |
| **版本** | 开发仓库（无固定版本号） | 2.0.5 |
| **谁在用** | 开发者/技术用户，我（智能体）在这种环境里跑 | 普通用户到进阶用户，你日常主要用它 |

> 💡 **一句话**：Cherry Studio 是给你用的"前台"，DeepSeek Harness 是给我（智能体）跑的"后台/引擎"。

---

## 二、两者都有的"共同概念"

虽然形态不同，但**核心机制高度相似**，这是你能"共享复用"的基础：

| 概念 | DeepSeek Harness | Cherry Studio | 是否对应 |
|------|------------------|---------------|----------|
| **技能 Skill** | `.agents\skills\` 下每个文件夹 = 一个 skill（含 `SKILL.md`） | `Data\Skills\` 下每个文件夹 = 一个 skill（含 `SKILL.md`） | ✅ **格式一样，都是 SKILL.md** |
| **智能体 Agent** | 用 `cordis.yml` 预设定义（agent-presets） | 用 `Agents\<GUID>\SOUL.md + USER.md` 定义 | ⚠️ **机制不同，需转换** |
| **工具/MCP** | 通过 Cordis 插件系统 + MCP provider | 内置 3 个 MCP 服务：`mcp__cherry-tools__*`、`mcp__agent-memory__*`、`mcp__skills__*` | ⚠️ **机制不同** |
| **记忆 Memory** | 会话/存储机制（`.dsh\sessions`） | 知识库 + `agent-memory` MCP | ⚠️ 不同实现 |
| **运行库/工具链** | Node.js、pnpm（在仓库内） | 自带 bun、uv、mise、rg（在 `.cherrystudio\bin`） | 各管各的 |

---

## 三、你的技能（Skill）清单对照

### 🟢 Cherry Studio 现有技能（`Data\Skills\`）
| 技能名 | 作用 | 位置 |
|--------|------|------|
| `cherry-tool-guide` | Cherry 内置工具/脚本路由指南 | `Data\Skills\cherry-tool-guide\SKILL.md` |
| `find-skills` | 查找可用技能 | `Data\Skills\find-skills\SKILL.md` |
| `skill-creator` | 创建新技能 | `Data\Skills\skill-creator\SKILL.md` |
| `tavily` | 联网搜索（Tavily 搜索 API） | `Data\Skills\tavily\SKILL.md` |

### 🟢 DeepSeek Harness 现有技能（`.agents\skills\`）
| 技能名 | 作用 |
|--------|------|
| `dsh-archive-agent-notes` | 归档 agent 笔记 |
| `dsh-code-review` | 代码审查 |
| `dsh-doc-site-sync` | 文档站点同步 |
| `dsh-doc-standards` | 文档规范 |
| `dsh-find-simplifications` | 找简化点 |
| `dsh-merging-stacked-prs` | PR 合并 |
| `dsh-pre-push-checks` | 提交前检查 |
| `dsh-prose-standard` | 文风/散文规范 |
| `dsh-translate-docs` | 文档翻译 |
| `dsh-trim-cot-leakage` | 思维链清理 |
| `record-browser-gif` | 录制浏览器 GIF |

> ⚠️ **结论**：两边的技能**内容完全不重叠**——Cherry 的是"用户日常助手"类，DSH 的是"开发/代码"类。**没有真正需要去重的重复技能**，只有功能互补。

---

## 四、你的智能体（Agent）清单对照

### 🟢 Cherry Studio 里的智能体（`Data\Agents\`）
| 智能体 | 身份 | 说明 |
|--------|------|------|
| `62843a8e-...` | **曹军宝**（Cao Junbao） | 已配置人格（SOUL.md）+ 用户信息（USER.md），是主智能体 |
| `0091a7af-...` | 未命名 | SOUL.md / USER.md 为**空**，是空壳/待配置 |
| `cherry-support` | 官方支持助手 | Cherry 自带 |

### 🟢 DeepSeek Harness 里的预设（`apps\cli\config\agent-presets\`）
| 预设 | 说明 |
|------|------|
| `cordis` | 插件化动态预设（**我当前跑的这个**，含 skill 系统） |
| `code` | 代码预设 |
| `standard` | 标准预设 |
| `minimal` | 最小预设 |

> ⚠️ **结论**：两边的"智能体"**定义机制完全不同**。Cherry 用 `SOUL.md`（人格文本），DSH 用 `cordis.yml`（声明式配置）。**不能直接互拷，需要转换**。

---

## 五、关键差异总结（一张表看透）

| 维度 | DeepSeek Harness | Cherry Studio | 你该知道 |
|------|------------------|---------------|----------|
| 使用场景 | 跑智能体/开发 | 日常对话/办公 | 两个都要用 |
| 技能格式 | `SKILL.md` 文件夹 | `SKILL.md` 文件夹 | ✅ 可互相借鉴 |
| 智能体格式 | `cordis.yml` 预设 | `SOUL.md`+`USER.md` | ⚠️ 不能直拷 |
| MCP 机制 | Cordis 插件 + MCP provider | 内置 3 个 MCP 服务 | ⚠️ 各自独立 |
| 配置文件 | `E:\dsh-workspace\deepseek-harness` | `C:\Users\HP\AppData\Roaming\CherryStudio` | 位置不同 |
| 运行时 | Node.js/pnpm | bun/uv/mise/rg | 各管各的 |

---

## 六、结论与建议

1. **不是谁替代谁**：Cherry Studio 是你日常入口，DeepSeek Harness 是智能体引擎，**互补共存**。
2. **"共享文件夹"做不到物理共用**：两边配置路径、格式、机制都不同，**不可能一个文件夹同时被两套软件识别**。
3. **能做到的是"逻辑对齐"**：建一个统一的**共享资源索引**文件夹，把两边的 skill、agent、mcp 都登记在册，两边都指向它来对照——这是现实可行的方案（见 [[共享资源索引]]）。
4. **需要处理"重复"**：实际你的 skill 不重复（Cherry 是助手类、DSH 是开发类），真正要整理的是"新智能体"的规划（见 [[工具整理步骤]]）。

---

*相关：[[我的电脑-索引]] · [[共享资源索引]] · [[工具整理步骤]]*