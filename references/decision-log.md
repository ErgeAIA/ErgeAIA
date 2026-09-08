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
