# Git/GitHub 版本管理与协作题目（10 分）

## 题目说明

使用 Git 管理整个工程，保留从 CAD、URDF、仿真、控制器、Linux、MCU 到 CAN 的真实开发历史。建立 `main`、`develop` 和按模块划分的 feature 分支；多人开发时使用 `feature/<姓名>/<模块>`，通过 Pull Request 合并并保留 Review 记录。

Commit 必须描述实际工作，例如 `feat: add wheelleg urdf`、`fix: correct joint axis`、`test: validate can frame parser`。禁止 `update`、`aaa`、`111`、`final` 等无意义信息。建议使用 v0.1.0 至 v1.0.0 的里程碑 Tag，具体要求见 [`../docs/development_log.md`](../docs/development_log.md)。

## 交付物

GitHub 仓库、可追溯的 Commit 历史、分支、Tag、Pull Request、Release，以及能证明每位成员贡献范围的记录。

## 评分

| 项目 | 分值 |
| --- | ---: |
| Git 仓库与远程配置 | 1 |
| 分支结构与命名 | 2 |
| Commit 开发历史 | 2 |
| Tag/Release 里程碑 | 2 |
| Pull Request 与 Review | 1 |
| 多人协作和贡献证明 | 2 |

## 严重扣分

最后一次性上传全部内容、模块只有 `Add everything` 历史、冒用他人代码或没有对应分支/PR 证据时，只能按可证明的实际贡献评分。
