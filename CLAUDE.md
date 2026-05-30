# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目性质

GitHub 个人主页 README 仓库，纯 Markdown + HTML + shields.io 徽章，无构建系统、无依赖、无测试。

## 仓库结构

- `README.md` — 仓库根目录的个人主页 README（部署目标）
- `profile/README.md` — README 的编辑/预览副本，内容与根目录同步
- `.github/workflows/update-readme.yml` — GitHub Actions 定时任务，每 6 小时 commit 一次触发 GitHub 缓存刷新

## 编辑流程

1. 修改内容通常在 `profile/README.md` 或根目录 `README.md` 进行，两者应保持同步
2. 徽章统一使用 `for-the-badge` 风格，配色遵循品牌色系（`#00D4FF` / `#A855F7` / `#0A1628`）
3. shields.io 徽章为实时查询 GitHub API，无需手动更新星标等数据
4. 占位符清单在 README 末尾注释中，替换时对照查找

## 品牌规范

| 用途 | 值 |
|---|---|
| 用户名 | ErgeAIA |
| 称呼 | 宝藏二哥AIA |
| 品牌主色 | `#00D4FF` |
| 辅助色 | `#A855F7` |
| 深色背景 | `#0A1628` |

## GitHub Actions

`update-readme.yml` 通过定时 commit `.last-updated` 文件来触发 GitHub 重新渲染页面（shields.io 缓存）。支持手动 `workflow_dispatch` 触发。
