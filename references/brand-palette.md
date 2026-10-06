# 品牌色板参考（opensquilla/ember）

> 给人类阅读的色板全量对照与配色决策记录。
> **AGENTS.md 只保留可执行规则**（用哪个色、禁用哪个色），色板全量、来源与取舍过程写在本文件。

## 唯一权威来源

品牌色取自用户的主题色板库项目 **ThemeVault** 的 **004 号主题 `opensquilla/ember`**。

查色流程（本地操作，路径不入库）：报主题编号 → 查 ThemeVault 的 `INDEX.json` 定位 `theme.number` → 读 `themes/<family>/<id>/palette.md` 全表。ThemeVault 的本地路径见 Agent 记忆。

## 色板全量

### 中性色（背景 / 文本 / 边框）

| 语义角色 | 色值 | README 中的用途 |
|---|---|---|
| `--bg` | `#1a0f0c` | 贪吃蛇深色底、streak 卡底色、访客徽章左色 |
| `--card` / `--bg-surface` | `#241512` | 贪吃蛇深色模式 0 贡献格 |
| `--bg-hover` | `#452c23` | 贪吃蛇深色模式低贡献格 |
| `--text` | `#ffe9dc` | streak 侧边数字 |
| `--text-muted` | `#e6b49a` | streak 侧边标签 |
| `--text-dim` | `#c08a6e` | streak 描边、侧边文字 |
| `--border` | `#4a2c22` | GitHub 徽章底色（`GitHub-xieyi` / `GitHub-ErgeAIA`） |

### 强调色

| 语义角色 | 色值 | README 中的用途 |
|---|---|---|
| `--accent` | `#ff6a2b` | **主色**：B 站徽章、星标徽章、打字机动画、贪吃蛇主色、Cursor / ComfyUI 徽章、站点入口徽章 |
| `--accent-hover` | `#ff8047` | Codex 徽章、贪吃蛇蛇身（深色模式）、streak 当前连续数 |
| `--accent-deep` | `#c23e12` | 知乎 / 邮箱徽章、更新时间徽章、Trae 徽章、贪吃蛇浅色模式蛇身 |
| `--accent-secondary` | `#ffb638` | Open Code 徽章、下载徽章、streak 当前连续标签、贪吃蛇高贡献格 |

### 功能状态色

| 语义角色 | 色值 | README 中的用途 |
|---|---|---|
| `--ok` | `#7fd66a` | 微信徽章、streak 日期 |

## AI 工具徽章配色

`skillicons.dev` 未收录 Claude / Cursor / Trae / Qoder / CodeBuddy / DeepSeek / OpenCode / Codex / ComfyUI，因此 AI 工具一律用 shields.io 文字徽章。配色规则：**有强品牌识别度的保留品牌色，其余用 ember 色阶区分**。

| 工具 | 徽章底色 | 说明 |
|---|---|---|
| Claude | `#D97706` | 保留品牌色（Anthropic 橙棕） |
| Cursor | `#ff6a2b` | `--accent` |
| ComfyUI | `#ff6a2b` | `--accent` |
| Qoder | `#ff6a2b` | `--accent`；shields.io 无 `qoder` logo slug，故纯文字 |
| Codex | `#ff8047` | `--accent-hover` |
| CodeBuddy | `#ff8047` | `--accent-hover`；无 `codebuddy` logo slug |
| DeepSeek Harness | `#c23e12` | `--accent-deep`；**有** `deepseek` logo slug |
| Trae | `#c23e12` | `--accent-deep`；无 logo slug |
| Open Code | `#ffb638` | `--accent-secondary` |

## 贪吃蛇配色推导

snk 的 `color_dots` 必须是**正好 5 个**颜色，顺序为「0 贡献 → 最高贡献」，因此直接映射 `--bg-surface` → `--accent-secondary` 的梯度：

| 档位 | 浅色模式（白底） | 深色模式 |
|---|---|---|
| 0 贡献 | `#ebedf0` | `#241512` |
| 1 | `#dfe1e6` | `#452c23` |
| 2 | `#ffb638` | `#c23e12` |
| 3 | `#ff6a2b` | `#ff6a2b` |
| 4（最高） | `#c23e12` | `#ffb638` |

蛇身：浅色模式用 `--accent-deep`，深色模式用 `--accent-hover`，保证在各自背景上都有足够对比。

## 退役色

以下颜色**已全量退役**，不得再出现在本仓库任何文件中（含注释）：

| 旧色 | 原用途 | 接手者 |
|---|---|---|
| `#00D4FF` 青 | 主色（B 站徽章、星标徽章、打字机动画、访客徽章右色） | `--accent` |
| `#A855F7` 紫 | 辅色（知乎 / 邮箱徽章、更新时间徽章） | `--accent-deep` |
| `#0A1628` | 深色背景（访客徽章左色） | `--bg` |
| `#FF8000` | 点缀色（打字机动画、下载徽章） | `--accent-secondary` + `--accent` |

## 数据区三联卡：为何选 `date_night`

`github-profile-summary-cards` 的配色由 `theme` 固定、**不支持完整色板覆盖**，因此需要在服务自带主题里挑最接近 ember 的。实测各候选主题的底色与 ember 对比：

| 主题 | 卡片底色 | 标题色 | 结论 |
|---|---|---|---|
| **`date_night`** | **`#170f0c`** | `#e1b2a2` | **选定**。底色与 `--bg #1a0f0c` 仅差 R=3，标题与 `--text-muted #e6b49a` 极接近，视觉上与 streak 卡成为同一块表面 |
| `maroongold` | `#260000` | `#e0aa3e` | 纯深红，过饱和 |
| `slateorange` | `#36393f` | `#faa627` | 冷灰，与暖色品牌不搭 |
| `holi` | `#030314` | `#d6e7ff` | 冷蓝黑 |
| ~~`radical`~~ | 深底 | `#fe428e` 粉红 | 已弃用：粉红标题与 ember 橙属两个色系 |

**换主题前 MUST 先比对底色**，不要凭主题名里的颜色词猜。

该服务另有速率限制：短时间并发请求多张卡会返回 `ERROR!!! Cards are temporarily rate limited` 卡片（不是 404）。预览时逐张请求并留间隔。

streak 卡不适用上述限制——`streak-stats.demolab.com` 支持 `theme=custom`，可逐项指定颜色，已锁定 ember。
