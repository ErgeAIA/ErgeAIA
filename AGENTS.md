# AGENTS.md

本文件是本仓库（GitHub: ErgeAIA/ErgeAIA，本地 D:\Workspace\ErgeAIA）中人类与任何 Agent 之间的合作协议。规则对所有 Agent 生效，不限于特定工具。

## Permissions（权限边界）

**IMPORTANT — 本仓库的 README.md 渲染为用户 GitHub 公开主页，任何 push 立即改变其公开形象。**

- **YOU MUST NOT 执行 `git push`**，除非用户在该次操作前明确确认。本地 commit 无需逐次确认。
- **YOU MUST NOT 将以下路径加入提交**：`Green-Wall/`（独立 git 仓库的本地克隆）、`.codebuddy/`（其他 Agent 的记忆目录）、`logs/`（本地日志）、`.env` 及任何密钥、凭据。
- **YOU MUST NOT 手动编辑 `.last-updated`**：该文件由 GitHub Actions bot 每 6 小时覆写一次。
- **YOU MUST NOT 修改 `.github/workflows/update-readme.yml`**（cron、bot 提交身份、push 逻辑），如确需改动，先向用户说明并确认。
- 不确定某文件是否应入库时：先询问，不要 `git add`。

## 项目性质与工具链

GitHub 个人主页 README 仓库（special repo：根目录 README.md 渲染在 github.com/ErgeAIA 主页）。

- 内容：纯 Markdown + HTML + shields.io / readme-typing-svg / visitor-badge 等第三方徽章服务
- 无构建系统、无包管理器、无依赖、无测试、无 lint —— 仓库级没有可运行的构建命令
- 唯一"部署"动作：push 到 main 即上线

## 命令表

| 场景 | 命令（可复制原文） | 说明 |
|---|---|---|
| 每次开工前（MUST） | `git pull --ff-only` | bot 每 6 小时自动 push main，不先拉取必然产生冲突/merge commit；失败时停止并询问用户 |
| 校验两份 README 同步 | `diff profile/README.md README.md` | 无输出才算同步通过 |
| 查看真实人工变更 | `git log --oneline --grep="refresh README stats" --invert-grep` | 过滤 bot 自动提交噪音 |
| 手动触发统计刷新 | `gh workflow run update-readme.yml` | 即 workflow_dispatch，需 gh CLI 已登录 |
| 上线（需用户确认） | `git push` | 即发布公开主页 |

## 反直觉约定（MUST READ）

1. **双 README 同步**：根 `README.md` 是部署目标；`profile/README.md` 是编辑/预览副本。内容修改 MUST 同时落两份，并以 `diff profile/README.md README.md` 无输出作为完成标准。当前编辑主战场是根 `README.md`，改完后镜像到 `profile/README.md`。
2. **bot 提交噪音**：提交历史中大量 `chore: refresh README stats` 是 github-actions[bot] 的自动提交（每 6 小时一次），不代表任何人的工作内容；分析历史时必须过滤。
3. **数据永远不要写死**：shields.io 徽章实时查询 GitHub API，星标/下载量等数字 MUST NOT 手工写入 README。
4. **徽章规范**：统一 `style=for-the-badge`；品牌色仅用 `#00D4FF`（主色）/ `#A855F7`（辅色）/ `#0A1628`（深色背景）；`#FF8000` 为已投入使用的点缀色（打字机动画、下载徽章），不得"顺手统一"掉。
5. **占位符清单**：根 `README.md` 末尾的 HTML 注释维护着全部可替换文案（社交链接、称呼、项目链接、语录）。修改文案 MUST 先对照该清单，并保持清单与正文一致。
6. **`Green-Wall/` 是独立仓库**：origin 为 ErgeAIA/Green-Wall（fork 自 Codennnn/Green-Wall），仅是本地克隆，与本仓库无版本关联。在其中的一切工作遵循其自身仓库的规则，不得将任何改动带入本仓库提交。
7. **AI Vault 的下载数据在 `ErgeAIA/updates-dist`**：release 发布于独立发行仓库 updates-dist，`aivault-site` 仅是官网仓库。AI Vault 卡的下载数徽章 MUST 指向 updates-dist，不得"纠正"回 aivault-site。

## 质量与文档指针

- 无测试、无 CI 内容校验。机器可校验的仅两件事：双 README diff 一致、HTML/Markdown 不含明显语法损坏；其余靠 push 前在 GitHub 网页预览确认渲染效果。
- 用户名、称呼、品牌语录、社交链接等事实的唯一权威来源是根 `README.md` 末尾占位符注释。
- 历史决策的存/改/删记录见 `references/decision-log.md`。

## 自维护协议

1. 视本文件为代码：任何改变规则的变更，MUST 在同一 PR/任务中同步更新本文件，否则视为规则漂移。
2. 就近更新：新规则写入离问题发生处最近的作用域；若未来出现纳入本仓库的子项目，规则写入对应子目录的本地 AGENTS.md，不堆根文件。
3. 提交前自检：命令更名、workflow 调整、品牌色变更、文案变更后，核对本文档准确性，过期内容当场更新。
4. 周期维护：每次实质性主页改版时复查本文件，清除失效链接与废弃约定。
5. 变更留痕：对既有规则的「改/删」决策 MUST 追加到 `references/decision-log.md`，随同一提交入库。
