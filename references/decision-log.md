# 决策变更日志

记录 AGENTS.md 对既有决策的每一次「存 / 改 / 删 / 并」。既有决策要么被继承，要么被记录地退役，不允许静默丢失。后续对 AGENTS.md 规则的改/删，按其自维护协议第 5 条追加到本文件末尾。

格式：`日期 | 旧值 → 处置 → 新值（或删除原因）`

## 2026-09-08 · 初次起草 AGENTS.md（模式：已初始化优化，源：CLAUDE.md）

1. 项目性质（GitHub 个人主页 README 仓库，纯 Markdown + HTML + shields.io，无构建/依赖/测试） → 存 → 并入 AGENTS.md「项目性质与工具链」，逐字保留。
2. 仓库结构三条（README.md 部署目标 / profile/README.md 同步副本 / update-readme.yml 每 6 小时一次） → 存 → 并入「Permissions」「命令表」「反直觉约定」，并经 workflow 原文核实（cron `0 */6 * * *`）。
3. 编辑流程「修改内容通常在 profile/README.md 或根目录 README.md 进行，两者应保持同步」 → 改 → 实况检查发现两份 README 已漂移（身份标签、精选项目顺序、下载徽章、stats 主题），根版本较新；升级为硬性规则：主编辑点为根 README.md，双份同步 MUST 以 `diff` 无输出为完成标准，并禁止擅自同步（方向由用户决定）。
4. 编辑流程「徽章统一 for-the-badge 风格，配色 #00D4FF / #A855F7 / #0A1628」 → 存 → 并入「反直觉约定」第 4 条；补充观察到 `#FF8000` 为已使用点缀色，明确禁止误改。
5. 编辑流程「shields.io 徽章实时查询，无需手动更新数据」 → 存 → 强化：从"无需"升级为禁令——数字 MUST NOT 写死进 README。
6. 编辑流程「占位符清单在 README 末尾注释中」 → 存 → 并入「反直觉约定」第 5 条，并要求清单与正文双向一致。
7. 品牌规范表（用户名 ErgeAIA、称呼 宝藏二哥AIA、三品牌色） → 并 → 用户名/称呼等事实与 README 末尾占位符清单重复，按双闸去重改为指针；三品牌色值保留在「反直觉约定」第 4 条（该集中清单为唯一处）。
8. GitHub Actions 段（定时 commit .last-updated 触发渲染缓存 + workflow_dispatch） → 存 → 拆入「命令表」（手动触发）与「Permissions」（禁手改 .last-updated）。
9. CLAUDE.md 本体（全文规则） → 改 → 降级为指向 AGENTS.md 的指针文件；全部规则已按上述条目继承，避免双源漂移。
10. 新增·push 须用户确认（非 CLAUDE.md 既有条目） → 新增 → 依据：.codebuddy/memory 中记录的用户既有协作偏好 + README 公开主页属性。
11. 新增·开工前 `git pull --ff-only`（非既有条目） → 新增 → 依据：bot 每 6 小时自动 push main，历史 ed2fd95 已因此产生被迫 merge commit。
12. 新增·Green-Wall/ / .codebuddy/ / logs/ 禁入库（非既有条目） → 新增 → 依据：实况检查（Green-Wall 为独立 git 仓库克隆，origin ErgeAIA/Green-Wall，fork 自 Codennnn/Green-Wall；.codebuddy 为其他 Agent 记忆；logs/ 由全局 gitignore 兜底）。
13. AGENTS.md Permissions「两份 README 当前不同步（根版本较新），MUST NOT 擅自覆盖任何一方」 → 删 → 2026-09-08 精选项目改版时已以根版本为源镜像 profile/README.md（diff 验证一致），漂移解除，临时条目失效；双 README 同步义务仍由「反直觉约定」第 1 条承载。
14. 新增·反直觉约定第 7 条（非既有条目） → 新增 → 依据：用户 2026-09-08 澄清——AI Vault 的 release 发布于 ErgeAIA/updates-dist（公开仓库，当时 6 个 release / 19 次下载），aivault-site 仅是官网仓库且无 release；下载数徽章 MUST 指向 updates-dist，防止后续 Agent 误"纠正"。

## 2026-10-06 · 四区块改版（参照 github.com/37chengshan）+ 品牌色换代

1. 品牌色 `#00D4FF`（青）/ `#A855F7`（紫）/ `#0A1628`，`#FF8000` 为点缀色 → 改 → 全量替换为 **ThemeVault 004 号 `opensquilla/ember`**（`#ff6a2b` 主 / `#ff8047` hover / `#c23e12` deep / `#ffb638` secondary / `#7fd66a` ok / `#1a0f0c`·`#241512` 底 / `#ffe9dc`·`#e6b49a`·`#c08a6e` 文本三档）。依据：用户 2026-10-06 澄清"品牌色早不是青紫，现为 004 号主题"；色值逐条取自 `themes/opensquilla/ember/palette.md`，未自拟。`#FF8000` 的点缀职责由 `--accent-secondary` 与 `--accent` 接手。
2. 命令表「校验两份 README 同步 = `diff profile/README.md README.md`，无输出才算通过」 → 改 → 改为 `git diff --no-index profile/README.md README.md`，并补哈希法。**Why：原命令在 PowerShell 下恒假阳性**——`diff` 是 `Compare-Object` 的别名，它比较的是两个*路径字符串*而非文件内容，任何时候都报"有差异"。本次改版前据此误判过一次。bash 环境下原命令仍有效，但本机 shell 是 PowerShell Core，故以 `-no-index` 版本为准。
3. 反直觉约定第 1 条内引用的 `diff` 同步标准 → 改 → 同步改为 `git diff --no-index`，并写明禁用 `diff` 的原因。
4. 「质量与文档指针」中"机器可校验的仅两件事" → 改 → 改为三件事（加 workflow YAML 可解析），并明确**渲染效果与配色无法离线验证**，必须 push 前网页预览。
5. 徽章规范中"品牌色仅用 #00D4FF / #A855F7 / #0A1628" → 改 → 替换为 ember 语义角色表（含每色的 README 具体用途），旧色标注"已于 2026-10-06 全量退役，不得再出现"。
6. 项目性质中"内容：纯 Markdown + HTML + 第三方徽章服务" → 改 → 补 `assets/` 仓库内快照资产说明，并新增完整的外部服务清单表（含各自注意事项）。依据：改版引入 `github-profile-summary-cards` / `skillicons.dev` / `streak-stats.demolab.com`，依赖面显著扩大，必须留清单以便后续 Agent 知道改动前要实测什么。
7. 新增·反直觉约定第 8 条 → 新增 → 外部图片 URL 必须实测再落盘。依据：`skillicons.dev` 对未收录 id 静默不渲染（实测 comfyui/trae/codex/cursor/claude/anthropic/opencode 缺失、tauri 存在），`github-profile-summary-cards` 参数错误返回错误卡而非 404——两类失效都不会报错，只能靠肉眼渲染发现。
8. 新增·反直觉约定第 9 条 → 新增 → `assets/` 截图是快照非数据源。依据：写意站与个人主页经查均无 `og:image`（写意站 `<head>` 只有 title/description/icon），Next.js 也未生成 opengraph-image，故无法用站点 OG 图替代，只能人工重截。
9. 新增·Permissions 中三个 workflow 的职责边界表 → 新增 → 依据：新增 `snake.yml` / `streak.yml` 后仓库有三个 workflow，其中两个写同一 `dist` 分支，若 cron 撞分钟会并发 push 互相覆盖产物，必须把边界写进规则。两者 cron 刻意错开（03:27 / 05:41 UTC）。
10. 数据区三联卡配色 → 存（作为已知例外） → `github-profile-summary-cards` 的 `theme=radical`（深底 + 粉红标题 + 黄）与 ember 属两个色系，但该服务不支持完整色板覆盖，用户明确选择接受。同服务的 `slateorange` / `maroongold` 是更接近的暖色主题，保留为后续可选项。streak 卡因支持 `theme=custom`，不适用此例外，锁定 ember 色。
11. `update-readme.yml` 中"Fetch repo stats"步骤（抓 3 个仓库星标写入 `$GITHUB_OUTPUT`） → 存（未改） → 该步骤产出的变量后续步骤从未引用，是死代码，多跑三次 API。清理需改动被禁改的 workflow，按 Permissions 须先向用户确认，故本次仅记录不动。
12. `Grep`/校验习惯新增 → 新增 → 查外部图片服务收录情况时，用"批量请求 + 逐个单独渲染 + 灰块即缺失"的方式验证，不依赖服务提供的图标列表页（`skillicons.dev/icons` 列表页经 MCP fetch 无法访问）。

## 2026-10-06 · 首次运行事故与修复（两个 workflow 全绿但产物全 404）

13. `snake.yml` 用 `color_A`~`color_E` / `background` 作为 action input 传色 → 改 → snk v3 的合法 input 只有 `entryPoint` / `args` / `github_user_name` / `github_token` / `outputs`，传上述参数会输出 `Unexpected input(s)` 警告并**静默忽略**（run 仍显示 success）。颜色实际写在 `outputs` 每行查询串：`color_snake`、`color_dots`（正好 5 个，顺序 0 贡献→最高）、`palette`。已改用 `Platane/snk/svg-only@v3` + 查询串传色。
14. `snake.yml` 假定 snk 会自己推分支 → 改 → snk 只把 SVG 写进工作区（日志 `💾 writing to dist/...`），从不推分支，必须自写 git 步骤。**"run 显示 success" 不等于产物存在**，已新增探测步骤与规则 11。
15. `streak.yml` 用第三方 action `peachris/actions-gg-pages@v4` 推送 → 改 → 该仓库已不存在，run 失败于 `Unable to resolve action peachris/actions-gg-pages, repository not found`。**参考作者（37chengshan）本地仍能跑不代表该依赖可用**——不可照抄他人 workflow 的 action 引用。改为纯 git（`git init` + `fetch origin/dist` + `checkout -B` + `commit` + `push`），刻意不用 force push。
16. 新增·Permissions 中"不得引入第三方 push action"约束 → 新增 → 依据：上述事故本质是外部 action 仓库消失导致静默或硬失败。纯 git 无外部依赖，是本仓库（零依赖、无包管理器的定位）唯一稳定的选择。
17. 新增·反直觉约定第 10 条 → 新增 → 页面裂图 ≠ 服务挂。camo 会缓存拉取失败结果。判定顺序：先命令行直连看 HTTP 码与 Content-Type，直连正常而页面裂图即为 camo 缓存，加防缓存参数强制重拉。本次访客徽章即此情形（直连 200/1320B，页面裂图）。
18. 访客徽章 URL 追加 `&v=2` → 新增 → 强制 camo 重新拉取。已实测该服务忽略未知参数（`&v=2`、`&t=1` 均返回 200/1320B）。
19. 新增·反直觉约定第 11 条 → 新增 → `dist` 分支产物必须实际探测 HTTP 码，且改配色后要 `Select-String` 确认产物 SVG 内真的写入了目标色值。依据：本次两个 workflow 首跑全绿但三个 URL 全 404，若只看 run 状态会误判为成功。
20. `snake.yml` 颜色参数用裸 hex（`color_snake=ff6a2b`） → 改 → 必须写成 `%23ff6a2b`（URL 编码的 `#`），否则整个参数被**静默丢弃**，产物退回 GitHub 默认色 `#1b1f23`。run 显示 success、日志无任何警告。依据：一次性生成 8 个变体（裸 hex / `%23` 编码 / 颜色名 / `palette` 预设 / 无参数）逐一比对产物内 hex 值实测确认。
21. 我此前"snake 颜色已生效"的结论 → 撤回 → 系**假阳性**：当时用的正则 `ff6a2b|ff8047|...` 未锚定 `#`，匹配到了 SVG 文件内其他位置的同名字符串。教训：校验产物颜色必须用锚定 `#` 的严格正则（`#[0-9a-fA-F]{6}`），并优先用 `git show origin/dist:<file>` 读已提交内容而非 raw（raw 有边缘缓存，会造成读到的不是最新产物）。
22. `snake.yml` 改用 `Platane/snk/svg-only@v3`（图快） → 改 → 换回 `Platane/snk@v3`。`svg-only` 是另一个更快的实现，不支持 `color_snake`/`color_dots`/`palette`。
23. `snake.yml` 发布步骤用 `rm -f ./*.svg` 清理旧产物 → 改 → 只删两个 snake 文件名。依据：snake 与 streak 共用 `dist` 分支，通配清空会把 `streak.svg` 一并删除（已实际发生，dist 分支一度只剩 2 个文件）。该步骤本是为清理测试变体引入的，属于自己制造的问题。
24. 产物新增"每次改动后核对文件清单"的自检 → 新增 → 依据：#23 的误删是靠 `git ls-tree --name-only origin/dist` 发现的，run 状态与 HTTP 200 都不能发现"文件被删但服务正常"这类问题。
