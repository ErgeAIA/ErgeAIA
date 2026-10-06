# AGENTS.md

本文件是本仓库（GitHub: ErgeAIA/ErgeAIA，本地 D:\Workspace\ErgeAIA）中人类与任何 Agent 之间的合作协议。规则对所有 Agent 生效，不限于特定工具。

## Permissions（权限边界）

**IMPORTANT — 本仓库的 README.md 渲染为用户 GitHub 公开主页，任何 push 立即改变其公开形象。**

- **YOU MUST NOT 执行 `git push`**，除非用户在该次操作前明确确认。本地 commit 无需逐次确认。
- **YOU MUST NOT 将以下路径加入提交**：`Green-Wall/`（独立 git 仓库的本地克隆）、`.codebuddy/`（其他 Agent 的记忆目录）、`logs/`（本地日志）、`.env` 及任何密钥、凭据。
- **YOU MUST NOT 手动编辑 `.last-updated`**：该文件由 GitHub Actions bot 每 6 小时覆写一次。
- **YOU MUST NOT 修改 `.github/workflows/update-readme.yml`**（cron、bot 提交身份、push 逻辑），如确需改动，先向用户说明并确认。
- **`.github/workflows/` 现有三个 workflow，职责边界如下**，改动前先确认不会互相覆盖产物：

  | workflow | 产物 | 写入位置 | 触发 |
  |---|---|---|---|
  | `update-readme.yml` | `.last-updated` | `main` 分支 | 每 6 小时 + 手动 |
  | `snake.yml` | `github-contribution-grid-snake{,-dark}.svg` | `dist` 分支 | 每天 03:27 UTC + 手动 |
  | `streak.yml` | `streak.svg` | `dist` 分支 | 每天 05:41 UTC + 手动 |

  `snake.yml` 与 `streak.yml` 写同一 `dist` 分支，**cron 必须错开**（当前已错开，勿改成同一分钟），否则并发 push 会互相覆盖产物。
- **两个 workflow 均只用原生 git 推送，不得引入第三方 push action**。原用 `peachris/actions-gg-pages` 已失效（仓库不存在，报 `Unable to resolve action / repository not found`），改为 `git init` + `fetch origin/dist` + `checkout -B` + `commit` + `push`，**不使用 force push**。
- **snk v3 的颜色不是 action input**，只能写在 `outputs` 每行的查询串里（`color_snake` / `color_dots`(正好 5 个，0 贡献→最高) / `palette`）。传 `color_A`~`color_E`、`background` 会输出 `Unexpected input(s)` 警告并**静默忽略**。另：snk 只把 SVG 写进工作区，**从不推分支**，推送必须自己写 git 步骤。
- 不确定某文件是否应入库时：先询问，不要 `git add`。

## 项目性质与工具链

GitHub 个人主页 README 仓库（special repo：根目录 README.md 渲染在 github.com/ErgeAIA 主页）。

- 内容：纯 Markdown + HTML + 第三方图片/徽章服务 + 少量仓库内静态图片
- 仓库内图片资产：`assets/`（`xieyi-preview.png` 写意站截图、`site-preview.png` 个人主页截图）。**这两张不会自动更新**，站点改版后必须手动重新截图覆盖，否则主页展示的是旧界面。
- 外部图片服务清单（改动前先实测能否渲染）：

  | 服务 | 用途 | 注意事项 |
  |---|---|---|
  | `shields.io` | 实时数字徽章（星标/下载/更新） | 唯一实时数据源，数字 MUST NOT 写死 |
  | `readme-typing-svg` | 顶部打字机动画 | |
  | `github-profile-summary-cards.vercel.app` | 数据区三联卡 | 配色由 `theme` 固定，**不支持完整色板覆盖** |
  | `streak-stats.demolab.com` | 贡献连续天数卡 | 支持 `theme=custom` 全自定义配色 |
  | `skillicons.dev` | 技术栈图标墙 | **未收录的 id 静默不渲染**，改 id 前必须逐个实测 |
  | `visitor-badge.laobi.icu` | 访问计数 | |
  | `dist` 分支（自建，非外部服务） | 贪吃蛇 / streak 图 | 由 `snake.yml` / `streak.yml` 生成 |

- 无构建系统、无包管理器、无依赖、无测试、无 lint —— 仓库级没有可运行的构建命令
- 唯一"部署"动作：push 到 main 即上线
- **首次启用 / 删改 workflow 后**：`dist` 分支产物可能尚未生成，README 图片会裂图。必须手动触发一次 `gh workflow run snake.yml`（必要时再跑 `streak.yml`）。

## 命令表

| 场景 | 命令（可复制原文） | 说明 |
|---|---|---|
| 每次开工前（MUST） | `git pull --ff-only` | bot 每 6 小时自动 push main，不先拉取必然产生冲突/merge commit；失败时停止并询问用户 |
| 校验两份 README 同步 | `git diff --no-index profile/README.md README.md` | 无输出才算同步通过。**不要用 `diff`**：PowerShell 下 `diff` 是 `Compare-Object` 的别名，它比较的是两个*路径字符串*，恒定报"有差异" |
| 同上（哈希法） | `(Get-FileHash README.md).Hash -eq (Get-FileHash profile/README.md).Hash` | 返回 `True` 即一致 |
| 查看真实人工变更 | `git log --oneline --grep="refresh README stats" --invert-grep` | 过滤 bot 自动提交噪音 |
| 手动触发统计刷新 | `gh workflow run update-readme.yml` | 即 workflow_dispatch，需 gh CLI 已登录 |
| 手动生成贪吃蛇 / streak 图 | `gh workflow run snake.yml` / `gh workflow run streak.yml` | 首次启用或产物缺失时必跑 |
| 上线（需用户确认） | `git push` | 即发布公开主页 |

## 反直觉约定（MUST READ）

1. **双 README 同步**：根 `README.md` 是部署目标；`profile/README.md` 是编辑/预览副本。内容修改 MUST 同时落两份，并以 `git diff --no-index profile/README.md README.md` 无输出作为完成标准（**不要用 `diff` 命令**，PowerShell 下恒假阳性，详见命令表）。当前编辑主战场是根 `README.md`，改完后镜像到 `profile/README.md`。
2. **bot 提交噪音**：提交历史中大量 `chore: refresh README stats` 是 github-actions[bot] 的自动提交（每 6 小时一次），不代表任何人的工作内容；分析历史时必须过滤。
3. **数据永远不要写死**：shields.io 徽章实时查询 GitHub API，星标/下载量等数字 MUST NOT 手工写入 README。
4. **徽章规范**：统一 `style=for-the-badge`；品牌色取自 **ThemeVault 004 号主题 `opensquilla/ember`**，唯一权威来源是 `D:\Workspace\Code\ThemeVault\themes\opensquilla\ember\palette.md`（报编号 → 查 `INDEX.json` 的 `theme.number` → 读对应 `palette.md`）：

   | 语义角色 | 色值 | README 中的用途 |
   |---|---|---|
   | `--accent` | `#ff6a2b` | 主色：B 站徽章、星标徽章、打字机动画、贪吃蛇主色 |
   | `--accent-hover` | `#ff8047` | Codex 徽章、streak 当前连续数 |
   | `--accent-deep` | `#c23e12` | 知乎 / 邮箱徽章、更新时间徽章、Trae 徽章 |
   | `--accent-secondary` | `#ffb638` | Open Code 徽章、下载徽章、streak 当前连续标签 |
   | `--ok` | `#7fd66a` | 微信徽章、streak 日期 |
   | `--bg` / `--card` | `#1a0f0c` / `#241512` | 深色背景、贪吃蛇底色、streak 底色、访客徽章左色 |
   | `--text` / `--text-muted` / `--text-dim` | `#ffe9dc` / `#e6b49a` / `#c08a6e` | streak 文字三档 |

   旧色 `#00D4FF`（青）/ `#A855F7`（紫）/ `#0A1628` / `#FF8000` **已于 2026-10-06 全量退役**，不得再出现。`#FF8000` 原本的"点缀色"职责由 `--accent-secondary` 与 `--accent` 接手。
   **唯一色系例外**：数据区三联卡用 `github-profile-summary-cards` 的 `theme=radical`（深底 + 粉红标题 + 黄），该服务配色由主题固定、无法锁定 ember 色板，用户已知悉并接受。streak 卡**不受此限**——它支持 `theme=custom`，MUST 填 ember 色。
5. **占位符清单**：根 `README.md` 末尾的 HTML 注释维护着全部可替换文案（社交链接、称呼、项目链接、语录）。修改文案 MUST 先对照该清单，并保持清单与正文一致。
6. **`Green-Wall/` 是独立仓库**：origin 为 ErgeAIA/Green-Wall（fork 自 Codennnn/Green-Wall），仅是本地克隆，与本仓库无版本关联。在其中的一切工作遵循其自身仓库的规则，不得将任何改动带入本仓库提交。
7. **AI Vault 的下载数据在 `ErgeAIA/updates-dist`**：release 发布于独立发行仓库 updates-dist，`aivault-site` 仅是官网仓库。AI Vault 卡的下载数徽章 MUST 指向 updates-dist，不得"纠正"回 aivault-site。
8. **外部图片 URL 必须先实测再落盘**：本仓库没有任何能离线验证图片渲染的手段，写进 README 的每个第三方图片 URL 都必须先在浏览器实际渲染确认。已知两个静默失效陷阱：
   - `skillicons.dev` 未收录的 id **不报错、也不显示**（实测 `comfyui` / `trae` / `codex` / `cursor` / `claude` / `anthropic` / `opencode` 全部缺失，`tauri` 存在）。技术栈因此是"图标墙 + shields.io 徽章"混合结构，不是漏改。
   - `github-profile-summary-cards` 参数拼错不会 404，而是返回一张错误卡片。
9. **`assets/` 里的截图是快照，不是数据源**：`xieyi-preview.png` / `site-preview.png` 均为人工截取，站点改版后 MUST 手动重截覆盖。写意站与个人主页均**未提供 `og:image`**，无法用站点自身 OG 图替代。
10. **图片显示裂图 ≠ 服务挂了**：GitHub 的 camo 图片代理会**缓存拉取失败的结果**。判定顺序 MUST 是：先用命令行直连该 URL 看 HTTP 码与 `Content-Type`（`Invoke-WebRequest -Uri ... -UseBasicParsing`）→ 若直连正常而页面裂图，就是 camo 缓存，追加一个防缓存参数（如 `&v=2`，前提是该服务忽略未知参数）让 camo 重新拉取。不要因为页面裂图就去换服务。本仓库的 `update-readme.yml` 每 6 小时提交 `.last-updated` 也是同一个目的：触发 GitHub 重新渲染。
11. **`dist` 分支产物验证**：改完 workflow 后不能只看 run 显示 `success` 就完事——snk 这类工具**不推分支**，可能 run 全绿但 URL 全 404。必须实际探测三个 URL 的 HTTP 码：`dist/streak.svg`、`dist/github-contribution-grid-snake.svg`、`dist/github-contribution-grid-snake-dark.svg`。同理，改配色后要 `Select-String` 确认产物 SVG 里真的写入了目标色值。

## 质量与文档指针

- 无测试、无 CI 内容校验。机器可校验的仅三件事：双 README 一致（`git diff --no-index`）、HTML/Markdown 不含明显语法损坏、workflow YAML 可解析；**渲染效果与配色必须靠 push 前在 GitHub 网页预览确认**。
- 用户名、称呼、品牌语录、社交链接等事实的唯一权威来源是根 `README.md` 末尾占位符注释。
- 历史决策的存/改/删记录见 `references/decision-log.md`。

## 自维护协议

1. 视本文件为代码：任何改变规则的变更，MUST 在同一 PR/任务中同步更新本文件，否则视为规则漂移。
2. 就近更新：新规则写入离问题发生处最近的作用域；若未来出现纳入本仓库的子项目，规则写入对应子目录的本地 AGENTS.md，不堆根文件。
3. 提交前自检：命令更名、workflow 调整、品牌色变更、文案变更后，核对本文档准确性，过期内容当场更新。
4. 周期维护：每次实质性主页改版时复查本文件，清除失效链接与废弃约定。
5. 变更留痕：对既有规则的「改/删」决策 MUST 追加到 `references/decision-log.md`，随同一提交入库。
